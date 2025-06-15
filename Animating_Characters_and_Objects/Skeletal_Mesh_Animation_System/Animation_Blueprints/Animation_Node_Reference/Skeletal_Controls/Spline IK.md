# Spline IK

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-spine-ik-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-spine-ik-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:42

---

With the **Spline IK** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can define a chain of bones within a character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), as a spline.

![spline ik animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ead1814-5fc7-4f35-9a5b-7977f88f9816/splineik.png)

After selecting the chain of bones as a spline the Spline IK node will create **Control Points** along the spline based on the parameters you set in the nodes **Details** panel.

![spline ik animation blueprint node demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7de8f49c-8e6f-49bb-a37c-5d0dc9aea167/demo.gif)

You can manually manipulate these **Control Points** to set locations for the spline to react to during animation playback. You can also drive these control points with dynamic values with internal functions or as pins in the **AnimGraph**. In addition, you can drive several Spline IK node properties, such as **twist**, **roll**, and **stretch**, using dynamic values in the same manner.

You can use the Spline IK node to create more realisting motion for tails or other malleable character structures that can be influenced by dynamic variables like velocity and movement direction.

![spline ik animation blueprint node tail dino demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db1be286-1cc6-4c28-b70c-17aa6ee9b7f3/dinodemo.gif)

## Property Reference

![spline ik animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7dcc12fe-da22-4d9b-8056-b326e3128b07/details.png)

Here you can reference a list of the Spline IK node's properties.

| Property | Description |
| --- | --- |
| **Start Bone** | Select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to begin the chain of bones that will comprise the spline. |
| **End Bone** | Select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to end the chain of bones that will comprise the spline. |
| **Bone Axis** | Select the Axis of motion (**X**, **Y**, or **Z**) the control points along the spline will move along. |
| **Auto Calculate Spline** | Enable this property to automatically calculate the number of **Control Points** based on the number of bones between the **Start Bone** and the **End Bone**. |
| **Point Count** | When **Auto Calculate Spline** is disabled you can specify how many **Control Points** will be added along the spline between the **Start Bone** and the **End Bone**. |
| **Control Points** | Here you can apply transforms to each of the **Control Points** along the spline. By default, these transforms can be applied manually in the viewport or with the transform properties under each array element for each control point. These properties can also be adjusted dynamically by exposing the **Control Points** as pins in the **AnimGraph**, or by using internal functions. |
| **Roll** | Set a degree of rotation of the **Control Points** between the **Start Bone** and the **End Bone** applied on top of the other motion along the direction of the spline. A value of 0 will disable an additional roll, positive values will roll the middle **Control Points** positively along the **Bone Axis** and negative values will roll the middle **Control Points** negatively along the **Bone Axis**. |
| **Twist Start** | Set a degree of twist the first **Control Point** (**Control Point 0**) applied on top of the other motion along the direction of the spline. A value of 0 will disable twist, positive values will twist the start **Control Point** positively along the **Bone Axis** and negative values will twist the start **Control Point** negatively along the **Bone Axis**. |
| **Twist End** | Set a value of the twist on the last **Control Point** (highest numerical **Control Point X**) applied on top of the other motion along the direction of the spline. A value of 0 will disable twist, positive values will twist the end **Control Point** positively along the **Bone Axis** and negative values will twist the end **Control Point** negatively along the **Bone Axis**. |
| **Twist Blend** | 
Select the properties of twist applied to the **Twist Start** and **Twist End**.

-   **Blend Time**: Set the time, in seconds, to blend between twist poses.
-   **Blend Option**: Select the type of blending used to blend between twist poses.
-   **Custom Curve**: Here you can set a curve to drive the blending between twist poses.



 |
| **Stretch** | Set the maximum stretch allowed when fitting bones to the spline. A value of 0.0 will disable stretch of the structure along the length of the spine. A value of 1.0 will enable the structure to fully stretch to the length of the spline. |
| **Offset** | Set the distance offset along the spline from the **Start Bone** from which bones are constrained. A value of 0 will not offset the structure, higher values will offset the structure twords the **End Bone**. |