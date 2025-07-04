# Navigation Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:04

---

Navigation Components are a type of component that modifies or extends the functionality of the **NavMesh** (Pathfinding) system in Unreal Engine.

## Nav Modifier Component

The **Nav Modifier Component** does nothing by itself, however, if you have a basic shape component as the root of an Actor, the volume of that Root Component will modify the NavMesh generation within it according to the Nav Modifier Component's **Area Class** property. You should only have one Nav Modifier Component per Actor as multiples of this Component have no effect. Also, these will appear outside the hierarchy in the Components Tab, and cannot be parented to another component or have anything parented to them.

These Area Classes can define basic things like **Cost** to enter an area or more advanced things such as areas where a crouched character should be able to navigate.

Cost is an important idea for the NavMesh system. Briefly, the total cost to move from one point to another using NavMesh is the sum of all the area costs the path moves through (a single area's size is defined in the Project's Preferences). But, the solver will always try to find the cheapest path, so you can have it avoid areas (like slippery oil or rough terrain) by increasing the cost to pass through that area. Just remember the solver will still path through high cost areas if it is the cheapest path.

For example, the red area has a very high cost to move through, but the Pawn has no other choice but to move through it.:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a69e8ac2-33d0-45e4-9b28-f74c921060cb/aroundthered.jpg)

But, if you remove a wall:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c186df4-b113-4683-a5de-2c89b00e0f16/throughthered.jpg)

Then the pawn will avoid the red area even though it means taking a much longer route.