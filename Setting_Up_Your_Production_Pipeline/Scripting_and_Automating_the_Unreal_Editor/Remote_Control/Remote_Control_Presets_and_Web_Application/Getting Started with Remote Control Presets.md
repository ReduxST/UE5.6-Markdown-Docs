# Getting Started with Remote Control Presets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/getting-started-with-remote-control-presets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/getting-started-with-remote-control-presets-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:57

---

With **Remote Control Preset**, you can collect and organize any UI parameters or functions in a single panel and expose them to the Remote Control API. These parameters and functions can be connected to widgets in a companion web application provided by the **Remote Control Web Interface** plugin to control the engine remotely.

![Remote Control panel in action](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b7be262-eb05-4873-b222-391a9966407c/rem-con.gif)

This page covers how to expose properties and functions from the Unreal Editor to the Remote Control API. For more details on all the settings in the Remote Control Panel, refer to [Remote Control Panel Reference](/documentation/en-us/unreal-engine/remote-control-panel-reference-for-unreal-engine).

## Prerequisites

The **Remote Control API** plugin provides the web server that hosts the data and websocket connections for the **Remote Control Preset**.

Follow these steps to enable the plugin for your project.

1.  Open your project in the Unreal Editor.
    
2.  In the Editor's main menu, choose **Edit > Plugins** to open the **Plugins** window.
    
3.  In the **Plugins** window, find the **Remote Control API** plugin in the **Messaging** category. Check its **Enabled** checkbox.
    
    ![Remote Control API plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/471ea7a9-8a6d-4481-96e3-97e31f739459/rm-cn-pl.png)
4.  Restart the engine.
    

## Exposing Properties to the Remote Control Panel and Remote Control API

The **Remote Control Panel** in the **Unreal Editor** is where you can collect properties from multiple objects in the level together for easy access. You can also add functions to the panel and call them from the panel. When properties and functions are exposed to the **Remote Control Panel**, they are also exposed to the **Remote Control API**. This helps an operator easily organize any items that they need to control in a live environment.

Follow these steps to add a **Remote Control Preset** and open the **Remote Control Panel**.

1.  Press **Add** in the **Content Drawer** and navigate to the **Miscellaneous** section. Select **Remote Control Preset**.
    
    ![Remote Control Preset menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4b662bf-b047-4348-b7ca-87394f60cbfe/rm-mn-op.png) ![Remote Control Preset in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8faa014a-beb6-438a-8957-db1b1d62c7f0/rem-con-cnbr.png)
2.  Open the **Remote Control Panel** by double-clicking the **Remote Control Preset Asset**.
    
    ![Empty Remote Control Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6761e6db-83c4-4ce9-acc1-08788ceae674/rm-cnt-pn.png)
3.  Check the **Edit Mode** checkbox.
    
    ![Edit Mode checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc0a8b11-5499-46fd-9cd1-61fe9bc1f59b/ed-md-ch.png)
4.  In the **Details** panels for **Assets**, every property now has the settings menu for that property (three dots).
    
    ![Remote Control settings menu in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fa6e164-c241-48f0-9d3d-1855cb0510d8/dt-pn-d.png)
5.  Left-click on the setting menu to see a closed or open eye icon.
    
    ![Remote Control eye icons in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a275887c-9285-4d71-941b-ba8d30366677/dt-pn-ye.png)
6.  The eye icon determines whether a property is added to the **Remote Control Panel**:
    
    -   An **open** eye icon means the property **is** added to the Remote Control Panel.
    -   A **closed** eye icon means the property **is not** added to the Remote Control Panel.
    -   Clicking on an open eye icon closes it, and vice versa; the property is added or removed from the Remote Control Panel accordingly.
7.  When the property is in the Remote Control Panel, it has the same interface as in the **Details** panel.
    
    ![Remote Control panel interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6808c9a0-0730-428c-a4cc-34440529f744/rm-pn-in.png) ![Details panel interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b15883b-c3a0-4a7f-89b4-b08f20b03db7/dpni.png)
    
    A Light Color property with RGB values in the Remote Control Panel (left) and in the Details panel (right).
    
8.  Right-click on the **Remote Control Preset** and select **Save** to keep your changes.
    

## Exposing Properties and Functions via Blueprint Library

This feature is experimental and may change in the next release.

You can use a Blueprint Library to expose properties, functions, and Actors to the Remote Control API and automate the process of populating a Remote Control Preset. Refer to [Blueprint API](https://docs.unrealengine.com/BlueprintAPI/) for more details on how to expose these using Blueprints.

In the following example Blueprint, the function is set up to expose all trees of the class **Light\_BP**.

Click image to expand.

When the function is run, the Remote Control Preset will show all the trees of the class **Light\_BP**.

Click image to expand.

## Next Steps

In this guide, you learned how to expose properties to the Remote Control API and create a Remote Control Preset. Refer to the following documentation for using these exposed properties in a live environment:

-   [Remote Control Web Application](/documentation/en-us/unreal-engine/remote-control-web-application-for-unreal-engine)
    
-   [Remote Control Protocols](/documentation/en-us/unreal-engine/remote-control-protocols-in-unreal-engine)