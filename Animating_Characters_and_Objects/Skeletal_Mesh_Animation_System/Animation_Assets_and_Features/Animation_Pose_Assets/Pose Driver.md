# Pose Driver

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pose-driver-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pose-driver-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:58

---

You can use the **Pose Driver** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node to drive [Pose Assets](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) using [animation curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) values to animate characters.

![pose driver aniamtion blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53707b89-a67d-4d45-8fab-401d9a0897fe/posedrivernode.png)

While the [Pose Blender](/documentation/en-us/unreal-engine/pose-blender-in-unreal-engine) and [Pose by Name](/documentation/en-us/unreal-engine/pose-blender-in-unreal-engine#posebyname) Animation Blueprint nodes are used to blend Pose Assets with existing animation poses, the Pose Driver node is used to drive the contained poses within a Pose Assets to animate characters.

With the Pose Driver node, you can use bone motion to drive the Pose Asset playback at runtime.

|   |   |
| --- | --- |
| ![pose driver demo using animation sequence curves to drive anim curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6b55be3-afc5-42ab-a87a-6d5b919b9b3e/armdemo.gif) | ![anim graph with pose driver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d09f42ce-075a-482c-a6d8-7272d01bad97/armdemo.png) |
| Viewport | Graph |

By selecting a Pose Asset, setting [Pose Targets](/documentation/en-us/unreal-engine/pose-driver-in-unreal-engine#posetargets) and a **Source Bone**, you can control the behavior of how the Pose Asset is driven using the source bone motion data.

When reselecting a Pose Driver node's pose asset, and importing a new set of poses using the **Tool** property, you must create a new **Pose Driver** node.

## Pose Targets

By assigning targets in the **Pose Targets** property, you can specify skeletal mesh poses from a **Pose Asset** or **Animation Curves** you want to target using the Pose Driver node. Pose targets can be manually entered or automatically assigned using the poses contained within a **Pose Asset**.

To import a Pose Asset's contained poses as Pose Targets, first, in the Pose Driver's **Details** panel, assign select a Pose Asset in the **Pose Asset** property.

![pose target properties in pose driver details panel add target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e500654-4377-4004-b13e-e6844d6354e3/addtarget.png)

Once a Pose Asset has been assigned, select the **Copy Poses** from Pose Asset option form the **Tool** property's context menu.

![tool drop down select copy poses from pose asset to import poses as pose targets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/afd97fd2-c395-45a2-9be4-f52e167c99bc/copyfromposeasset.png)

The imported Pose Targets are now controllable using the Pose Driver node.

### Pose Target Property Reference

![pose target property reference general](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89992311-accf-4200-8d0f-fd44fb2a8b4a/posetargetprop1.png)

The following properties control the behaviors of all of the Pose Driver node's Post Targets. Here you can reference a list of the Pose Target properties.

| Property | Description |
| --- | --- |
| **Solo Driven Pose / Curve Only** | Here you can toggle if the Pose Target is representative of an entire pose or just an Animation Curve. When enabled the property will only interpet curve data and leave the source joint(s) in place. When Disabled, all pose data will be used. |
| **Tools** | 
When the **Pose Driver** node has a pose asset set in the Pose Asset property, you can select the following options to dictate the behavior of the poses or curves driven by the Pose Driver. From the drop down menu you can select from the following options:

**Copy All from PoseAsset**: Create and set all Pose Targets from the associated animation poses from the set **Pose Asset**. When selected, this option will overwrite any existing pose targets. **Auto Scale**: Automatically set all **Scale** factors, based on distance to the nearest neighbor pose target.



 |
| **Add Target** | You can add a pose target with the **(+) Add Target** button. |

![pose target property reference specific](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79c1494c-5ea2-4e60-981d-7c8358b033aa/posetargetprop2.png)

The following properties can be adjusted for each individual Pose Target registered within the Pose Driver node. Here you can reference a list of the pose target properties.

| Property | Description |
| --- | --- |
| **Solo** | Clicking and holding the solo button will preview the pose target in the viewport. You can also Double-click the solo pose to lock the Pose Target pose preview. You can double-click on a locked pose's solo button to unlock its preview. |
| **Remove Target** | You can remove a target by selecting the **Remove Target** button, adjacent to the specific Pose Target you wish to remove. |
| **Scale** | Here you can set the Pose Target's curve or pose scale. A value of 1 will result in the full curve or pose value being used as the Pose Target. |
| **Drive** | Here you can select which pose from the set Pose Asset to drive using the Pose Target. |
| **Hidden** | When enable this property will hide this Pose Target from debug drawing. |
| **Override** | 
Here you can set an override the pose targets blending method and function. In the first field you can set the Blending Method form the following options:

-   **Euclidian**
-   **Quaternion**
-   **Swing Angle**
-   **Twist Angle**
-   **Default Method**

In second field you can select an override blending function from the following options:

-   **Gaussin**
-   **Exponential**
-   **Linear**
-   **Cubic**
-   **Quintic**
-   **Default Function**



 |
| **Curve** | Enable this property when the Pose Target is an [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) rather than an animation pose. When using animation poses as pose targets, disable this property. |
| **X**, **Y** and **Z** | Here you can reference and adjust the **X**, **Y**, and **Z** values of the Pose Target location. Which, by default, can be seen in the **Viewport** as a **green object**. If all values are set to Zero, the motion of the pose target will be isolated to the **Source Bone** and its **Children**. |

### Curve-Based Pose Targets

Pose Targets can also be driven by [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) instead of using a **Pose Asset**. In the Details panel of a **Pose Driver** node, set the **Drive Output** property to **Drive Curves**.

![drive output property in pose driver details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/beec09d5-f9a4-4a61-ace6-e542d4315676/driveoutput.png)

In the Pose Target section, enable the **Solo Driven Pose / Curve Only** and for each curve Pose Target, enable the *\*Curve*. After enabling the Curve property you can now edit the curve graph within the property window.

![curve property and graph in pose driver details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1062dcd7-35cd-42db-bf8b-c283c7305451/addcurve.png)

### Property Reference

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bda915b3-7d01-4889-af5d-0b56ea80a1af/details.png)

Here you can reference a list of the Pose Driver node's properties.

| Property | Description |
| --- | --- |
| **Source Bones** | Select a bone from the character's **skeleton** to use as a **Source Bone** to apply the driven animation pose parameters based on orientation. Many source bones can be added, but at least one is required. **Add (+)** Indexes, to define source bones to drive the pose orientation from. |
| **Eval Space Bone** | Here, you can select optional bones from the character's **skeleton** to evaluate the **Source Bone**'s transform. If not specified, the **local space** of **Source Bone** is used. |
| **Eval from Ref Pose** | 
When enabled, the Source Bone orientation and transform will be evaluated relative to its **Reference Pose** position. This is recommended when using **Swing** and **Twist Angle** as **Distance Method**, since the twist will be computed from the character's **Reference Pose**. When disabled, the **local space** of **Source Bone** will be used.

When **Eval Space Bone** is set, **Eval from Ref Pose** will be ignored.



 |
| **Only Drive Selected Bones** | When enabled, all bones that are not set in the **Only Drive Bones** property will be filtered out. |
| **Only Drive Bones** | Here you can add and select bones from the character's skeleton, to be exclusively used when the **Only Drive Selected Bones** property is enabled. |
| **Solver Type** | 

Here you can specify which type of blending solver to use. Typically, the **Additive** solver requires normalization, and the **Interpolation** solver does not. The **Interpolative** solver also has smoother blending, whereas the **Additive** solver requires more targets but has a more precise control over the influence of each target.

-   **Additive**: The additive solver sums up contributions from each target. It's faster but may require more targets for a good coverage, and requires the normalization step to be performed for smooth results.
    
-   **Interpolative**: The interpolative solver interpolates the values from each target based on distance. As long as the input values are within the area bounded by the targets, the interpolation is well-behaved and return weight values within the 0% - 100% limit with no normalization required. Interpolation also gives smoother results, with fewer targets, than additive but at a higher computational cost.
    



 |
| **Radius** | Here you can set the default radius for each target. |
| **Automatic Radius** | When enabled, the node will automatically pick the radius based on the average distance between targets. |
| **Function** | 

Here you can set the blending function to use. The options available are:

-   **Gaussin**
-   **Exponential**
-   **Linear**
-   **Cubic**
-   **Quintic**
-   **Default Function**



 |
| **Distance Method** | 

Here you can set the blending method to use. The options available are:

-   **Euclidian**
-   **Quaternion**
-   **Swing Angle**
-   **Twist Angle**
-   **Default Method**



 |
| **Twist Axis** | Axis to use when the **Distance Method** is set to **Swing Angle**. You can set the values of the axis limits on the **X**, **Y**, or **Z** axes. |
| **Weight Threshold** | Here you can set the weight, below which should be ignored, in the contribution from the target. |
| **Normalize Method** | 

Here you can set the method to use for normalizing the weight. The options include:

-   **Only Normalize Above One**: When values exceed 1, values will be normalized.
-   **Always Normalize**: Zero distribution weights stay zero.
-   **Normalize Within Median**: Normalize only within the **Median Reference** property values. The median is a cone with a **minimum** and **maximum** angle within which the value will be interpolated between non-normalized and normalized. This helps to define the volume in which normalization is always required.
    
-   **No Normalization**: Don't normalize at all. This should only be used with the interpolation method, if it is known that all input values will be within the area bounded by the targets.



 |
| **Median Reference** | When enabled, you can set the rotation or position of median limits used for normalization, when the **Normalize Method** is set to **Normalize Within Median**. |
| **Median Min** | Here you can set the minimum distance used for the median normalization method. |
| **Median Max** | Here you can set the maximum distance used for the median normalization method. |
| **Drive Source** | Here you can select which part of the transform is read, the **Rotation** or **Translation**, to apply the alpha to drive **Pose Targets**. |
| **Drive Output** | 

Here you can select if the Pose Targets are animation poses from a Pose Asset or animation curves to drive. You can select:

-   **Drive Poses**: Use target DriveName to drive poses from the assigned PoseAsset.
-   **Drive Curves**: Use the target's DriveName to drive curves.



 |
| **Pose Asset** | Here you can select a \*Pose Asset\*\* from your project to drive. |

### Debug Settings

![debug properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ef8f02b-e69c-4d52-8835-97923d83564f/debugprop.png)

Here you can reference a list of the Pose Driver node's debug settings.

| Property | Description |
| --- | --- |
| **Axis Length** | Length of axis in world unity used for debug drawing. |
| **Cone Subdivision** | Number of subdivisions / lines used when debug drawing a cone. |
| **Draw Debug Cones** | When enabled, the cones will be drawn in 3d for debugging. |