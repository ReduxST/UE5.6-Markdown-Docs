# Trail Controller

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-trail-controller-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-trail-controller-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:45

---

Using the **Trail Controller** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can define a chain of bones to animate based on a delayed replication parent bone motion.

![trail controller skeletal control animaiton blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d796319-4f7f-49fc-892e-2d029fd975cd/trailcontroller.png)

You can use the Trail Controller node to create more realistic trailing motion on your character's auxiliary boned objects, such as tails, capes or accessories.

![trail controller skeletal control animaiton blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8c592bf-e101-47f9-9771-097bd4684336/taildemo.gif)

By defining a bone as the **Trail Bone**, you can select how many bones up the chain from the **Trail Bone** that will be influenced by the Trail Controller node. You can then set constraints on **Stretch**, **Rotation** and even **Planer Limits** on transforms.

## Property Reference

![trail controller skeletal control animaiton blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3d0cfd1-24af-400f-b3ba-7a2df62bb9d1/details.png)

Here you can reference a list of the Trail Controller node's Trail properties.

| Property | Description |
| --- | --- |
| **Trail Bone** | Set the bone at the end of a chain structure to trail the parent bone motion. |
| **Chain Length** | Set the number of bones to influence up the chain from the Trail Bone. |
| **Chain Bone Axis** | Set the axis (**X**, **Y**, or **Z**) to orient the chain points to one another. |
| **Invert Chain Bone Axis** | Set a scale alpha to apply the **Relation Speed Scale Input Processor** properties. A value of 0 will disable the effect, while a value of 1 will fully enable the effect. Values greater than 1 will act as a multiplier. |
| **Trail Relaxation Speed** | 
Here you can use the **Trail relaxation speed graph** to set a curve to define the behavior at which the transform returns to the animated pose.

![trail controller trail relaxation speed scale graph details property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da39c88b-9472-4378-9fe6-fe8af85ccfc7/graph.png)

Using the graph editor in the property's settings, you can edit the beginning and ending point of the graph to control how the behavior of the chains return to the animated pose. Or right click the graph to add a new point on the graph to manipulate the curves position.

The graph's X-axis is ranged from 0 to 1, and it is mapped to the chain of joints. 0 represents the last joint in the chain and 1 represents the closest joint to the **Trail Bone**.

The graph's Y-axis controls the rate at which the delayed motion is passed to the next joint in the chain. Values less than or equal to 0 will prevent joints from continuing to pass the delayed motion. Higher values will pass the delayed motion on quickier. The Y-axis operates as an absolute value to prevent frame dependency. The default range is from 5 to 10 resulting in a faster return from the root joint to the bottom joint.



 |

### Limit Properties

![trail controller skeletal control animaiton blueprint node details panel limit properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd4c960d-6b15-4af1-8803-39aeaaaf5e35/otherprops.png)

Here you can reference a list of the Trail Controller node's Limit, Velocity and Rotation properties

| Property | Description |
| --- | --- |
| **Limit Stretch** | Enable a constraint on the structures stretching. This constraint can be set in the **Stretch Limits** property. |
| **Limit Rotation** | Enable rotation constraints and offsets on each chain point. Rotation constraints can be set on each chain point using the **Indexes** within the **Rotation Limits** property. |
| **Use Planer limit** | Enable planer constraints to eliminate motion past set planes. These planes can be added and set in within the **Planer Limits** property. |
| **Max Delta Time** | To avoid hitches caused by stretching the chain, you can use this property to clamp the length of the delta time. For example, if you want a 30 fps trail animation playback, set this property to 0.03333f (or 1/30). |
| **Rotation Limits** | 
Set the rotation limits at each joint along the chain points. The highest **Index** number represents the **Trail Bone** and **Index 0** represents the furthest bone from the **Trail Bone** in the chain.

**Limit Min**: Set the minimum range of rotation on the **X**, **Y** and **Z** axis. **Limit Max**: Set the maximum range of rotation on the **X**, **Y** and **Z** axis.



 |
| **Rotation Offsets** | Set a rotational offset, in degrees, for each joint's **X**, **Y**, and **Z** axes, along the chain. The highest **Index** number represents the **Trail Bone** and **Index 0** represents the furthest bone from the **Trail Bone** in the chain. |
| **Planer Limits** | 

Add and set planer limits to constrain the chain's motion from crossing a plane. After adding a planer limit with **Add (+)**, you can adjust the following properties to set up a plane limit:

**Driving Bone**: Select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) that will become the reference point to set the **Plane Transform** properties. **Plane Transform**: Set the planer properties, **Location**, **Rotation**, and **Scale**, to limit the chain's motion, in context to the **Driving Bone**.



 |
| **Stretch Limits** | Select how far the chain structure can stretch from the reference pose. A value of 0 will disable stretching, while values greater than 0 will increase the amount of stretching that is possible. |
| **Actor Space Fake Vel** | When enabled, simulated velocity will be applied in actor-space. When disabled, simulated velocity will be applied in world-space. |
| **Fake Velocity** | Here you can set the the simulated velocity vector that will be applied to the **Base Joint**. |
| **Base Joint** | Here you can select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to serve as the base joint that can receive a simulated velocity vector to apply motion to the chain. |
| **Reorient Parent to Child** | When enabled, child bones are free to rotate to preserve the structure integrity. |
| **Last Bone Rotation Anim Alpha Blend** | This property controls the blend between the parent joint of the structure and animated pose. With a value of 0, the last joint will copy the previous joints alpha. A value of 1 will use the animated pose. |

### Debug Properties

![trail controller skeletal control animaiton blueprint node details panel debug properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/909f9627-1181-45c9-9ef2-c9844a98e33b/debug.png)

Here you can reference a list of the Trail Controller nodes Debug properties.

| Property | Description |
| --- | --- |
| **Enable Debug** | Enables debug drawing in the preview viewport. |
| **Show Base Motion** | Draws red lines that follow the basic transform path, (**X**, **Y** and **Z** axes) of the structure. A dot will be drawn on the line to indicate the location of the joint before the application of any motion. |
| **Show Trail Location** | Draws color coded sections of lines, to delineate different segments of the chain, between each joint in the chain. |
| **Show Limit** | Draws any planer limits. |
| **Debug Life Time** | This value determines the duration of time any debug feature remains drawn in the viewport, in seconds. |