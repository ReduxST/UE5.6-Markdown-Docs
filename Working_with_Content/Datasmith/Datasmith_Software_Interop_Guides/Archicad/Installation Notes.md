# Installation Notes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-plugin-for-archicad-installation-notes](https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-plugin-for-archicad-installation-notes)  
**Processed:** 2025-06-14 16:18:57

---

Windows macOS Linux

Before you can begin exporting your Archicad content, you will need to download the [Unreal Datasmith Exporter for Archicad](https://www.unrealengine.com/en-US/datasmith/plugins).

To see what versions of Graphisoft Archicad the plugins support, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

We encourage you to share the download link for the Datasmith Exporter plugins with any number of people, both inside and outside of your organization. Please note that users are not permitted to distribute the Datasmith Exporter plugins themselves.

## Installing the Datasmith Plugin for Archicad

1.  Close any running instances of Archicad that you may have running on your machine. If any instances are currently running, the installation will fail.
    
2.  If you already have an older version of the Datasmith Exporter plugin installed, we recommend first uninstalling it before proceeding. For details, see [Removing the Datasmith Exporter for Archicad](/documentation/en-us/unreal-engine/datasmith-plugin-for-archicad-installation-notes#removingthedatasmithexporterforarchicad).
    
    Graphisoft provides their own Datasmith Exporter for Archicad. Epic Games recommends removing the Graphisoft plugin before installing its own Datasmith Plugin for Archicad.
    
3.  Download the Datasmith Exporter plugin installer from the [Datasmith Exporter Plugins download](https://www.unrealengine.com/en-US/datasmith/plugins) page.
    
4.  When the download is complete, navigate to the location of the file and run the installer.
    
    ![Datasmith Archicad Installer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76f615cb-c15c-401e-bb96-aeac6249ccfc/image_14.png)
    
    The Unreal Datasmith Exporter for Archicad Setup Wizard.
    
5.  Follow the on-screen instructions and accept the license agreement to continue.
    
6.  The installer automatically detects which versions of Archicad have installed on your system. Check the box for each version you want to export to Datasmith and click **Install**.
    
    ![Archicad Version Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b8da312-179c-4f59-9bc9-1e8412f2e47b/image_15.png)
    
    Select which versions of Archicad you want to use with the plugin.
    

1.  Close any running instances of Archicad that you may have running on your machine. If any instances are currently running, the installation will fail.
    
2.  If you already have an older version of the Datasmith Exporter plugin installed, we recommend first uninstalling it before proceeding. For details, see [Removing the Datasmith Exporter for Archicad](/documentation/en-us/unreal-engine/datasmith-plugin-for-archicad-installation-notes#removingthedatasmithexporterforarchicad).
    
    Graphisoft provides their own Datasmith Exporter for Archicad. Epic Games recommends removing the Graphisoft plugin before installing its own Datasmith Plugin for Archicad.
    
3.  Download the Datasmith Exporter plugin installer from the [Datasmith Exporter Plugins download](https://www.unrealengine.com/en-US/datasmith/plugins) page.
    
4.  Open an instance of Archicad and open the Add-On Manager by opening the **Options** menu and selecting **Add-On Manager**.
    
    ![Mac Install Step 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27399f53-e724-49c8-84cf-ce0ef118f897/mac-step-1.png)
    
    Opening the Add-On Manager.
    
5.  Navigate to the **Edit List of Available Add-Ons** section and click the **Add** button.
    
    ![Mac Install Step 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b1a6e39-9c2c-42d9-a68c-b320f7fb1102/mac-step-2.png)
    
    Adding a new add on in Archicad.
    
6.  Navigate to the location of the Datasmith Exporter for Archicad file andselect the package that corresponds with your version of Archicad. Click ok to continue.
    
    ![iMac Install Step 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b30241f3-117b-45d9-9925-1a4262bcbd23/mac-step-3.png)
    
    Navigate to the location of the Datasmith Exporter for Archicad install file and select the package that corresponds with your version of Archicad.
    

### End Result

With the Datasmith Exporter plugin installed, you can now use the Direct Link workflow and export scenes from Archicad as `.udatasmith` files. See [Exporting Datasmith Content from Archicad](/documentation/en-us/unreal-engine/exporting-datasmith-content-from-archicad-to-unreal-engine).

Epic Games releases a new version of the Unreal Datasmith Exporter plugin for Archicad with every new release of Unreal Engine. If you switch to a different version of Unreal Engine, remember to download and install the matching version of the plugin.

## Removing the Datasmith Exporter for Archicad

Use the standard control panel utilities for your system to find and remove the Unreal Datasmith Exporter for Archicad application.

For example, on Windows 10, you can use the **Apps & features** control panel.

![Apps and Features Control Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75a9f604-bf27-4366-9871-db002b6354b5/image_16.png)

Search for the Datasmith plugins in the Apps & features control panel.

Click the entry for your Datasmith Exporter plugin in the list, then click **Uninstall**.

Alternatively, use the **Uninstall or change a program** window from the Control Panel. Right-click the entry for your Datasmith exporter plugin, and choose **Uninstall** from the contextual menu.

![iUninstall or Change a Program Control Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f96bb5b-9834-4213-a6f4-8b234abc3f8f/image_17.png)

Removing a Datasmith plugin using the Uninstall or change a program control panel.

Use the Add-On Manager inside Archicad to remove the Unreal Datasmith Exporter for Archicad.

1.  Open the Add-On Manager by clicking on the **Options** menu and selecting **Add-On Manager**.
2.  Click the checkbox next to **Datasmith for ARCHICAD** in the **Available Add-Ons** list to disable the add-on.
3.  Click the Remove button to remove the plugin.

![Mac Uninstall](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/064f82f2-e0a5-48d3-a7e4-5877d2fce759/mac-uninstall.png)

Removing a Datasmith plugin using the Add-on Manager.