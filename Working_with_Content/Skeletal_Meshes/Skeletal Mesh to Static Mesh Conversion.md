# Skeletal Mesh to Static Mesh Conversion

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-to-static-mesh-conversion-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-to-static-mesh-conversion-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:49

---

When creating splash-screens, screenshots, or other in-game static versions characters, it can be helpful to non-destructively convert a posed [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) assets to [Static Mesh](/documentation/en-us/unreal-engine/static-meshes), in order to preserve its position and reduce the render cost of the still objects.

The following document will provide an example workflow of how to pose and convert a **Skeletal Mesh** asset to a **Static Mesh** asset in Unreal Engine.

#### Prerequisite

-   Your project contains a **Skeletal Mesh** character.

## Posing Skeletal Meshes

To begin posing a Character in Unreal Engine, open the Skeletal Mesh asset in the [Skeletal Mesh Editor](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7832a4e-03bd-4264-93b8-fd08c26fa118/skelmesheditor.png)

To expose the Skeletal Mesh's bones, in order to manipulate their position, navigate in the **Viewport** panel to **Character** > **Bones** and toggle the **All Hierarchy** option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/539390b4-d19f-4582-96c5-351f1593c46d/exposebones.png)

Select a bone to adjust by clicking on it, and then use the **Move**, **Rotate**, and **Scale** tools, to manipulate your character's pose.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7869737c-665f-4813-8c7d-a85bd8ba9f53/manipulatetools.gif)

## Saving Skeletal Mesh Poses

After Manipulating your character's pose to your desired position, you can then save the pose as a Static Mesh asset using the **Make Static Mesh** button in the Skeletal Mesh Editor's **toolbar**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64f434cb-3d9a-4019-b4ae-004a0a13e954/makestaticmesh.png)

**Name** and select a location to save the new Static Mesh asset, and then select **Save**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cc7831e-a1d7-422a-9df6-1ed2fc47666e/save.png)

You can now use your converted Static Mesh in your project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba0388d7-d051-4915-9d5a-025c6ef322b8/placestatic.gif)

After converting your Skeletal Mesh to a Static Mesh you can safely reposition your mesh to its reference pose by re-importing your Skeletal Mesh's `.fbx` source file using the **Reimport Base Mesh** button in the Skeletal Mesh Editor's **toolbar** or by manually reverting your manipulation edits using **Ctrl** + **Z**.

If you do not revert your bone manipulation edits, your Skeletal Mesh's Animation Sequences will not play properly.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1273300b-b1f0-4ecd-b294-0693f6942604/reimport.png)

You can also save posed Skeletal Meshes as [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) and [Pose assets](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) for other more dynamic use cases using the Create Asset button in the Skeletal Mesh Editor's toolbar.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b383fea7-71ae-4030-aefc-eded6c24fc7a/createasset.png)

For more information about using saved Skeletal Mesh poses, see the following documentation:

## Converting Multiple Skeletal & Static Meshes

You can also convert a group of Static or Skeletal mesh objects, that have been placed into a level, to a single Static Mesh asset, in order to pose multiple characters together, or combine characters with other objects such as backgrounds or weapons. After placing and positioning your objects in a level, you can multi-select each object you want to convert to a static mesh, and then navigate in the **Menu Bar** to **Actor** > **Convert Actors to Static Mesh**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8da2e746-60c0-4cf4-b679-eb77d1dc039c/convertinscene.png)

**Name** and select a location to save the new Static Mesh asset and then select **Save**. You can now use the converted Static Mesh in your project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9ee9bf8-0b4b-4901-8de9-4d12a2e56f99/staticscene.gif)

You can also convert groups of game objects to a single Static Mesh during **Play In Editor** (**PIE**), and other simulation modes within the editor, such as recorded gameplay segments using the [Rewind Debugger](/documentation/en-us/unreal-engine/animation-rewind-debugger-in-unreal-engine) to save more dynamic gameplay snapshots.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a71bb24e-8693-48ce-8bcc-305a13d2a0e4/pie.gif)