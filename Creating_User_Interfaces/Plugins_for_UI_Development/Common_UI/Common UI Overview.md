# Common UI Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-advanced-multiplatform-user-interfaces-with-common-ui-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-advanced-multiplatform-user-interfaces-with-common-ui-for-unreal-engine)  
**Processed:** 2025-06-14 16:40:49

---

**Common UI** supports the development of cross-platform UIs with complex navigation, such as menus with layers, submenus, or popups. Originally developed for UI in Fortnite, this plugin is available to Unreal Engine users through the **Plugins** menu. This page details the use-cases Common UI was designed to address, and the main concepts that drive its design.

## Problems Common UI Solves

### Navigating Multi-Layered Menus

The image below shows an example of a complex menu:

![The dual blade menus in Fortnite](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e4bbe91-249a-4cf2-ac08-ecd14e4c4900/blade-menu-example.png)

This UI shows two blade menus overlaid on top of a tabbed UI in the background. The background UI still exists, but cannot be interacted with if the top layer exists. **How is this selective interactivity achieved?**

Meanwhile, input methods can vary between different platforms and controllers. On PC, users select the UI elements above by clicking them with a mouse cursor. On consoles, however, the user selects UI elements using cardinal navigation and button presses. **How do we create a UI that works across multiple platforms, consoles, and PC?**

### Returning to the Correct Element

![Example of a popup window appearing in front of other menus.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/593c74ca-f264-4583-92b6-f202d2c15c56/popup-example.png)

Suppose the user sees a popup like the one in the image above. Then, the user closes the popup. **How does the UI return to the correct element for cardinal navigation?** If the overlay UI beneath the popup is then closed, then it will again need to find somewhere to return to. The solution to this problem must be applicable in a wide variety of circumstances.

### Console-specific UI Elements

![Example of an action bar showing button icons.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dbd3a28-1200-41b0-b968-6e75e0fe0163/button-icon-example.png)

In the image above, the UI displays the button to press for each interaction. However, these buttons' icons vary per console. **How do we create a UI that is indifferent to console-specific UI elements?**

### Common UI's Features

Common UI's features are designed to address the problems listed above. With Common UI, you gain:

-   Selective widget interactivity, providing an easy way of creating rich UIs with layering.
    
-   Multiplatform console and PC support.
    
-   On consoles:
    
    -   Cardinal navigation management, including breadcrumbs and history.
        
    -   Console-specific UI element management.
        

## Key Concepts

This section explains the design and main features of Common UI.

### Input Routing

On consoles and PC, interactivity is determined by input. To achieve *selective interactivity,* CommonUI uses **Input Routing**, which only permits certain widgets to receive input, whether from a mouse or a gamepad, at a given time.

![Input routing makes menus with many elements easier to manage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/355f0db1-4625-4d1b-828b-ce527f11dedd/inventory-example.png)

Input routing can also selectively distribute input across widgets. For instance, in the image above, the bumper buttons are always routed to the tab widget at the top, while the 'X' action button is routed to the widget currently selected by cardinal navigation.

For a deeper look, refer to `CommonGameViewportClient.h` and `CommonUIActionRouterBase.h` in Common UI's source code.

### Nodes

Common UI routes inputs to whatever UI widget is visually rendered on top. Common UI converts widgets into **nodes**, which handle input routing based on visual and logical hierarchies.

Nodes are organized into trees which, with a few exceptions, match the **Slate** hierarchy. Each tree consists of a root node, usually represented with a widget placed directly in the Viewport, as well as leaf nodes, usually represented with individual UI elements like buttons.

Once per tick, Common UI finds the tree of nodes painted higher than any other tree, then sends input to that tree's root node. That root widget will then forward input to the first leaf widget within the tree ready to handle input, which will then process the input or forward it again if needed.

![Flowchart showing input routing logic.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/976f5fc7-9a1b-429c-8a97-bef66d0fb31a/input-routing-chart.png)

For a deeper look, see **UIActionRouterTypes.h**.

### Activatable Widgets

Within Common UI, only certain widgets are converted into nodes for the purpose of handling input, and only widgets that are ready to handle input receive input. These widgets are called **activatable widgets**, and they are considered \_active \_if they are ready to receive input.

Activatable Widgets:

-   Can be toggled between active or inactive states, indicating if they are ready to receive input.
    
-   Can forward input to other activatable widgets within the same tree.
    
-   Can deactivate automatically when appropriate, such as when handling back actions.
    

With activatable widgets, if the user dismisses an overlay UI that is currently receiving input, the issue of returning to the correct element is trivial. Since input is only routed to the highest painted tree, we can leave widgets active without concern if they are on a lower UI layer. Once that upper level UI is dismissed, Common UI routes input to the still-active widgets in the next-highest UI layer.

For a deeper look, refer to `CommonActivatableWidget.h`.

## Further Reading

For detailed information about how to set up Common UI for first-time use, refer to the [Common UI Quickstart Guide](/documentation/en-us/unreal-engine/common-ui-quickstart-guide-for-unreal-engine).

## Content Examples

For a basic example of Common UI in action, look at the Common UI content sample. For a more advanced example that includes a full frontend menu, download the Lyra sample project.