# Blend Space Analysis

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/automatic-blend-space-creation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/automatic-blend-space-creation-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:19

---

Placing samples accurately in the [Blend Graph](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#blendgraph) can be slow and tedious, especially if you are not sure exactly what characteristics the animations have. **Blend Space Analysis** can be used to calculate a range of relevant properties, and to then automatically place your samples in the Blend Space.

This document provides an overview of the Blend Space Analysis system in Blend Spaces.

#### Prerequisites

-   You have an understanding of [Blend Spaces](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine).
-   Your project has a Skeletal Mesh character with the necessary imported animations to use as samples in the Blend Space graph.

Blend Space Analysis cannot be used for Blend Space nodes created in Animation Blueprints.

## Enabling Analysis

Blend Space Analysis can be enabled for all [Blend Space types](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#blendspacecreationandtypes) by setting the analysis axis function properties located in the **Asset Details** panel. Setting the **Axis Function** to a value other than **None** will enable Blend Space Analysis, and the value to select depends on the kind of Blend Space you are creating. For example, if you are creating an [Aim Offset](/documentation/en-us/unreal-engine/aim-offset-in-unreal-engine), then typically you may want to select **Orientation**.

![blend space analysis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a94d67cb-75d4-4d03-b1b2-471eed556f49/enableanalysis.png)

The following **Axis Functions** are available for use:

| Axis Function | Description |
| --- | --- |
| **None** | Disables analysis for this axis. |
| **Position** | Calculates the position of a Bone or Socket averaged over the duration of the sample. |
| **Velocity** | Calculates the velocity of a Bone or Socket averaged over the duration of the sample. |
| **Delta Position** | Calculates the change in position of a Bone or Socket over the duration of the sample. |
| **Orientation** | Calculates the orientation (roll, pitch and yaw) of a Bone or Socket averaged over the duration of the sample. |
| **Orientation Rate** | Calculates the rate of change of roll/pitch/yaw of a Bone or Socket averaged over the duration of the sample. |
| **Delta Orientation** | Calculates the change in roll/pitch/yaw of a Bone or Socket over the duration of the sample. |
| **Angular Velocity** | Calculates the angular velocity as a rotation vector (in degrees per second) averaged over the duration of the sample. |
| **Locomotion** | Estimates the locomotion velocity of a biped character based on the foot movements. |
| **Root Motion** | Estimates the locomotion velocity of a character based on the motion of the root (requires root motion data in the animation sequences). |

### Analysis Properties

Selecting any of the Axis Function types will reveal additional properties, which are used to configure the analysis. Most of these properties are common for all types, however there are some that are exclusive to certain types.

![analysis properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d83d82a-750a-4f8c-b0c9-daac54bf05bf/analysisproperties.png)

| Name | Description |
| --- | --- |
| **Axis** | 
The axis of the Bone or Socket to analyze. Depending on the chosen Axis Function, there will be a different **Axis** to select:

-   **Position**, **Velocity**, **Delta Position**, and **Angular Velocity** provides **X**, **Y**, or **Z** for the analysis axis.
-   **Orientation**, **Orientation Rate**, and **Delta Orientation** provides **Pitch**, **Roll**, or **Yaw** for the analysis axis.
-   **Locomotion** and **Root Motion** provides **Speed**, **Direction**, **Forward Speed**, **Rightward Speed**, **Upward Speed**, **Forward Slope**, and **Rightward Slope** for the analysis axis.



 |
| **Bone/Socket** | This specifies the Bone or Socket to analyze. If **Axis** is set to **Locomotion**, then two Bone/Socket properties are required, one for each foot. Some analysis functions will also use the orientation of the Bone for calculating Pitch, Roll, or Yaw values. In these cases, you need to ensure that the **facing** and **right** axes are set correctly, depending on how the character's skeleton is set up. |
| **Bone Facing Axis** | The forward-facing axis of the selected Bone or Socket if **Orientation**, **OrientationRate**, or **DeltaOrientation** is selected as the Axis Function. |
| **Bone Right Axis** | The right-facing axis of the selected Bone or Socket if **Orientation**, **OrientationRate**, or **DeltaOrientation** is selected as the Axis Function. |
| **Space** | 

The spatial coordinates in which to perform the analysis, so you can calculate the position and orientation of one Bone with respect to another. You can select the following spatial coordinates:

-   **World** space represents the space the character is in at the start of each animation sequence, and can be determined from the viewport axis display.
-   **Fixed** space uses the space of a particular bone or socket, without updating it during the animation sequence. Using it, you can specify your own "world space" coordinate frame using the Bone or Socket from the first frame of the animation sequence.
-   **Changing**, which is similar to **Fixed**, but the space is updated for each frame that is analyzed in the animation sequence.
-   **Moving** space, which is similar to **Changing**, except that the velocities are also calculated relative to the Bone space.



 |
| **Analysis Space Bone/Socket** | If Space is set to either **Fixed**, **Changing**, or **Moving**, then this is where you specify the Bone or Socket to use for the spatial analysis. |
| **Character Facing Axis** | 

The facing direction of your character, which can be determined from the viewport axis display. Typically this should be set to **+Y**.

![character facing axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca2b6183-250d-43e4-be94-7c779d173329/characterfacingup.png)

 |
| **Character Up Axis** | The upward direction of your character, which can be discerned from the viewport axis display. Typically this should be set to **+Z**. |
| **Start Time Fraction** | The normalized start time of the animation sample to analyze. You may want to adjust this if you only want a certain section of an animation to be analyzed. |
| **End Time Fraction** | The normalized end time of the animation sample to analyze. You may want to adjust this if you only want a certain section of an animation to be analyzed. |

## Analysis Examples

The following are some examples of how you can use Blend Space Analysis to populate your Blend Space graph.

### Aim Offset

If you want to automatically place your [Aim Offset](/documentation/en-us/unreal-engine/aim-offset-in-unreal-engine) samples, you can use Blend Space Analysis in the following way. This example will assume you have already created an Aim Offset Asset.

In the Aim Offset Asset Details panel, locate both the **Horizontal Axis Function** and **Vertical Axis Function** properties and set them to **Orientation**.

![aim offset analysis orientation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc93321e-3feb-4677-b047-8a1dc1856fbe/aimoffset1.png)

Additional [analysis properties](/documentation/en-us/unreal-engine/automatic-blend-space-creation-in-unreal-engine#analysisproperties) will appear under each Axis Function. Under **Horizontal Axis**, set the following properties:

-   Set **Axis** to **Yaw**, which will analyze the selected Bone or Socket along its yaw (sideways) axis.
-   Set **Bone/Socket** to your character's **weapon** or **prop Bone** that the weapon attaches to. In most cases this will be the weapon bone on the right hand.
-   Set **Bone Facing Axis** to match the direction the weapon will be aimed when attached to the Bone. In most cases this will be **+X**.
-   Set **Bone Right Axis** to match the right-facing direction of the weapon when attached to the Bone. In most cases this will be **+Y**.

![aim offset horizontal axis properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/317b357f-cac3-4ca8-aa27-5f50a3a8265f/aimoffset2.png)

Under Vertical Axis Function, set the following properties:

-   Set **Axis** to **Pitch**, which will analyze the selected Bone or Socket along its pitch (up and down) axis.
-   Set **Bone/Socket** to your character's **weapon** or **prop Bone** that the weapon attaches to. In most cases this will be the weapon bone on the right hand.
-   Set **Bone Facing Axis** to match the direction the weapon will be aimed when attached to the Bone. In most cases this will be **+X**.
-   Set **Bone Right Axis** to match the right-facing direction of the weapon when attached to the Bone. In most cases this will be **+Y**.

![aim offset vertical axis properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ef06bba-d994-4a17-9122-dac9dcfb188f/aimoffset3.png)

You can now drag in your samples from the **Asset Browser**. Doing this will analyze and automatically position them within the blend graph. The graph will also automatically adjust its ranges and grid divisions based on the analysis.

![add samples to analyze](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3d38e57-ad04-4fce-a527-b6eaba71fdc2/aimoffset4.gif)

Press **Ctrl** and move your cursor in the graph to preview the results.

![preview analysis results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9fceb7f-d47f-411b-ab90-ce342430326a/aimoffset5.gif)

After analyzing your samples, you may need to adjust the axis ranges for your Blend Space so that they encompass your samples more accurately.

### Locomotion

This example will create a Blend Space that controls forward movement on the vertical axis, and sideways / strafing movement on the horizontal axis. We will assume you have already created a Blend Space Asset.

In the Blend Space Asset Details panel, locate both the **Horizontal Axis Function** and **Vertical Axis Function** properties and set them to **Locomotion**.

![locomotion analysis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6cca86d-8c25-440e-90f5-d34a5b3e03a4/locomotion1.png)

Additional analysis properties will appear under each Axis Function. Under **Horizontal Axis**, set the following properties:

-   Set **Axis** to **Rightward Speed**.
-   Set **Bone/Socket 1** to one of your character's feet bones.
-   Set **Bone/Socket 2** to the other foot bone.

![locomotion analysis properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64baae0f-ef35-488a-8eb8-6cfcb321cd0f/locomotion2.png)

Under **Vertical Axis Function**, set the following properties:

-   Set **Axis** to **Forward Speed**.
-   Set **Bone/Socket 1** to one of your character's feet bones.
-   Set **Bone/Socket 2** to the other foot bone.

![locomotion analysis properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a38b1ff-6304-45bc-8b41-a16b11e5665a/locomotion3.png)

You can now drag in your samples from the Asset Browser. Doing this will analyze and automatically position them within the blend graph. The graph will also automatically adjust its ranges and grid divisions based on the analysis.

![analyze locomotion samples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5091d5aa-366b-4864-bcc9-8da58aa5fbc1/locomotion4.gif)

You can also drag in additional samples, which will add them to the analysis array.

![additional samples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8130e435-dc2b-47f0-aed0-c09cff689e6c/locomotion5.gif)

## Managing your Analysis

When tweaking your sample positions in the graph, you can click **Analyze all Samples** in the Asset Details panel to revert all samples back to their analyzed positions.

![reset analysis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba7e6af5-1a7d-4d35-8b04-3cf676bf94a7/managing1.gif)

### Post-Analysis Cleanup

Depending on your Blend Space complexity, you may see some resulting triangulation problems, indicated by red lines in the graph.

![blend space analysis red error](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d764d0cf-603a-4b5a-a89d-0e8ef4a0548c/cleanup1.png)

These can cause blending discontinuities when interpolating the Blend Space, and need adjustment. You can perform any of the following operations to resolve this:

-   Moving existing samples, which can fix the triangulation problems, but may result in slightly inaccurate sample positions.
-   Duplicating existing samples and placing them outside the current area so the perimeter is more convex (circular) shaped.
-   Creating new samples that you can place in locations to remove the bad triangles.

#### Moving Example

In this example, two samples were placed almost on top of each other on the left of the graph, causing blending problems. The extra sample can be selected and moved to its desired position at the right side of the graph, since aiming distinguishes between +180 and -180 degrees.

![move sample to fix analysis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e5f4a7a-0b0a-4e41-8e80-4ee1ac9b5249/cleanup2.gif)

#### Duplication Example

In this example, a few perimeter samples will cause problems when using the Blend Space outside or near the edge of the region containing samples. You can move these samples to the outer edges of the graph where they will no longer generate long / thin triangles, then duplicate them by right-clicking on them and selecting **Duplicate**. This will place the duplicate at the analyzed position, while retaining the sample you just moved.

![perimeter blend space fix analysis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44f6e10d-2b8c-42f6-98f8-94e1dfdc15e7/cleanup3.gif)