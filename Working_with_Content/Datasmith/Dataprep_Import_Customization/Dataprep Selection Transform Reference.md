# Dataprep Selection Transform Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-selection-transform-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-selection-transform-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:47

---

This page describes each of the **Transform** blocks that you can use in the Visual Dataprep system to change the objects selected for an Action.

Each type of **Transform** block encapsulates a specific type of modification that the Unreal Editor can make to the selection of Assets and Actors passed to it. The block then passes the modified selection on to the next block below it within the same Dataprep Action.

Transform blocks are like filters, in that they determine the set of Actors and Assets that other Dataprep blocks in the same Action will operate on. However, a filter block can only cut down the list of objects passed down to it. A **Transform** block, on the other hand, can *add* objects to the current selection.

## Common Controls

All **Transform** blocks offer the **Output Can Include Input** setting.

-   When this setting is enabled, the **Transform** block always adds the Actors and Assets passed in to the block to the output selection that it passes on to the next block in the Dataprep Action.
    
-   When this setting is disabled, the **Transform** block *only* adds the Actors and Assets passed in to the block to the output selection *if* those Actors and Assets also pass the other selection criteria built in to the block.
    

## Reference Selection Transform

This operation checks each Actor and Asset in the input list looking for references to other Assets in the temporary world. It then adds each referenced Static Mesh, Material, and Texture Asset that it finds to the output selection that it passes on to the next block.

![Reference Selection Transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/125d117e-a3dc-45d6-a0f6-9e4733ffcf8b/reference-selection-transform.png "Reference Selection Transform")

## Select Hierarchy

For each Actor passed in to this block, this transform looks for other Actors that are children of that input Actor. It then adds all of those child Actors to the output selection that it passes on to the next block.

![Select Hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbbfe045-a985-4b25-953e-b32900f5b23c/select-hierarchy.png "Select Hierarchy")

| Setting | Description |
| --- | --- |
| **Select** | 
Determines how deeply the selection extends into the descendants of each input Actor.

-   Use **Immediate Children** to have the output selection contain only Actors that are direct children of the Actors passed in to the transform block.
-   Use **All Descendants** to have the output selection recurse to include the complete hierarchies under the Actors passed in to the transform block.



 |

## Select Actor Components

For each Actor passed into this block, this transform looks for all Components of previously selected Actors. It then adds those Components to the output selection that it passes on to the next block.

![Select Actor Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5e16709-46e7-4c4f-a254-72b4cb11e35a/select-actor-components.png "Select Actor Components")

## Select Owning Actor

This transform looks for the parent Actor of each Component passed in to this block. It then adds the parent Actor to the output selection that it passes on to the next block.

![Select Owning Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87d95764-8225-4bdd-b0a7-5778d3c38ac7/select-owning-actor.png "Select Owning Actor")