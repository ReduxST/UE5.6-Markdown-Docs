# Two Bone IK

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-two-bone-ik-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-two-bone-ik-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:49

---

With the **Two Bone IK** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can control two-bone chains, such as a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine), character's limbs, to make contact with the **Effector Location** or an end point, using the **Joint Target Location** reference point to control the bone chain's middle point.

![two bone ik animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad93b5dd-b07c-42fa-85ea-6c2893ff4b24/twoboneik.png)

With the Two Bone IK node's **Effector Location**, you can drive the position of the bone at the end of the two-bone chain. This property can be set in the **AnimGraph** to follow the location of a socket on an interactable object, or make a grounded contact point with a point in the level.

![effector location demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10582da7-3904-41d6-982a-9468c683e983/effectorlocationdemo.gif)

With the Two Bone IK node's **Joint Target Location**, you can set the location of the bone chain's middle joint, to control the rotation behavior of the bone chain.

![joint target location demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9cf495b-dd43-4dbf-a84f-a45208f136c7/jointtargetlocationdemo.gif)

You can also set other properties such as **Stretching** and **Twisting** to control the behavior of the two-bone chain.

## Property Reference

![two bone ik aniamtion blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0349f9f5-afe3-4c1f-a1d3-2cac76b36d15/details.png)

Here you can reference the Two Bone IK node's properties.

| Property | Description |
| --- | --- |
| **Enable Debug Draw** | When enabled, debug tools will be drawn in the preview viewport. The **Effector Location** will be represented with a red object, and the **Joint Target Location** will be drawn as a green object. Lines will also be draw from each bone position, including the chain's root bone, to the **Joint Target Location** to show their position. |
| **IK Bone** | Set a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) as the bone to control.From this bone, the node will consider two bones up the chain, to build the two-bone chain. The first parent bone will act as the joint, and the second parent bone will become the root for the chain. |
| **Start Stretch Ratio** | When the **Allow Stretching** property is enabled, you can set the threshold to control when the two-bone chain is able to begin stretching. This value determines when to start stretching. For example, 0.9 means once it reaches 90% of the whole length of the limb, it will start to apply a stretch to the structure. |
| **Max Stretch Scale** | When the **Allow Stretching** property is enabled, you can set the limit to control the maximus scale of the stretch allowed for the structure. This value determines what is the max stretch scale. For example, 1.5 means it will stretch until 150% of the whole length of the limb. |
| **Twist Axis** | When the **Allow Twist** property is disabled, you can specify which axis (**X**, **Y**, and **Z**) the bone is aligned to. This property is most helpful when isolating twists for a structure. When the **Allow Twist** property is disabled, You can also enable the twist to be calculated in local-space. |
| **Allow Stretching** | When enabled, stretching of the set two-bone chain will be allowed. You can set the limits of the stretching in the **Start Stretch Ratio** and the **Max Stretch Scale** properties. |
| **Maintain Effector Rel Rot** | Keep local rotation of the end bone. |
| **Allow Twist** | When enabled, the bone chain will perform under normal structure constraints. When disabled, you can manually set the axes of twist that the structure will be allowed to twist on, in the **Twist Axis** property. |
| **Effect Location Space** | 
Here you can set the frame of reference to calculate the position of the **Effector Location**. You can set the reference frame from the following options:

**World Space**: The Effector Location's absolute position will be calculated using world space. **Component Space**: The Effector Location's set position will be calculated in the Skeletal Mesh component's reference frame. **Parent Bone Space**: The Effector Location's set position will be calculated in the parent bone space of the bone set as the **Effector Target**. **Bone Space**: The Effector Location's set position will be calculated in the reference frame of the bone set as the **Effector Target**.



 |
| **Take Rotation from Effector Space** | When the **Effector Location Space** property is set to **Parent Bone Space** or **Bone Space** you can enable this property to take the rotation of the effector location and apply it to the **IKBone**. When disabled, rotation will be ignored. |
| **Effector Target** | When the **Effector Location Space** property is set to **Parent Bone Space** or **Bone Space** you can select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to use as the Effector Location. |
| **Effector Location** | By default this property appears as a pin on the Two Bone IK node in the **AnimGraph**. The Effector Location drives the two-bone chain end point's location. When the **Enabled Debug Draw** property is enabled this property will appear as a red object in the preview viewport. |
| **Joint Target Location Space** | 

Here you can set the frame of reference to calculate the position of the **Joint Target Location**. You can set the reference frame from the following options:

**World Space**: The Joint Target Location's absolute position will be calculated using world-space. **Component Space**: The Joint Target Location's position will be calculated using the Skeletal Mesh Component's reference frame. **Parent Bone Space**: The Joint Target Location's position will be calculated using the parent bone space of the bone set as the **Joint Target**. **Bone Space**: The Joint Target Location's position will be calculated in the reference frame of the bone set as the **Joint Target**.



 |
| **Joint Target** | When the **Joint Target Location** Space property is set to **Parent Bone Space** or **Bone Space**, you can select a bone from the characters [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to use as a reference space to calculate the set position of the **Joint Target Location**. |
| **Joint Target Location** | By default this property appears as a pin on the Two Bone IK node in the **AnimGraph**. With the Joint Target Location you can control the motion and behavior of the two-bone chain's middle joint. The Joint Target acts as a reference point to bend the joint. When the **Enabled Debug Draw** property is enabled this property will appear as a green object in the preview viewport. |