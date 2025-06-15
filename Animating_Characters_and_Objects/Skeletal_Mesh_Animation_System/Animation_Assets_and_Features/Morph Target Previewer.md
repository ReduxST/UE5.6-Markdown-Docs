# Morph Target Previewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/morph-target-previewer](https://dev.epicgames.com/documentation/en-us/unreal-engine/morph-target-previewer)  
**Processed:** 2025-06-14 16:36:50

---

The **Morph Target Previewer** previews any **Morph Targets** (sometimes called "morphs" or "blend shapes") that are applied to a **Skeletal Mesh**. Each **Morph Target** is additively blended into the existing **Skeletal Mesh** geometry. Multiple morph targets can be combined to create a complex vertex-driven animation, which is often ideal for such things as facial expressions.

The **Morph Target Previewer** window is visible by default whenever any [Animation Editor](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) is open.

## Interface

The **Morph Target Previewer** panel has two main sections:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2153926c-9243-4327-bebc-35c1d7e08092/morphtargetpreviewerinterface.png)

1.  Search Bar
2.  Morph Target List

The Search Bar filters the list of **Morph Targets** to quickly find the one you need. Type the first few letters of the desired target and the list will begin filtering. You can also right-click on a **Morph Target**, which will pop-up a dialog box with additional actions, such as **Delete** or **Copy Morph Target Names**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f524fbac-176e-4ae6-adb1-76fb038b9ef0/rightclickdelete.png)

## Creating Morph Targets

You can import **Morph Targets** as a part of a **Skeletal Mesh**, as well as independently (from a given mesh). This is supported via the FBX file format.

For more information on the setup procedure, as well as how to import Morph Targets into Unreal, please see [FBX Morph Target Pipeline](/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine).

## Using Morph Targets

Once your Morph Targets are in place, you will need to set up your [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) to utilize them. This is done within your Event Graph via the **Set Morph Target** node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7150255-13aa-4760-ac62-8e11c99ec289/setmorphtarget.png)

| Pin | Description |
| --- | --- |
| Input Pins |   |
| Execution | An execution wire to trigger the effect of the node. |
| Target | The target **Skeletal Mesh**. For most circumstances, this will point to "self". |
| Morph Target Name | The name of the **Morph Target** being edited. |
| Value | A float value (between 0.0 and 1.0) used to set the value of the **Morph Target** being edited. |
| Output Pins |   |
| Execution | Passes execution on to the next node. |

## Morph Target Debug View Mode

You can enable this view mode to easily see what vertices are affected by each Morph Target.

1.  In the viewport window, click on **Show** > **Mesh Overlay** >, and then **Selected MorphTarget Vertices**.
2.  Now select any **Morph Target** from the **Morph Target Preview** panel to see the debug view.

## Optimization

For target platforms that support Shader Model 5, you can enable the GPU calculation of morph targets. This means that the CPU does not have to perform the calculations if your game is CPU bound, and you have GPU processing to spare. This feature can be activated in the **Project Settings**, as follows:

1.  On the file menu, go to **Edit** > **Project Settings**.
2.  Open the **Rendering** section of **Project Settings**.
3.  In the **Optimizations** category, find the **Use GPU for computing morph targets** checkbox and enable it.

Click for full image.