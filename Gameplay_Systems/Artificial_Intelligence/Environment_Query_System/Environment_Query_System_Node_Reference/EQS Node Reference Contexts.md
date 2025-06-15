# EQS Node Reference: Contexts

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:28

---

Within the Environment Query System (EQS), **Contexts** provide a frame of reference for any [Tests](/documentation/en-us/unreal-engine/eqs-node-reference-tests-in-unreal-engine) or [Generators](/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine) used. A Context can be as simple as the **Querier** (who is performing the Test) or more complex such as **All Actors of a Type**. A Generator, such as a **Points: Grid**, can use a Context that returns multiple locations or Actors. This will create a grid (of the defined size and density) at the location of each Context. In addition to Engine supplied Contexts, you can create custom Contexts in Blueprint with the **EnvQueryContext\_BlueprintBase** class or through C++ code. 

## EnvQueryContext\_Item

**Items** are created by the Generator, and if using the **EQS Testing Pawn**, they are the spheres that appear in the Editor. An EnvQueryContext\_Item is either a location (FVector) or an Actor (AActor).

## EnvQueryContext\_Querier

The **Querier** is the Pawn that is currently possessed by an AI Controller and is executing the [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) that initiated the Environment Query. An example of where Querier as the Context could be used is if you want to search the environment around the AI character for an item they can use or find a place that provides cover from the player, or just to determine the current location of the AI performing the query.

In the **Details** panel for a Generator type, you can assign the Querier as a Context for the following properties:

| Generator | Property |
| --- | --- |
| **Actors of Class** | 
**Search Center**

![Actors of Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ce3af12-de40-4c2e-869b-cf0f9cc54393/querier-actors-of-class.png)

 |
| **Current Location** | 

**Query Context**

![Current Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d63def26-0781-4cb5-ab16-3a8a11b9b63d/querier-current-location.png)

 |
| **Points: Circle** | 

**Circle Center**

![Circle Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92726a9c-f742-475d-b484-d8e975b0ca62/querier-circle.png)

 |
| **Points: Cone** | 

**Center Actor**

![Cone Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0aa9d574-1763-43bd-a1f9-393d34c69b07/querier-cone.png)

 |
| **Points: Donut** | 

**Center**

![Donut Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb10d9f0-c3de-4cdf-bdf5-07eb9fa45189/querier-donut.png)

 |
| **Points: Grid** | 

**Generate Around**

![Grid Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd4d0b36-a7aa-42f1-bd74-2167dc5de182/querier-grid.png)

 |
| **Points: Pathing Grid** | 

**Generate Around**

![Pathing Grid Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4c12896-f2df-4b4f-b1d6-34dc564d3911/querier-pathing-grid.png)

 |

## EnvQueryContext\_BlueprintBase

You can create a custom Context through Blueprint using the **EnvQueryContext\_BlueprintBase** Class. This provides four functions that can be overridden, enabling you to add your custom Contexts for use within Tests in a query.

To use a custom Context:

1.  Create a new Blueprint of the **EnvQueryContext\_BlueprintBase** class.
    
    ![Create a new Blueprint of the EnvQueryContext BlueprintBase class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a7410ed-339f-4ce1-a41d-566d9867f7ae/blueprint-base-create.png)
2.  In EnvQueryContext\_BlueprintBase, click **Override** and select the type of function you wish to use.
    
    ![Click Override and select the type of function you wish to use](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26e77b39-10da-413d-a061-2a1ea7b2f594/blueprint-base-function.png)

Refer to the table below for a description of each function override:

| Function | Description |
| --- | --- |
| Provide Single Location | 
This returns a single location (vector). How you generate that location is up to you. For example, the function below will return the trace hit location of a random Actor (one that is found in the DesiredObjectType array, such as Pawn, Vehicle) found within 1500 cm of the Querier:



 |
| Provide Single Actor | 

This returns a single Actor. You can obtain that Actor through any method you desire. In this example, the function will return Player 0's controlled Actor:

![Provide Single Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ef21354-ad83-48a8-a03d-2af3283637b9/provide-single-actor.png)

 |
| Provide Locations Set | 

This returns an array of locations (vectors). How you generate these locations is up to you. In the example below, this function will trace from 16 evenly spaced locations on a circle with a radius of 1500 units, returning successful hits on the environment:



 |
| Provide Actors Set | 

This returns an array of Actors. You can use any desired method to obtain those Actors. In the example below, we use a Get All Actors of Class node to retrieve our specified class as the Actors to return:

![Provide Actors Set](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc79208f-dc58-4198-bf79-e11b36695de7/provide-actors-set.png)

 |