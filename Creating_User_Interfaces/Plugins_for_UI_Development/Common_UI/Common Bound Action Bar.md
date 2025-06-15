# Common Bound Action Bar

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-common-bound-action-bar-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-common-bound-action-bar-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:21

---

User Interfaces can map Input Actions to onscreen buttons. For example, an options menu with multiple tabs may use the left and right shoulder buttons on a gamepad to toggle between multiple tabs. Interactions such as these are highly contextual, therefore, CommonUI includes a widget called the **Common Bound Action Bar**, which shows all Input Actions in your currently active UI in a single, easily referenced location. Typically, this widget is placed across the bottom of the screen.

### How the CommonBoundActionBar / NavBar Works

`UCommonBoundActionBar` updates on Tick. The final bar update is implemented in the function *UCommonBoundActionBar::HandleDeferredDisplayUpdate*. Any Input Actions that have the `bDisplayInActionBar` property set to `true` are gathered, sorted, then added to a list for display.

This update is bound to the **Action Router** delegate `UCommonUIActionRouterBase::OnBoundActionsUpdated_`\_, which fires during various node change points in CommonUI. Node changes occur whenever a widget activates or deactivates, so this is a perfect point to trace available action changes.

However, `UCommonUIActionRouterBase` is a local player subsystem, which means it relies on the local player for Ticking. This means that when games pause Ticking to display a menu, `UICommonBoundActionBar` will not update dynamically as the available CommonUI actions change, because it depends on the player's Tick process.

Not all actions are added to the action bar, nor do they have to be. `FBindUIActionArgs::bDisplayInActionBar` determines if an Input Action will get added to the action bar. This is exposed in Blueprints through the **Display In Action Bar** setting, and you can also access it with `UCommonUserWidget::bDisplayInActionBar` in C++.

As a possible workaround, you can enable Ticking while paused for the Actor or local player who owns player interactions or your UI. You can also make subclasses of widgets and set those to be tickable when paused.

## Implement the CommonBoundActionBar in Your UI

To set up the Common Bound Action Bar:

1.  Add a CommonBoundActionBar to your Widget Blueprint. The Content Examples project anchors it to the bottom of the screen in **CommonUI\_ActivatableWidgetsKB**. You can find this widget in **ExampleContent** \> **UMG** \> **CommonUI** \> **ActivatableWidgetsKB**.
    
    ![The ActivatableWidgetsKB Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64ed6d49-667c-45a7-acf4-7dafc47fa428/activatablewidgetskb.png)
2.  Create a class that derives from `UCommonBoundActionButton`. In the Content Examples project, this widget is named **NavigationBarAction**.
    
    ![Selecting the Common Bound Action Button class for a new Widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6371af6-fed5-4e80-92a3-64d3a45c4bf2/navbaractionclass.png)
3.  For a simple implementation, use a **Common Input Action** widget and a **Common Text Widget** in a horizontal box. The Common Input Action widget displays your button icons, while the Common Text Widget displays the friendly name for the Input Action.
    
    ![Composition of a simple Common Bound Action Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6c2bc1b-59dc-41bc-96da-5011368e0ca4/textactionname.png)
4.  Name your Common Text Widget "**Text\_ActionName**". `UCommonBoundActionButton` binds the text widget to the InputAction's text based on this specific name.
    
    If you do not rename your Common Text Widget to "Text\_ActionName", your Blueprint will fail to compile.
    
5.  Add your CommonBoundActionButton to the **Action Button Class** for your CommonBoundActionBar.
    
    ![Setting the Action Button Class in the CommonBoundActionBar's Details pannel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f329c0e3-b30a-4925-b06c-813fe68a6a15/actionbuttonclass.png)
6.  Select the CommonUI widgets in your UI whose actions you want to display in the CommonBoundActionBar, then set **Display in Action Bar** to **true**. In C++, this is represented with `bDisplayInActionBar`.
    
    ![The Display In Action Bar setting in the widget's Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11726cca-2744-4911-88b1-5a99ffcdde6d/displayinactionbar.png)
    
    `bDisplayInActionBar` is a member of `UCommonUserWidget` and its derived classes, like `UCommonButtonBase`. Like Input Actions themselves, it is not available in base UMG's library of widgets.
    
7.  Make sure that the widgets containing the Input Actions you want to display are **Activated**. This means that either the widgets themselves must be Activatable Widgets, or they must be children of an Activatable Widget.
    

Activatable Widgets start in a deactivated state by default. You can call `UCommonUserWidget::Activate` to manually activate these widgets, or you can use the **Auto Activate** setting (UCommonActivatableWidget::bAutoActivate) to make them self-Activate on being added to the Viewport.

When playing, assuming the widgets containing your actions are activated, the actions should display in the navigation bar.