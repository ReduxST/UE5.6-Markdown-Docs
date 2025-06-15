# Remote Control Web Application

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-web-application-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-web-application-for-unreal-engine)  
**Processed:** 2025-06-14 16:46:39

---

Parameters and functions exposed in the [Remote Control Preset](/documentation/en-us/unreal-engine/getting-started-with-remote-control-presets-in-unreal-engine) can be connected to widgets in a companion web application provided by the **Remote Control Web Interface** plugin to control the engine remotely. This web application has a built-in UI editor so you can customize its interface without any additional code to create or format it.

![Remotely editing post process contrast using a widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffbdb74d-7eb6-418e-98c1-0ff43477a46d/rm-con-pst.gif)

Since this is a web application, you can run multiple clients at the same time. Any properties that are modified in one client will have their changes propagated through the web server to all the other clients. This can help create a collaborative workflow in a live environment.

This page covers how to connect exposed properties and functions to widgets in the companion Remote Control web application, and build your own UI with the application's UI builder.

## Prerequisites

The **Remote Control Web Interface** uses NodeJS to provide a companion web app with default widgets, such as gauges, sliders, and color pickers, for controlling the engine remotely without any additional code.

Follow these steps to connect the web application to your project:

1.  [Install NodeJS](https://nodejs.org/en/download/) on your machine.
    
    1.  Minimum version: 8.
        
    2.  Maximum version: 14.15.5.
        
2.  Open your project in the Unreal Editor.
    
3.  In the Editor's main menu, choose **Edit > Plugins** to open the **Plugins** window.
    
4.  In the **Plugins** window, find the **Remote Control Web Interface** plugin in the **Messaging** category. Check its **Enabled** checkbox.
    
    ![Remote Control web interface plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b4a19ec-c517-42c2-a7c8-5b048ef90403/01-rem-con-w-i.png)
5.  Restart the engine.
    
6.  Verify the web app launched successfully. In the Editor's main menu, choose **Window > Developer Tools > Output Log** and filter by "remote control web" to see a success log similar to: LogRemoteControlWebInterface:
    
    `[Success] Remote Control Web Interface is running - WebApp started, port: 7000`
    
    ![Success message displayed in the output log](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f190b852-3c89-4104-9fa4-305a060e7879/02-com-l.png)

## Getting Started with the Remote Control Web Application

Connect properties and functions in the Remote Control Panel to a web application. The web application will read any Remote Control Preset that you have open in your Unreal session. The following browsers are officially supported: Chrome, Firefox, and Safari.

To see updates in the Editor as you change property values in the web app, open **Edit > Editor Preferences** and, in the **Performance** section under **General**, disable **Use Less CPU when in Background**.

![Use Less CPU in the Background setting in the Editor Preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7e7b437-7725-4173-847f-75b8fb6fd039/03-les-cpu.png)

Follow these steps to launch the web application and add an exposed property:

1.  Open your web browser on the same machine running the engine and enter the URL 127.0.0.1:7000. See the Remote Control Quick Start for details on how to expose the Remote Control API to other machines.
    
    ![Enter the URL in your browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8edb4c80-5dfc-4b34-b3c0-f5d8e1e4551f/enter-url.png)
    
    You can change which port the **Remote Control Web Interface** uses for your project. In the Editor's main menu, choose **Edit > Project Settings…** to open the **Project Settings** window. In the **Project Settings** window, select **Remote Control** in the **Plugins** section to see its settings, where you can change the default port.
    
    ![Remote control web interface plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/003fe0fb-e2c8-4b4f-8cfb-3a2cc11737e7/05-rem-web-prt.png)
    
    You can also launch the web application from the **Remote Control Preset**. See [Remote Control Panel Reference](/documentation/en-us/unreal-engine/remote-control-panel-reference-for-unreal-engine#menu) for more details.
    
2.  When the page loads, you should see a blank Remote Control application. Click the **Control** toggle in the web application to switch to **Design** mode so you can start adding widgets.
    
    ![Mode toggle in Control mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec139294-3323-48c0-af5e-da4d35085d77/mode-toggle-control.png) ![Mode toggle in Design mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2510801f-fe97-4cec-a4d2-a46800c4ca98/06-des-but.png)
3.  Select the **Properties** tab.
    
    ![Remote control properties tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e12f83b0-80e8-41d6-bae6-298da1be72b5/07-prop-b.png)
4.  Drag and drop one of the exposed properties into the right panel. When you add a property from the **Properties** panel, a **Panel Widget** is created if one doesn't currently exist, and the associated widget for the property is added to the Panel Widget.
    
    In the following example, a Panel Widget was created and a Color Picker Widget added to the Panel Widget. The Color Picker is bound to the **Contrast** field for the scene's **PostProcessVolume**.
    
    ![Color Picker Widget bound to Post Process Volume Contrast property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59baf4e2-c6fe-4aa1-b1c1-336a1c6dca77/08-con-arr.png)
5.  Switch to **Control** mode.
    
    ![Color Picker Widget in Control mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf53f39f-a4ee-4752-9514-8cc41071090b/09-con-web.png)
6.  Modify the exposed property in the web app and verify the associated property is updated in the Editor.
    
    ![Remotely editing post process contrast using a widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e22ad17a-0893-42f9-a9ba-71792705be57/rm-con-pst.gif)
7.  Save your changes to the web application by saving the corresponding Remote Control Preset in the Unreal Editor. The next time you open the web application, the layout will be the same as when you last saved the Asset.
    

## Presets

You can have multiple remote presets available in the web application, but you can only have one Remote Control Preset open at a time. In **Design** mode, go to the **Presets** section to see the available remote presets on the left side of the window and select the one you want to view. The name of the currently opened Remote Control Preset is displayed in the top right of the window.

![Multiple presets in the Remote Control window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/003ad56f-06b9-403b-b0c5-44033da1a9e4/10-1rem-pr.png)

## Tabs

You can have multiple Tabs in your web application. This is helpful for creating different views for the operators in a live environment.

-   You can change a Tab's label and choose an icon from a library of icons to differentiate the Tabs.
    
-   You can also duplicate a Tab to use as a starting point for a new interface.
    

![Multiple tabs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8f31445-aa6c-4180-b170-66ca910b8bf9/11-tab-pn.png)

There are two unique tabs you can add to your web application that are already set up to work with other Unreal tools: [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine) and [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine). The sections below describe these integrations with Remote Control.

### Level Snapshots Integration

In the Remote Control Web Application, you can take new snapshots of the level or switch to a previously taken snapshot remotely. For more details on using Level Snapshots in your project, see [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine).

![Remote Control Level Snapshots](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbd8c893-00dd-4d03-999b-3b2839f4bd9c/lvl-sn-in.jpg)

The Level Snapshots plugin must be enabled to use this feature in the Remote Control Web Application.

### Sequencer Integration

In the Remote Control Web Application, you can view all the sequences in your project, filter them by name, and select a sequence to view. For more details on using sequences in your project, see [Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine). By clicking the Play button icon to the right of a sequence, you can start or resume a sequence in the current level. There may be a short delay before the sequence begins to play.

Sequences in the page will be listed by their asset name and not the name listed in the outliner. Assets renamed after being placed in the world will still be listed by their name in the content browser.

![Remote Control Sequencer integration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3558b92-89e6-48f6-9d04-a9c70d9a8f94/sequencer-integration.png)

This tab shows all sequences in the project, but you can only play the sequences that exist in the current level. The filter is only based on the asset path, so you currently cannot filter based on which sequences are in the level.

## Widgets

Widgets are included in the web application to represent interactable data formats in the engine, and to provide formatting for the web page.

![Adding Panel widgets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa6476fd-8c0a-4024-9a8a-a6d6ffdfa65c/paneldrop.gif)

The following list shows all of the available widgets you can add to your UI:

-   Button
-   Color Picker
-   Dial
-   Dropdown
-   Joystick
-   Label
-   List
-   MiniColorPicker
-   Panel
-   Slider
-   Spacer
-   Tabs
-   Text
-   Toggle
-   Vector

A **Panel** widget is used to contain all the other widgets and must be placed before placing other widgets. A **List** widget is used to contain **Panels** and provide multiple UIs in the same **Tab**.

![Adding List widgets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a65882ce-fa6a-41c3-989e-bb7b2795b560/listwidgets.gif)

## Properties

The properties and groups listed in the Properties tab of the Remote Control Web Application directly match the properties and groups in the Remote Control Preset.

![Comparing properties in Web Application and Preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb77f3be-aca9-4734-af8d-33e027a881c8/14-com-pan.png)

Drag and drop a property from the left tray of the web application over the canvas area, to add a widget already bound to the property in your UI. If the property is released over a panel, it will automatically be added to it. If there are no panels it will create an empty one for you and wrap it inside.

![Add a property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64d89e7b-5a7c-44d4-a406-8465d8b4c3ba/propertywidget.gif)

## Widget and Property Settings

When you select a widget in the web page during **Design** mode, a settings panel appears in the bottom left corner of the window. Different fields appear depending on the type of widget and data it represents.

For every widget type, you can change its label. If the widget is bound to a property, you can change which property it's connected to.

### Widget Modes

Some data formats, such as vectors, can be represented in multiple ways in the UI.

Follow these steps to change the mode for your widget.

1.  Select the widget you want to view to open its settings panel.
    
2.  In the widget's settings panel, select the mode you want to use. For example, with vectors, you can choose a **Joystick**, **Dial**, or **Sliders**.
    
    ![Select a widget's mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e840480-6554-4133-95ed-9fa851bec3b7/15-rel-loc.png)
3.  A game controller icon appears next to the property when you select a mode. Select this button to open the property in the mode you selected.
    
    ![Click game controller button to open property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0f41707-b6c5-40fb-bb9f-3844618f58c3/16-vec-wid.png)
4.  The mode appears at the bottom of the window.
    
    ![Widget mode appears at the bottom of the screen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dff07b80-9054-4c15-ae0b-dac1f0adfb30/17-dil-wid.png)

### Deleting Widgets

You can delete widgets individually, or delete all the widgets in a Panel at the same time. To delete a widget, select the widget to open its settings panel and select **Delete Widget**. To delete all the widgets in the Panel, select the Panel to open its settings panel and select **Delete Widget**.

![Deleting widgets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d94be5d7-00fa-4b2a-a622-f1a9f56a898d/delete-widget.gif)