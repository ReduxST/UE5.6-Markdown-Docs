# Animation Pose Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:25

---

In **Unreal Engine**, animation **Pose assets** are stored [skeletal mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) poses that you can use in your project, as an animation target or reference point.

![animation pose asset in content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f4f89e0-96ac-4a18-9006-64b72799689c/contentbowser.png)

Pose assets save the position of the mesh geometry as well as the skeleton data. Pose assets can contain a single static pose, or many poses, saved as animation curves within the asset.

## Creating Pose Asset

There are many ways to create an animation Pose asset.

While working in the [Skeleton Editor](/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine), [skeletal mesh editor](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine), or the [animation sequence editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine), you can create a pose asset, using the **create asset** button in the [animation editor](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) **Toolbar** to save the current skeletal mesh position as an animation Pose asset.

![create a pose asset with the create asset button in the animation editors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/286e3932-06e8-41d0-b089-da5db66d3d21/creatassetbutton.png)

You can also create an animation Pose asset from an entire [animation sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) by **right-clicking** the asset in the **Content Browser** and selecting **Create > Create PoseAsset** from the context menu.

![create a pose asset in the content browser by right clicking and slecting create pose asset in the context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cec1a416-d4ed-4732-9bd1-2fc800152d0b/createposeasset.png)

After selecting **Create PoseAsset**, the Create Pose Asset window will open, where you can select which animation sequence you wish to create an animation pose asset from.

![select the animation sequence to generate a pose asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ce24b0d-70be-45fb-b6d4-3b8ce64af69a/poseassetwindow.png)

When generating a Pose asset from an entire **animation sequence**, Unreal Engine will create a pose for each frame of animation. The generated poses will then be accessible using [animation curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) present in the Pose Asset.

You can sequentially input any desired names for the generated pose curves by typing a name on a new line for each curve or frame of animation, in the **\[OPTIONAL\] Pose Names** field.

![name pose curves in the option pose names field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32995031-b863-47a6-b98b-721580433046/name.png)

### Additive Pose Assets

After creating and opening a Pose Asset, you can modify a pose asset, to behave as additive by toggling the **Additive** property and selecting the **Convert to Additive Pose** button in the pose asset's **Asset Details Panel**.

![additive pose asset setting in the pose asset details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/090a8c84-6b91-41d4-81a8-50ec9609b79c/additive.png)

Additive pose assets are able to play in an additive capacity, in conjunction with other animation data, such as animation sequences, without overriding the entire pose.

## Using Pose Assets

Pose assets can be used in many ways to animate characters.

### Pose Blender

You can use the **Pose Blender** and **Pose Driver** animation blueprint nodes, to control the playback and blending of animation Pose assets to animate characters at runtime.