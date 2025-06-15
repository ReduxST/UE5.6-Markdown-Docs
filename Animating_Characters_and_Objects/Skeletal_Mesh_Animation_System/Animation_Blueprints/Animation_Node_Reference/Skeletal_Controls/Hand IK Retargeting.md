# Hand IK Retargeting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-hand-ik-retargeting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-hand-ik-retargeting-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:27

---

With the **Hand IK Retargeting** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can retarget IK bone chains, to correct fk hand locations when using animations with characters of different proportions.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f32e90c-0848-4447-b4e4-cc983829200b/handikretargeting.png)

Here, the same animation is playing across both Masculine and Feminine characters, as the Feminine character twists, their right arm is overextending in order to keep their hands connected to the weapon.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56906d4d-bd68-4408-8e53-2f4f42cd6017/handikdisabled.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2bcbdb7-7908-4fcc-b2b5-c2e9bc74228f/handikdisabledquinn.gif) |
| Masculine Character with Hand IK Retargeting Node Disabled | Feminine Character with Hand IK Retargeting Node Disabled |

You can use the Hand IK Retargeting node's **Hand FKWeight** property to shift the prioritization weight of the set FK bone, to correct any over-extension.

|   |
| --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0175fed4-d8ea-4fed-b48d-cdcc0480540a/handikenabledquinn.gif) |
| Feminine Character with Hand IK Retargeting Node Enabled |

In the example, the characters arms are being attached to the weapon, using a combination of the [Two Bone IK](/documentation/en-us/unreal-engine/animation-blueprint-two-bone-ik-in-unreal-engine) nodes. The Hand IK Retargeting node is then being used to correct for the over extension of the character's left arm. The Hand FKWeight is set to a value of 0 to achieve this result.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a73be05-3a79-46f5-99d8-9e96ed2b48fc/graph.png)

## Property Reference

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34a595c4-5d6a-4583-b25c-3b34794f6f13/details.png)

Here you can reference a list of the Hand IK Retargeting node's properties.

| Property | Description |
| --- | --- |
| **Right Hand FK** | Select the characters right hand bone from the characters skeleton to set as the **Right Hand FK**. |
| **Left Hand FK** | Select the characters left hand bone from the characters skeleton to set as the **Left Hand FK**. |
| **Right Hand IK** | Select the right hand IK bone from the characters skeleton to set as the **Right Hand IK**. |
| **Left Hand IK** | Select the left hand IK bone from the characters skeleton to set as the **Left Hand IK**. |
| **IKBones to Move** | 
Here you can select other bones to be moved. You can add bones with **Add (+)** and select a bone from the character's skeleton in the drop down.

Additional bones to move could be weapon bones, or other bones used for object interactions.



 |
| **Hand FKWeight** | Here you can set the weight to favor the right or the left hand to correct for joint popping and stretching. For example, 0 would favor the left hand, 1 would favor the right hand and 0.5 would be equal weight. By default this property appears as a pin on the Hand IK Retargeting node in the **AnimGraph**. |