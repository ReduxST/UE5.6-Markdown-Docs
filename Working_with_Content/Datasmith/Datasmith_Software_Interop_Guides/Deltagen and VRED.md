# Deltagen and VRED

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-deltagen-and-vred-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-deltagen-and-vred-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:48

---

This page describes how Datasmith imports scenes from 3DExcite Deltagen and Autodesk VRED into Unreal Editor. It follows the basic process outlined in the [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [About the Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine), but adds some special translation behavior that is specific to Deltagen and VRED. If you're planning to use Datasmith to import scenes from Deltagen or VRED into Unreal Editor, reading this page can help you understand how your scene is translated, and how you can work with the results in Unreal Editor.

Datasmith currently only works with VRED Professional. It does not support VRED Design.

## Workflow

### Deltagen

Datasmith uses an **Export** workflow for Deltagen. This means that to get your Deltagen content into Unreal using Datasmith, you need to:

1.  Export your Deltagen scene to an `.fbx` file using the export feature built in to Deltagen.
    
2.  Enable the **Importers > Datasmith FBX Importer** plugin for your project, if it is not already enabled. Restart Unreal Engine if prompted.
    
3.  On the Main Toolbar, click the Datasmith button. Then, from the **All Files** drop-down, select **DeltaGen Fbx files**. file. See See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).
    

### VRED

Datasmith uses an **Export Plugin** workflow for VRED. This means that to get your VRED content into Unreal using Datasmith, you need to:

1.  Install a plugin script for VRED, and use it to export your VRED scene to an `.fbx` file. See [Exporting Datasmith Content from VRED](/documentation/en-us/unreal-engine/exporting-datasmith-content-from-vred-to-unreal-engine).
    
2.  Enable the **Importers > Datasmith FBX Importer** plugin for your project, if it is not already enabled. Restart Unreal Engine if prompted.
    
3.  On the Main Toolbar, click the Datasmith button. Then, from the **All Files** drop-down, select **VRED Fbx files**. file. See See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine)..
    

To read more about other types of Datasmith workflows, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

## Variants

The Datasmith Importer does not support look variants from Deltagen.

The Datasmith FBX importer for Deltagen and VRED brings the variants and variant sets that you've defined in your Deltagen or VRED scene into a new **LevelVariantSets** Asset that it creates in your **Content Browser**. It also places an instance of this Asset into your Level.

Double-click this Asset to open the **Variant Manager** window. You can use this window to switch between different variants and variant sets while you're working in the Unreal Editor. You can use a dedicated set of Blueprint functions provided by the **LevelVariantSets** Actor to switch variants at runtime. You can also customize your variants further, making each variant affect more objects in the Level, or triggering custom Blueprint functions each time it is activated.

It is up to you to decide how the user running your Unreal project should choose between these variants at runtime, and to write the code that triggers the appropriate Blueprint functions. For example, you might want to create a UI or a set of menus where users can select variants, or you can configure your project to switch variants in response to key presses or other inputs. The Datasmith importer and the Variant Manager do not create these UI or menus for you — they only give you all the tools you need to create them yourself.

For more information on the Variant Manager and how it works, see [Working with Scene Variants](/documentation/en-us/unreal-engine/working-with-scene-variants-in-unreal-engine).

To see an example of how to use the Variant Manager with a UI generated from the variants, see the [Product Configurator template](/documentation/en-us/unreal-engine/product-configurator-template-in-unreal-engine).

## Animations

If your Deltagen or VRED scene contains any animated scene elements, the Datasmith FBX importer brings those animations into Unreal as **Level Sequences**. You can use the **Sequencer** tool in the Unreal Editor to work with and edit the animations, use Blueprints to control and play back the animations in your project at runtime, and take advantage of all the other features of the Sequencer tool described in the [Sequencer documentation](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview).

For important information about working with Sequencer animations imported by Datasmith, see also the Animations section of [About the Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine#animations).