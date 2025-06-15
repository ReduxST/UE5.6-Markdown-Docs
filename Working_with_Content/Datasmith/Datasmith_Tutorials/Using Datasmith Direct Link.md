# Using Datasmith Direct Link

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-direct-link-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-direct-link-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:40

---

**Datasmith Direct Link** is a feature found in many Datasmith Exporter plugins that can incrementally update the viewport in an Unreal Engine-based application, such as **Twinmotion**, with the push of a button.

|   |   |
| --- | --- |
| ![Archicad Direct Link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad4c0f27-9d2f-4c7b-9203-53eb4ea46d70/archicad-directlink.png "Direct Link open in Archicad") | ![Collab Viewer Direct Link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0901f5a0-f9f2-49f0-9211-b65cff616a42/collab-viewer-directlink.png "Direct Link options open in the Collab Viewer template") |
| Source Application | Destination Application |

With the Direct Link workflow, you can set up a Datasmith Direct Link between one or more source applications and multiple destinations such as an Unreal Engine-based application or Twinmotion.

![Direct Link Diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef422dd6-8569-4c84-a2c1-0c20412c82ca/directlink-diagram.png "Illustrating how Direct Link connects Sources and Destinations")

Datasmith Direct Link allows multiple Source applications to connect to one or more Destinations.

This link updates your Unreal Engine Level or Twinmotion model, removing the need to re-export a `*.udatasmith` file from your source every time you make a change. This makes it easier to update and visualize incremental changes to your 3D scene in near real time.

## Setting up a Direct Link Connection

Getting started with the Datasmith Direct Link workflow begins with creating the connection between your 3D application and your Unreal Engine-based application.

1.  Download and install the appropriate Datasmith Exporter plugin for your application. You can download the appropriate plugin [here](https://www.unrealengine.com/en-US/datasmith/plugins). For more information on using the Datasmith Exporter plugin with your application, see [Datasmith Software Interop Guides](/documentation/en-us/unreal-engine/datasmith-software-interop-guides-for-unreal-engine).
    
    ![Archicad Plugin Install](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d037de3-b9bb-4bb0-a515-59917f32753b/archicad-install.png "Archicad Plugin install")
    
    Installing the Datasmith Exporter plugin for Archicad.
    
2.  Once you have installed the Datasmith Exporter plugin for your 3D application, check to ensure the Datasmith features are enabled. This will depend on your application.
3.  Open your destination application and select your 3D application as the **Source**.
    
    ![Direct Link Destination setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a292910e-14d6-4ccc-be44-df8ec62e143a/directlink-destination-setup.png "Setting up the Direct Link Destination")
    
    Datasmith options panel in the Collab Viewer template.
    
    For example, when running a local session in a project setup with the **Collab Viewer** template, press and hold the **spacebar** and select the **Datasmith** options to add one or more Direct Link sources to the Level. For more information on using the Collab Viewer template, see [Collab Viewer Template Quick Start](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine).
    
4.  Back in your source application, sync your Direct Link connection by clicking the Synchronize with Direct Link button.
    
    ![Archicad Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/664958cb-8824-447a-8e4d-800503b8d15b/archicad-toolbar.png "The Archicad Datasmith toolbar")
    
    Sync your changes between applications by clicking the Synchronize with Direct Link button.
    

## Using Direct Link in Packaged Projects

To use Direct Link in packaged projects, you must take an additional step to enable UDP messaging for your project's `.exe` file.

1.  From Windows Explorer or another file explorer, go to your project folder, then open the `WindowsNoEditor` folder.
2.  Right-click your project's executable file and, from the context menu, select **Create Shortcut**.
    
    ![Creating a shortcut to the packaged Unreal Engine project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ea09074-51d1-4b6d-ada8-0b5b8e6712ee/create-shortcut.png)
3.  Right-click the shortcut you created and, from the context menu, select **Properties**.
    
    ![Opening the properties of the newly created shortcut](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7689e2f0-e5b6-411c-be34-d2b258af9aae/shortcut-properties.png)
4.  In the shortcut's **Properties** window, add the `-messaging` parameter to the **Target** property.
    
    For the current example, the full line would look like this: `"C:\Users\admin\Documents\Unreal Projects\DirectLinkTest\WindowsNoEditor\DirectLinkTest.exe" -messaging`
    
    ![Adding a parameter to the shortcut's target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2fd0a70-9364-4e5a-8857-967f437685af/target-parameter.png)
5.  Click **OK** to save your changes.

## End Result

With the Direct Link connection established, you are now able to update your Unreal Engine or Twinmotion models with the push of a button.

![Direct Link Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e392544-d836-4b53-b80c-0194433ec9dc/directlink-example.gif "Example of Direct Link working between Archicad 24 and the Collab Viewer template.")

Disabling the **Use Less CPU when in Background** option enables the engine to update the 3D viewport when the Unreal Engine window is not focused and when a Pawn in the level is not possessed. This option is found in the **Editor Preferences** under **General > Performance**.