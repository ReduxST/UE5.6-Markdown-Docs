# Importing Datasmith Content into Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine)  
**Processed:** 2025-06-14 16:30:17

---

This page describes how to use Datasmith to import content from a supported 3D design application or file format into Unreal Engine.

## Prerequisites

Before you can import content with Datasmith, you might have to enable some Unreal Engine plugins or install additional software.

### Datasmith Plugins

To import content into Unreal Engine using Datasmith, your project must have the **Datasmith Importer** plugin enabled. If you don't enable the plugin, you won't see the Datasmith import options in Unreal Engine. Some supported file formats require additional plugins.

-   For a list of supported applications, file formats, and plugin requirements, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).
-   To learn how to enable plugins in Unreal Engins, see [Customizing Unreal Engine](/documentation/en-us/unreal-engine/customizing-unreal-engine).

If you start your project from one of the **Architecture** or **Automotive, Product Design, and Manufacturing** templates, some or all of the Datasmith plugins are enabled by default.

### Additional Software

To import some supported file formats, you must install additional software. The following file formats have specific software requirements:

| File Format | Requirement |
| --- | --- |
| `.wire` | Install a version of Autodesk Alias AutoStudio that is compatible with your `.wire` file. |

## Import Datasmith Content into Unreal Engine

1.  In Unreal Editor, open the project that you want to import Datasmith content into.
    
2.  If you want to bring your content into an existing Level in your project, open it now. Otherwise, create a new Level or use the default Level.
    
3.  In the main toolbar, open the Create menu and select **Datasmith > File Import**. A file import dialog opens.
    
    ![The Datasmith import option in the Create menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fc57557-b1c2-4611-9dce-2701624d7bfd/datasmith-import-menu.png "The Datasmith import option in the Create menu")
4.  Select the file you want to import, and click **Open**. A file dialog opens.
    
5.  Choose a location in your project to store the imported content, and click **OK**. The **Datasmith Import Options** dialog opens.
    
    To create a new top-level folder for your Datasmith content, right-click an empty area in the file dialog. To create a subfolder of an existing folder, right-click that folder.
    
6.  In the **Datasmith Import Options** dialog, select the types of content that you want to import from your source file, and set the other import options as needed.
    
    ![Set import options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b85e645-e4fb-4d62-80c4-c09960dce9ae/unrealdsimportoptions-1.png "Set import options")
    
    The **Datasmith Import Options** dialog displays different import options for different file types. For more information about import options, see [Datasmith Import Options](/documentation/en-us/unreal-engine/datasmith-import-options-in-unreal-engine).
    
7.  When you finish setting the import options, click **Import**. Datasmith Does the following:
    
    -   Reads the imported file.
    -   Creates new Assets in your project.
    -   Places the Datasmith Scene into the current Level.
    
    For more information about the import process, see the [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview).
    

## Customizing the Import Process

You can customize the Datasmith import process in the following ways:

-   Use Blueprints visual scripting or Python scripts to automate the import. For details, see [Customizing the Datasmith Import Process](/documentation/en-us/unreal-engine/customizing-the-datasmith-import-process-in-unreal-engine).
-   Use Dataprep to perform additional operations on the data at import time. You can save and reuse Dataprep import recipes to create your own set of Asset import pipelines. For details, see [Dataprep Import Customization](/documentation/en-us/unreal-engine/dataprep-import-customization-in-unreal-engine).