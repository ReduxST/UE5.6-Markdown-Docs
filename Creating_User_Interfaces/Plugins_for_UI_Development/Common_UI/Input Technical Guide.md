# Input Technical Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/commonui-input-technical-guide-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/commonui-input-technical-guide-for-unreal-engine)  
**Processed:** 2025-06-14 16:14:27

---

**CommonUI's** input system manages cross-platform input support, especially for complex or multi-layered menus. This guide provides detailed information about how CommonUI's input system works, including:

-   Handling navigation with the **synthetic cursor**.
    
-   Capturing input in the viewport.
    
-   How the Input Router determines which widgets receive input.
    
-   How individual widgets affect and respond to the Input Routing process.
    
-   Altering the way widgets respond to Input Routing.
    

To set up Input Routing support for your project, refer to the instructions in the [CommonUI Quickstart guide](/documentation/en-us/unreal-engine/common-ui-quickstart-guide-for-unreal-engine).

## Gamepad Navigation With Synthetic Cursors

In CommonUI, several gamepad interactions are driven by an invisible synthetic cursor. That means that if you set up your UI to work with a mouse, all you need for CommonUI to behave correctly is for an invisible cursor to be in the right location and click like a mouse. This setup simplifies the flow for cross-platform input by funneling it all through one input path.

This section details how the synthetic cursor and basic input work. It starts with the basics of how the synthetic cursor registers a click in the general **Unreal Motion Graphics (****UMG)** and **Slate**\-based input flow. It then moves into the specifics of how CommonUI's implementation diverges from it.

### Click With the Synthetic Cursor/Gamepad

This section demonstrates how the Synthetic Cursor works. It uses the input flow for an '**Accept**' or '**Default Click**' action on a gamepad as an example.

![Chart illustrating how CommonUI handles clicks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1d160f7-58c1-4908-afe7-b76f7fa6449c/click-routing.png)

Typically, the virtual Accept key should map to `EKeys::Virtual_Accept`. Internally, Input flow starts from a platform-specific application that derives from `GenericApplication`. For example, Windows uses `FWindowsApplication`.

This input is processed by the `FSlateApplication` using `FSlateApplication::ProcessKeyDownEvent`. That method uses input processors that implement the `IInputProcessor` interface to process, and possibly **handle** the input. When input is handled, it prevents further processing. `FCommonAnalogCursor`, like its parent class `FAnalogCursor`, is an `IInputProcessor`. \_It attempts to handle the key down input in `FCommonAnalogCursor::HandleKeyDownEvent`.

FCommonAnalogCursor does not handle the input for standard 'Accept' actions on the gamepad that aren't captured by **Bound Actions** on the current widget. Instead it forwards the input to `FAnalogCursor::HandleKeyDownEvent`. `FAnalogCursor` then creates a synthetic mouse click event for the `FSlateApplication` to process.

At this point, this mouse event goes through a similar input processing process as regular clicks, and triggers the final click.

To investigate the regular click input flow, add a breakpoint to `SButton:OnMouseButtonDown`.

#### Troubleshooting Synthetic Cursor Clicks

If CommonUI's synthetic cursor clicks do not behave as expected, the source of the problem is likely to be one of `FPointerEvent`'s processes.

The following are a few possible issues you could encounter:

-   The FPointerEvent is not handling input for the correct user.
    
-   The synthetic cursor is not close to the expected position.
    
-   When the click is processed in `FSlateApplication::ProcessMouseButtonDownEvent`, another widget that has capture is affecting the `FWidgetPath`. This can occur based on the `MouseCaptureMode` of your Input Config.
    
-   The `FWidgetPath` is generated naturally based on position using `FSlateApplication::LocateWindowUnderMouse`.
    

`FWidgetPath` contains the list of widgets the input might be routed to.

### How Synthetic Cursors and Gamepads Navigate and Focus

Speaking purely in terms of navigation, CommonUI does not behave differently than the base implementation of UMG. This section provides details about this process for your convenience.

As in the previous section, input starts with a platform-specific application. This section uses the example of an arrow key or analog movement. The Input Routing system routes this UI navigation input to a widget within the UI.

In this example, when navigation occurs, assume that the widget isn't specialized to handle this specific navigation input.

![Chart illustrating how CommonUI handles Navigation Focus](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07409f22-d4cf-43d2-9cdc-e33c0828710d/navfocusrouting.png)

When navigation input occurs, the input is handled by the default `SWidget::OnKeyDown` or `SWidget::OnAnalogValueChanged` methods. However, these default methods do not directly change widget focus. Instead, the following occurs:

1.  The navigation method uses either `FSlateApplication::GetNavigationDirectionFromKey` or `FSlateApplication::GetNavigationDirectionFromAnalog` to translate the input into a navigation direction. It takes the Navigation Config for the widget into account when it runs this translation.
    
2.  The navigation direction is captured and included in the `FReply::Handled` reply, which is sent through `FReply::SetNavigation`.
    
    `FReply` can carry a lot of contextual information. For more see the information on [FReply](/documentation/en-us/unreal-engine/commonui-input-technical-guide-for-unreal-engine#changehowwidgetsrespondtoinput) in the Input Routing section below.
    
3.  Slate starts processing the `FReply` using `FSlateApplication::ProcessReply`, which causes navigation to occur. If a navigation event is loosely defined by direction, then `_FSlateApplication::AttemptNavigation` \_attempts to find the correct widget to navigate to.
    
4.  If possible, `FSlateApplication::ExecuteNavigation` navigates to the destination widget.
    
5.  If the destination widget is valid, `FSlateApplication::SetUserFocus` is called on that widget. This happens whether the destination widget was specified directly, or found beforehand.
    
6.  After the Slate focus navigation occurs, `FCommonAnalogCursor::Tick` automatically **moves and centers the synthetic cursor onto the focused widget** during the next tick.
    

This makes it possible to use hover effects when you use a gamepad.

### Customize Synthetic Cursor Behavior in CommonUI

You can provide your own analog cursor or synthetic cursor in CommonUI. There are many reasons you might want to do this. For example, if you are attempting to make keyboard navigation that functions similarly to a gamepad, you could make `FCommonAnalogCursor::Tick` snap to the center of a widget even when not using a gamepad. Alternatively, you could make the synthetic mouse visible, and perhaps implement some sort of tween between focus changes.

To create a custom cursor:

1.  Derive from `UCommonUIActionRouterBase`
    
2.  Override `UCommonUIActionRouterBase::MakeAnalogCursor` to return your custom analog cursor class.
    

`UCommonUIActionRouterBase::ShouldCreateSubsystem` does not create an instance of itself if you override it with your own action router class.

Keep in mind that **Input Processors are run on all input**. This includes input for the Unreal Editor. You can use `FCommonAnalogCursor::IsGameViewportInFocusPathWithoutCapture` to help distinguish between your application and things outside of it.

## CommonUI Input Routing

The following is a brief, high-level overview of the Input Routing process:

1.  CommonUI organizes Activatable Widgets into trees of nodes that handle navigation. Deactivated widgets are not added to the list of nodes, and therefore are never considered for Input Routing.
    
2.  CommonGameViewportClient captures input, then finds the topmost painted node in the hierarchy.
    
3.  The node checks to see if it can handle the input using one of its available Input Handlers. If none of its Input Handlers match the player's input, it can forward input to its topmost child node and repeat this step.
    

This process repeats recursively until all nodes are checked. The sections below provide more details about these steps and the components of this system.

### Input Routing Execution Flow

As described in the section on [Clicking With the Synthetic Cursror](/documentation/en-us/unreal-engine/commonui-input-technical-guide-for-unreal-engine#clickingwiththesyntheticcursor), Input Processors get the first opportunity to handle input events before Input Routing occurs. If an input event is not handled by an Input Processor, it goes through CommonUI's input routing flow.

#### Click Event Process

Input begins when a platform-specific application triggers FSlateApplication::ProcessKeyDownEvent.

![Chart illustrating how key input is routed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85cbb108-c8d2-48a4-877a-4eb381e9876b/keyinputrouting.png)

The Slate application then forwards the input event to a widget, based on the current focus path. In a game, this input event is usually `SViewport::OnKeyDown`, which then forwards the key down to whichever class implements the current viewport interface. Forwarding the key down usually triggers `FSceneViewport::OnKeyDown`.

Finally, the scene viewport forwards the input to the InputKey method of the current game viewport client. In CommonUI's case, this is `UCommonGameViewportClient::InputKey`. This is why the game viewport class must be set to **CommonViewportClient** for CommonUI to function properly.

Refer to the [CommonUI Quickstart guide](/documentation/en-us/unreal-engine/common-ui-quickstart-guide-for-unreal-engine) for more information about setting the Viewport Client class.

#### Action Router Process

CommonUI's specific implementation of Input Routing begins once input is forwarded to the game viewport client. `UCommonGameViewportClient::InputKey`\_ \_gives the **A****ction Router** the opportunity to handle input in `UCommonGameViewportClient::HandleRerouteInput`. If this is successful, it will then call UCommonUIActionRouterBase::ProcessInput.

If the input isn't handled, the game attempts to process the input through the normal method when the Common Game Viewport client calls `Super::InputKey`.

![Chart illustrating the Action Router process](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0f66547-5adc-4715-aa7f-8409a8e72044/actionrouterprocess.png)

Activatable Widgets are abstracted as nodes in a tree using `FActivatableRootNode`. Nodes are arranged in a hierarchy based on the hierarchy of Activatable Widgets in the UI's widget tree. Parent nodes act as **root nodes**, while their children are considered **child** or **leaf nodes**. Refer to the [CommonUI Overview](/documentation/en-us/unreal-engine/overview-of-advanced-multiplatform-user-interfaces-with-common-ui-for-unreal-engine) for more information.

The Action Router maintains the currently-active root node in the tree of Activatable Widgets. `UCommonUIActionRouterBase::ProcessInput` tells the root node to attempt to process the input by calling `FActivatableTreeNode::ProcessNormalInput`. This recursively tells all child nodes to attempt to process the input.

`FActivatableTreeNode` is an `FActionRouterBindingCollection`, which maintains a list of all the Action Bindings on the node's Activatable Widget. If all child nodes within the current node fail to process input, the current node calls `FActionRouterBindingCollection::ProcessNormalInput`. As a binding collection, the current node checks all of the widget's Action Bindings. If any Action Bindings match the corresponding key, then the related behavior is executed and the input is considered handled.

## Modify The Input Routing System

The following are the main methods you should use to change the Input Routing system:

-   Derive a new Viewport class from `UCommonGameViewportClient` and override any of its input handling methods. Then, in the Project Settings, set the game viewport to your derived class.
    
-   Derive a new class from `UCommonUIActionRouterBase` and override any of its virtual functions.For example, you could override `UCommonUIActionRouterBase::ApplyUIInputConfig` for custom [Input Config](/documentation/en-us/unreal-engine/input-fundamentals-for-commonui-in-unreal-engine#changeyourapplicationsuiinputhandlingwithinputconfigs) settings.
    

`UCommonUIActionRouterBase::ShouldCreateSubsystem` does not create an instance of the base Action Router if you override it with your own action router class.