# Transform Bone

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-transform-bone-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-transform-bone-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:46

---

You can use the **Transform (Modify) Bone** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node to transform (**Translation**, **Rotation**, and **Scale**) a specified bone.

![transform bone animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5d5be6d-1a35-45bf-9768-34a079f2e380/transformbone.png)

After selecting a bone to control with the **Bone to Modify** property, you can select the kind of transform mode within the **Translation**, **Rotation**, and **Scale** property sections. Here the character's `upperarm_l` has been selected and additive transforms are being made using the controller in the viewport.

![transform modify bone animation blueprint node demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42805c76-542b-4a6a-a1fe-ab8d878dcbe0/demo.gif)

The Transform Bone node operates within **Component Space**, so a [space conversion](/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine) will need to occur to implement the node within your character's Animation Blueprint.

## Property Reference

![transform bone animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb2527fd-f46a-48cc-a5af-aa95addc6031/details.png)

Here you can reference a list of the Transform Bone node's properties.

| Property | Description |
| --- | --- |
| **Bone To Modify** | Select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to control with the Transform Bone node. |
| **Translation** | 
Control the **translation** of the selected bone. By default the translation coordinates are controllable in the AnimGraph.

With the **Translation Mode** property you can set the node to **Ignore** the modifications made by the node, retaining any existing translation on the bone, **Replace Existing** to replace any translation on the bone with the translation the node is performing, and **Add to Existing** which will add the Transform Bone's translation to any existing Translation on the bone.

You can also set the **Translation Space** of the node to control the space the translation is applied. You can set the following options:

-   **World Space**: Applies the translation based on the absolute position in world space.
-   **Component Space**: Applies the translation based on the bones position in relation to the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)'s reference frame.
-   **Parent Bone Space**: Applies the translation based on the bones position in relation to its parent bone.
-   **Bone Space**: Applies the translation based on the bone's own reference frame.



 |
| **Rotation** | 

Control the **rotation** of the selected bone. By default the rotation coordinates are controllable in the AnimGraph.

With the **Rotation Mode** property you can set the node to **Ignore** the modifications made by the node, retaining any existing rotation on the bone, **Replace Existing** to replace any rotation on the bone with the rotation the node is performing, and **Add to Existing** which will add the Transform Bone's rotation to any existing rotation on the bone.

You can also set the **Rotation Space** of the node to control the space the rotation is applied. You can set the following options:

-   **World Space**: Applies the rotation based on the absolute position in world space.
-   **Component Space**: Applies the rotation based on the bones position in relation to the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)'s reference frame.
-   **Parent Bone Space**: Applies the rotation based on the bones position in relation to its parent bone.
-   **Bone Space**: Applies the rotation based on the bone's own reference frame.



 |
| **Scale** | 

Control the scale of the selected bone. By default the scale coordinates are controllable in the AnimGraph.

With the **Scale Mode** property you can set the node to **Ignore** the modifications made by the node, retaining any existing scale on the bone, **Replace Existing** to replace any scale on the bone with the scale the node is performing, and **Add to Existing** which will add the Transform Bone's scale to any existing scale on the bone.

You can also set the **Scale Space** of the node to control the space the scale is applied. You can set the following options:

-   **World Space**: Applies the scale based on the absolute position in world space.
-   **Component Space**: Applies the scale based on the bones position in relation to the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)'s reference frame.
-   **Parent Bone Space**: Applies the scale based on the bones position in relation to its parent bone.
-   **Bone Space**: Applies the scale based on the bone's own reference frame.



 |