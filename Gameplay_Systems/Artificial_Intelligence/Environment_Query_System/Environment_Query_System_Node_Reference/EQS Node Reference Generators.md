# EQS Node Reference: Generators

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:29

---

Within the Environmental Query System (EQS), **Generators** are used to produce the locations or Actors (referred to as **Items**) that will be tested and weighted, with the highest weight location or Actor being returned to the [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine). There are different types of Generators that you can use to retrieve information and they can be created either in Blueprint or C++. 

## Actors of Class

![Actors Of Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40a348e3-d4dc-4434-b627-b87b8e82dd05/generators-actors-of-class.png)

The **Actors of Class** Generator finds all of the Actors of a given class within the specified **Search Radius** around the **Search Center**. The Actors returned can be used as Items in your tests. 

![The Actors of Class Generator finds all of the Actors of a given class within the specified Search Radius around the Search Center](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de605fa4-fd8e-40c1-ab80-cd05b87b563e/actors-of-class-details.png)

| Property | Description |
| --- | --- |
| **Searched Actor Class** | The Actor class to look for (for example, Pawn, Character). |
| **Generate Only Actors in Radius** | If enabled, this will only return Actors of the specified **Searched Actor Class** within the **Search Radius.** If disabled, it will return all Actors of the specified **Searched Actor Class** in the game world. You can also optionally include user-defined **Data Bindings** to go along with this option. |
| **Search Radius** | 
The max distance to look for the specified **Searched Actor Class**.  

Zero and negative values will never return any results.



 |
| **Search Center** | The context to center to search for, such as from the Querier or perhaps some other context. |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Composite

![Composite Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60614a0d-4b12-4145-8d06-ef9fc2b9ebe7/generators-composite.png)

When setting up an EQS Query, there may be instances where you want to include more than one **Generator** in a test case. With the **Composite** node, you can add multiple **Generators** to an array, which can be used in your Tests. 

![With the Composite node you can add multiple Generators to an array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef28a26e-b2b7-4d56-a1db-58ce1c17eb3a/generators-composite-details-1.png)

| Property | Description |
| --- | --- |
| **Generators** | Enables you to add multiple Generators to include in the test. |
| **Allow Different Item Types** | 
This allows tests to be performed on Generators with different Item types. 

The generator will use **ForcedItemType** for raw data and you must ensure the proper memory layout of child Generators as they write to memory blocks through their Item types. For example, data must fit into blocks allocated by **ForcedItemType** while Tests will read item location/properties through **ForcedItemType**.



 |
| **Forced Item Type** | The Item type to use in Tests. For example Actor, Direction, or Point. |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Current Location

![Current Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1664d512-da07-4ef9-8f2c-a140e3aeaac8/generators-location.png)

The **Current Location** Generator can be used to get the location of the specified **Query Context**  to validate Tests. 

![The Current Location Generator can be used to get the location of the specified Query Context for the purposes of validating Tests](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f75427b-365f-4510-a4ca-d9067ff21f94/generators-location-details.png)

| Property | Description |
| --- | --- |
| **Query Context** | The Context to use in the Test and its current location. |
| **Option Name** | 
This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Custom Generators

In addition to the Generator types provided by the Engine, you can create your custom Generators by creating a new Blueprint of the **EnvQueryGenerator\_BlueprintBase** class type.

![Custom Generators](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fff8ca2-edf7-45f7-8d46-67fc23f9a982/custom-generator.png)

Generators developed in C++ will execute generally faster than that developed through Blueprint.

Once created, your custom Generator will be available within an Environmental Query:

![Your custom Generator will be available within an Environmental Query](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b56407ed-4d92-40e8-8f55-e7a4307485fe/add-custom-generator.png)

Inside your custom Generator, there is a function you can override called **Do Item Generation**:

![There is a function you can override called Do Item Generation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3449d5c2-1214-4b51-94c1-8a32c02f9ec6/do-item-generation-1.png)

When you override this function, you'll get an array of locations that are the Context locations passed in from the Environmental Query.

![You will get an array of locations that are the Context locations passed in from the Environmental Query](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4619f07b-79f9-4b8a-8440-89469a0d6d0d/do-item-generation-2-1.png)

Depending on the Context, the array may vary. For example, this could be an array of just a single entry containing the location of the Querier, or, it could be the locations of every health pickup inside your Level.

Since functions can only return one value, the Do Item Generation function has two arrays it can pass back to the Environment Query: **Add Generated Actor** and **Add Generated Vector**.

![Add Generated Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/378ee825-cf38-48ff-a2c2-766720a68352/add-generated-actor.png)

The Add Generated Actor node will add an Actor to the Actor return array. This node can also be used with the **Add Generated Vector** node (below) to also return location values. How the Generator determines what it is passing back to the Behavior Tree is based on what Blackboard key you are setting from the Environment Query node. 

![Add Generated Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1e2c736-d8fc-479e-b578-245e7c6c1339/add-generated-vector.png)

## Points: Circle

![Circle Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d9a69c5-c6c4-4c6d-b95f-a671c5f2a624/generators-circle.png)

The **Points: Circle** Generator radiates traces out from the **Circle Center**, returning the hits on the edge of the radius (of the generated Circle) as Items. 

![Circle Generator radiates traces out from the Circle Center](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db2f3f2d-b753-4c59-89fa-2c6e08a4e571/on-circle-details.png)

| Property | Description |
| --- | --- |
| **Circle Radius** | The max radius of the circle that will expand out from the **Circle Center** context. |
| **Spawn Between** | The space (in centimeters) between the Items generated on the outer edge of the circle. |
| **Number Of Points** | The number of Items to be generated on a circle. |
| **Arc Direction** | Define the mode at which the arc direction is determined. You can choose between **Two Points** (direction from the location of one context to another) or **Rotation** (where the context's rotation will be used as a direction). |
| **Arc Angle** | Defines the angle at which the arc is measured in degrees. |
| **Circle Center** | The context used as the center for the circle. |
| **Ignore Any Context Actors when Generating Circle** | When enabled, ignore tracing into context Actors when generating the circle. |
| **Circle Center ZOffset** | Optional offset to apply to the context in the Z-axis. |
| **Trace Data** | 
Options related to how the trace is performed. 

-   **Trace Mode**: Shape used for geometry tracing.
-   **Navigation Filter**: Navigation filter used for tracing.
-   **Extent X**: Shape parameter for the trace.



 |
| **Projection Data** | If the resulting Items should be projected onto the NavMesh (and which NavMesh data set to use). |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Points: Cone

![Cone Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a91105f-c357-4fae-b177-07c92c00acc2/generators-cone.png)

The **Points: Cone** radiates a trace out from the **Center Actor** in the shape of a cone with the specified **Cone Degrees** as Items. 

![Cone radiates a trace out from the Center Actor in the shape of a cone with the specified Cone Degrees as Items](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f26f7b5-93cd-42e1-bcda-b046737223a6/cone-details.png)

| Property | Description |
| --- | --- |
| **Aligned Points Distance** | The distance between each point on the same angle. |
| **Cone Degrees** | Maximum degrees of the generated cone. |
| **Angle Step** | The step of the angle increase. Angle step must be greater than or equal to one. Smaller values generate fewer Items. |
| **Range** | Distance to generate the cone from the context. |
| **Center Actor** | The Actor (or Actors) that will generate a cone in their facing direction. |
| **Include Context Location** | 
Whether to include **Center Actor** locations when generating Items. 

This option skips the **MinAngledPointsDistance** parameter.



 |
| **Projection Data** | 

If the resulting Items should be projected onto the NavMesh (and which NavMesh data set to use). 



 |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Points: Donut

![Donut Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1295e2b5-a7bc-486e-803a-eb982fb0dade/generators-donut.png)

The **Points: Donut** Generator, creates a shape-based trace with the user specified **Number Of Rings** radiating from the **Center** Context. 

![Donut Generator, creates a shape based trace with the user specified Number Of Rings radiating from the Center Context](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca8ff7f4-2180-4057-bdf3-29d172a80cbb/donut-details.png)

| Property | Description |
| --- | --- |
| **Inner Radius** | The minimum distance between point and context. |
| **Outer Radius** | The maximum distance between point and context. |
| **Number of Rings** | The number of rings to generate. |
| **Points Per Rig** | Number of Items to generate for each ring. |
| **Arc Direction** | 
Define the mode in which the arc direction is determined. You can choose between **Two Points** (direction from the location of one context to another) or **Rotation** (where the context's rotation will be used as a direction). 



 |
| **Arc Angle** | 

Defines the angle at which the arc is measured in degrees.



 |
| **Use Spiral Pattern** | If enabled, the rings of the wheel will be rotated in a spiral pattern. If disabled, they will all be at a zero rotation, looking more like spokes on a wheel. |
| **Center** | The context to center the search on, such as from the Querier or perhaps some other context. |
| **Projection Data** | 

If the resulting Items should be projected onto the NavMesh (and which NavMesh data set to use). 



 |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Points: Grid

![Grid Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0270a42-5746-4c9f-8119-2c0ceebf0319/generators-simple-grid.png)

The **Points: Grid** Generator will generate a grid of Items around the specified querier assigned under **Generate Around**. 

![Grid Generator will generate a grid of Items around the specified querier assigned under Generate Around](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c37a110-f991-460f-91ab-c44d187e1394/simple-grid-details.png)

| Property | Description |
| --- | --- |
| **GridHalfSize** | The height and width of the grid of Items to generate. |
| **Space Between** | The distance between the grid Items. |
| **Generate Around** | The context used to generate the grid around. |
| **Projection Data** | 
If the resulting Items should be projected onto the NavMesh (and which NavMesh data set to use). 

This will move Items that may be inside walls or blocked, back onto the NavMesh, which can create bunching if a grid line happens to be just beyond the edge of the NavMesh.



 |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |

## Points: Pathing Grid

![Pathing Grid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/287fbc4e-7f62-408e-8c34-40dcd8f68440/generators-pathing-grid.png)

You can use **Points: Pathing Grid** to generate a grid around the given Context location. 

![Pathing Grid to generate a grid around the given Context location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63b383bc-eaed-47a8-a35a-97cd7a1ed4dc/pathing-grid-details.png)

| Property | Description |
| --- | --- |
| **Path to Item** | If the pathfinding direction should be towards (enabled) or away (disabled) from the Item. |
| **Navigation Filter** | Navigation filter to use in pathfinding. |
| **GridHalfSize** | Half of square's extent (edge distance). |
| **Space Between** | Defines the generation density of points on the grid. |
| **Generate Around** | The context used to generate the grid around. |
| **Projection Data** | 
If the resulting Items should be projected onto the NavMesh (and which NavMesh data set to use). 

This will move Items that may be inside walls or blocked, back onto the NavMesh, which can create bunching if a grid line happens to be just beyond the edge of the NavMesh.



 |
| **Option Name** | 

This property is inherited from the base class of the Generator ActorsOfClass. It is mostly used when displaying the Name of this Generator (for example, HUDs or output messages). 



 |
| **Auto Sort Tests** | If enabled, Tests will automatically be sorted for best performance before the query is run. |
| **Scan Range Multiplier** | Multiplier for the max distance between point and context. |