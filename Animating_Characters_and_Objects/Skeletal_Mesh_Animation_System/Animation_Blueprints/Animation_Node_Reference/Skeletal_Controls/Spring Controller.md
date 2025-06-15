# Spring Controller

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-spring-controller-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-spring-controller-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:43

---

With the **Spring Controller** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can apply a controlled stretch to bone from a character's skeleton.

![spring controller animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bbec2cf-db23-4f25-9d2a-b8157e4786b1/springcontroller.png)

Here is an example of the Spring Controller node being used to simulate movement of non-animated bones by applying a force in the opposite direction for the character's motion.

|   |   |
| --- | --- |
| ![spring cotroller demo disabled](BPDemoOff.gif)(convert:false) | ![spring controller demo enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2bc3954-7a51-451a-b594-4dea2a97d6b6/bpdemo.gif) |
| Spring Controller Disabled | Spring Controller Enabled |

## Property Reference

![spring controller animation blueprint node details pannel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97e97454-1422-4145-a678-e51755319b23/details.png)

Here you can reference a list of the Spring Controller node's properties.

| Property | Description |
| --- | --- |
| **Spring Bone** | Select the bone from the character's skeleton to apply the Spring Controller node to. |
| **Max Displacement** | Set the maximum distance the bone can stretch from the reference pose location, in Unreal Engine units, when **Limit Displacement** is enabled. |
| **Spring Stiffness** | Set a multiplier value used to calculate the stiffness of the spring. Larger values require more bone velocity to displace the bone and result in a larger applied force with quicker reactive movements. |
| **Spring Damping** | Set a multiplier to reduce the **Spring Bones**'s velocity, to create smoother and more controlled results. |
| **Error Reset Thresh** | Set a threshold to reset the Spring Bones in Unreal Engine units. If the **Spring Bone** stretches more than this amount, it resets in order to avoid errors introduced by sudden, large displacements such as those caused by teleporting Actors. |
| **Limit Displacement** | When enabled the **Max Displacement** property will be considered. |