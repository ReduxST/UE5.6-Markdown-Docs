# Look At

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-head-look-at-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-head-look-at-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:28

---

With the **Loot At** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can drive a bone's rotation to follow a point of reference.

![look at skeletal control animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90169f08-88b2-420c-b1a2-718e19e8a55f/lookat.png)

You can use the Loot At node to drive motion like head rotation to follow a reference point, and even set the reference point to follow the motion of another bone of the character's skeleton.

Here, the Look At node is set to drive the character's head to follow the character's hand. Then, the **Look At Location** is offset from the hand, and shown driving the motion form the offset location.

![look at skeletal control animation blueprint node demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/127ee66a-973d-4efd-bafe-81c033f1a3b2/demo.gif)

## Property Reference

![look at skeletal control animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76af98b9-109f-4f82-b8a6-5cbafba0d481/details.png)

Here you can reference a list of the Look At node's properties.

| Property | Description |
| --- | --- |
| **Bone to Modify** | Select the bone from the character's skeleton to be driven with the **Look at Target** and **Look at Location** properties. |
| **Look at Axis** | Set the axis of the **Bone to Modify** to point towards the **Look at Target**. A value of 1 will enable the axis to be factored, a value of 0 will disable the axis to be factored. A value set of (0, 0, 0) will allow a default axis to be used. You can also enable the axis to be factored in local space by enabling the **Local Space** property. When the **Local Space** property is disabled, the axis will be factored in world space. |
| **Use Look Up Axis** | When enabled, the **Bound Bone** will be pointed towards the **Look Up Axis**. |
| **Interpolation Type** | 
Select the interpolation type when factoring the modified motion. Options include:

**Linear**: Blends along a linear trajectory. **Cubic**: Blends along a cubic trajectory. **Sinusoidal**: Blends along a sine wave trajectory. **Ease in Out Exponent 2**: Blends in and then out, along a squared trajectory. **Ease in Out Exponent 3**: Blends in and then out, along a cubed trajectory. **Ease in Out Exponent 4**: Blends in and then out, along a quartic trajectory. **Ease in Out Exponent 5**: Blends in and then out, along a quintic trajectory.



 |
| **Look Up Axis** | When **Use Look Up Axis** is enabled, set the axis to align the **Bone to Modify** with the **Look at Target**. You can also enable **In Local Space**, to factor the axis in local space. When **In Local Space** is disabled, the axis will be factored in world space. |
| **Look at Clamp** | 

Set a clamp to limit the angles the **Bound Bone** can rotate on the **X**, **Y**, and **Z** axes.

Since the axis used as the **Look at Axis** is occupied, only the other axis will be used when clamping. For example, if the **Look at Axis** is **Z**, only **X**, **Y** degree of clamp will be used.



 |
| **Interpolation Time** | Set the duration of time, in seconds, to perform the interpolation using the **Interpolation Type**. |
| **Interpolation Trigger Threshold** | Set the threshold to trigger the interpolation in seconds. |
| **Look at Target** | Set a bone from the character's skeleton to use as the target socket to look at. |
| **Look at Location** | Set a reference point in world space to angle the **Bone to Modify** towards. When a bone is set as the **Look Target**, this property's value is factored in local space and used as an offset from the selected bone. |