# 3ds Max

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-3ds-max-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-3ds-max-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:43

---

This page provides a quick description of the Datasmith 3ds Max Exporter plugin, and instructions for how to install it.

![V-Ray in 3ds Max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c8572a5-e3a4-4b4f-9030-7c6a90cc77cb/max_datasmith_compare_vray.png)

![Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8a2c8c1-d04f-4363-9ac5-72522e110228/max_datasmith_compare_unreal.png)

Images courtesy of Litrix.

## Datasmith 3ds Max Workflows

Use Datasmith to bring 3ds Max content into **Unreal Engine** in the following ways:

-   **Export a `.udatasmith` file**: export 3ds Max content as `.udatasmith` files, and import those files into Unreal Engine. For details, see [Exporting Datasmith Files from 3ds Max](/documentation/en-us/unreal-engine/exporting-datasmith-files-from-3ds-max-to-unreal-engine).
-   **Set up a Direct Link**: create a live connection between an instance of 3ds Max and an instance of Unreal Engine (or another Unreal Engine-based application), then push 3ds Max content to Unreal Engine automatically or as-needed. For details, see [Synchronizing 3ds Max and Unreal with Direct Link](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine).

For detailed information about how Datasmith translates 3ds Max content for Unreal Engine, see [How Datasmith Translates 3ds Max Content](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine).

## Installing the Datasmith Exporter plugin for 3ds Max

Before you can synchronize or export 3ds Max content, you must download and install the **Datasmith 3ds Max Exporter plugin** from the [Datasmith Export Plugins page](https://www.unrealengine.com/en-US/datasmith/plugins).

To see what versions of Autodesk 3ds Max the plugin supports, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

### Pre-Install Checklist

Before you install the Datasmith 3ds Max Exporter plugin:

-   Close all running instances of 3ds Max.
-   Download the installer for the exporter plugin that matches the Unreal Engine version you intend to use.
-   Uninstall all previous versions of the Datasmith 3ds Max Exporter plugin.

### Install or Remove the Plugin

After you download the installer, open it, and follow the instructions on-screen.

If you need to uninstall the Datasmith 3ds Max Exporter plugin, you can do this from the **Control Panel**, like any other Windows application.

## Configuring an Unreal Engine Project for Datasmith

To import a `.udatasmith` file into Unreal Engine, or synchronize a 3ds Max Scene with Unreal Engine, your project must have the Datasmith Importer plugin enabled. If you don't enable the plugin, you won't see the Datasmith options in Unreal Engine.

If your project uses the Architecture template, the Datasmith Importer plugin is enabled by default.

### Enable the Datasmith Importer Plugin

1.  In Unreal Engine, open the Plugins window: from the main menu, select **Edit > Plugins**.
2.  In the left pane, select the **BUILT-IN > Importer** category.
3.  In the right pane, enable the **Datasmith Importer** plugin.