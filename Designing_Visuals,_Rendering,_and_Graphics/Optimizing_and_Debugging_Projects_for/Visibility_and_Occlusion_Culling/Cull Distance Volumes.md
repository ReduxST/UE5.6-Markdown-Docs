# Cull Distance Volumes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cull-distance-volumes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cull-distance-volumes-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:01

---

**Cull Distance Volumes** are a useful optimization tool that defines what distance to draw (or make visible) any Actor within the volume. These volumes store any number of size and distance combinations called **Cull Distance Pairs**. These are mapped to the bounds of an Actor (along its longest dimension) and then assigned to that Actor instance in the level. Cull Distance Volumes are most useful for optimizing large outdoor levels that have detailed interiors. The interiors can be culled when they are small enough to be considered unimportant.

## Setup and Usage

Cull Distance Volumes can be added to your level through the **Place Actors** panel in the Editor, and you can scale it to fit the level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ae20d14-06ff-4a1a-b04f-d932472a3925/addcdvtoworld.png "AddCDVToWorld.png")

With the volume selected, use the **Details** panel to access the **Cull Distance** pairs array. Each Cull Distance pair includes a value for **Size** and **Cull Distance**. Click the **plus** (**+**) sign to add a new Cull Distance pair to the bottom of the array elements list.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/952bed4f-bb29-49ec-97d3-24e9c4a957b3/addcdvpairs.png "AddCDVPairs.png")

By default, there are two **Cull Distances** pairs added; one to edit as your first entry but with no set size or distance yet, and another that will be keep objects larger than 10000 units from ever being culled because those objects have a distance of 0. By setting cull distances pair that is large, you can keep objects in the far distance, like large buildings or mountains, from being culled.

### Inserting, Deleting, and Duplicating Cull Distance Pairs

Use the dropdown next to each array element to insert, delete, or duplicate a Cull Distance pair element.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc71e9c6-45ed-4c37-98c2-ee87afc85ab2/editcdvpairs.png "EditCDVPairs.png")

-   **Insert** adds a new Cull Distance pair above the element selected.
-   **Delete** removes an existing Cull Distance pair element from the list.
-   **Duplicate** copies the selected Cull Distance pair to a new array element below.

You can have as many or as few Cull Distance array elements as you'd like and there is no requirement that they be in sequential order for them to work properly.

## Example Scene and Setup

In this example using the Infinity Blades Grasslands project, a few Cull Distance pairs have been set up to cull different sized objects from the camera's position.

The values used here are an extreme example to quickly see how the Cull Distance pairs are working with Actors in the level. Additional pair values and testing would improve the "popping" visible in the example.

The following values have been used for the demonstration that define a few Cull Distances and Sizes:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddc7389b-0b63-4a3f-a286-d6d6172369a7/examplescenecdvvalues.png "ExampleSceneCDVValues.png")

-   Objects within the volume that have a size closest to **200** units will be culled from view when they are **1000** units or more from the Camera.
-   Objects within the volume that have a size closest to **500** units will be culled from view when they are **2000** units or more from the Camera.
-   Objects within the volume that have a size closest to **1000** units will never be culled. This ensures that very large objects are treated as infinity, meaning the camera can never get far enough away to cull them.

When setting up Cull Distance pairs, keep the following in mind:

-   The Cull Distance pairs array is not linearly interpolated.
    -   This means you won't have to use dummy pairs and in the event of overlapping Cull Distance pairs, the engine will pick the most aggressive settings (or the lowest that is larger than 0) to assign to an Actor.
-   You can have as many Cull Distance Pairs as needed.
    -   For organizational purposes, it's best to keep pairs in a sequential order (like highest to lowest), but it is not required.
    -   When adding new pairs, keep in mind you can always add pairs later using the **Insert** dropdown.
-   Cull Distance pairs are assigned to Actors with bounds diameters closest to their size. Use the **Current Max Draw Distance** of an Actor to see what cached draw distance group it's being assigned to based on Cull Distance pair values.

These are some suggested pair values to help get you started:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60fd7023-6520-4d5b-9370-0452381a29a6/examplescene_suggestedpairvalues.png "ExampleScene_SuggestedPairValues.png")

## Best Practices

The following suggestions can help you achieve an effective result:

-   Use a single Cull Distance Volume to encompass the entirety of the level.
    -   Include a variety of Cull Distance pairs that represent the majority of your level.
    -   For areas within the volume, you can use additional Cull Distance Volumes to have additional, more aggressive control over culling.
-   When setting up Cull Distance pairs, start with large size and distances to get a sense of the upper and lower limit you want to use.
    -   With the Level Viewport in "Game" view, move around your level to see if there is any visible "popping" in of objects.
    -   Make alterations and possibly add some new Cull Distance pairs between existing ones. Select offending Actors and use their **Cached Cull Distance** to get an idea of which Cull Distance pair grouping some Actors are falling into.
-   Keep in mind that Cull Distance pair groups are only used if lower than the **Max Draw Distance** of the individual Actor.
    
-   If you have some Actors that should never be culled by a Cull Distance Volume, use the Actor Details panel and disable **Allow Cull Distance Volume**.
    -   Keep in mind that if you have a lot of Actors that require this to be disabled, consider having the last Cull Distance pair be your "too large for cull distance" value with a large value for **Size** and a **Cull Distance** of **0**. This prevents really large objects, such as mountains or buildings, from being culled.