# Vehicle Center of Mass

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vehicle-center-of-mass-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/vehicle-center-of-mass-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:45

---

Weight distribution of a vehicle is important to its control, as it affects a variety of its characteristics, like handling, acceleration, and traction. Different vehicle types will require different weight distributions depending on their intended use. For the purposes of game development, these characteristics can also define what style of game you are making, whether that is an arcade-style racer, a simulation, or even a hybrid of the two. Altering **Center of Mass** enables you to change the weight distribution of your vehicle.

In games, the primary use of Center of Mass is for vehicles, but it can also be used for large Physics Bodies encapsulating an irregular shape. In your [Physics Asset](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine), you will often use one large Physics Body to define the majority of the Mass for the vehicle (or large object). The Center of Mass will be generated at the center of this Physics Body, which can make the vehicle handle oddly, so you can adjust the Center of Mass to account for where the mass of the vehicle is really located.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62a0c003-df6b-45e6-9fd4-e07fbd607818/centerofmass.png)

## Understeering versus Oversteering

Depending on where the Center of Mass is located, you can shift it to be predominantly front-heavy, causing the vehicle to have a tendency toward **understeering** (not turning enough when going around corners), or to be predominantly rear-heavy, causing it to tend toward **oversteering** (turning more sharply than intended). In most cases, it is ideal to find a neutral balance for your Center of Mass so that the vehicle is more easily controlled.

![Understeering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1beb7e76-efdb-45cc-a837-4796d99ac4bc/understeering.png)

![Oversteering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3342ba20-4aad-48bd-b20a-dbc9e229187f/oversteering.png)

Also, when you consider where to place the Center of Mass, it is worth noting that this choice can have an effect on how your vehicle handles in the air. In this example, the Center of Mass has been lowered and moved closer to the rear of the car. Since it's low to the ground and can get to high speed quickly, the lower rear Center of Mass helps to stabilize the car, especially with jumps!

|   |   |
| --- | --- |
| 
 | 

 |
| Center of Mass: X: 0, Y: 0, Z: 0 | Center of Mass: X: -25, Y: 0, Z: -10 |

## Debugging Center of Mass

To help you debug mass properties and inertia tensors associated with physics objects while in the Level Editor, you can enable the `Show` flag by going to **Show** > **Advanced** > **Mass Properties**.

![Center of Mass: X: 0, Y: 0, Z: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f4e4022-c9d1-4b1c-b360-9d550322481b/vehiclecom1.png)

![Center of Mass: X: -25, Y: 0, Z: -10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0fbef74-05f5-4150-8051-28e5f44e8a21/vehiclecom2.png)

The thickness of each axis indicates the moment of inertia magnitude along that axis.