# Using the Switch Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-switch-actor-within-scene-variants](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-switch-actor-within-scene-variants)  
**Processed:** 2025-06-14 17:01:57

---

The Switch Actor provides a quick way to toggle the visibility of Actors or entire hierarchies of Actors in your Level.

Only one child of the Switch Actor can be visible at any time. When you choose a child Actor that you want to be visible, the Switch Actor automatically hides all other child Actors, along with all their descendants. It then makes the one child Actor you chose visible, along with all of the descendants of that selected child Actor.

This behavior is most convenient when you have mutually exclusive Level Actors or hierarchies of Actors, where only one of those Actors or hierarchies should ever be visible at any given time. For example, a car configurator might offer several different trims, each of which is represented by a different set of Static Mesh Actors that have different geometry, as shown below:

Click image for full size.

To switch the visible model of the car from one trim option to another would require showing and hiding multiple Actors. You could do this using Blueprint, the Variant Manager, or even manually in the Unreal Editor. However, changing visibility on dozens or potentially hundreds of different Actors at the same time can be cumbersome. If you use a Switch Actor as the parent for all the different trim options, you can easily switch between the different trims by setting a single option on the Switch Actor parent.

The Switch Actor is contained in the **Editor > Variant Manager Content** Plugin. This Plugin is typically enabled by default. However, if you don't see the Switch Actor in your **Modes** panel, you may need to enable this Plugin for your project.

## Adding the Switch Actor to a Level

The **Switch Actor** is listed in the **All Classes** tab of the **Place Actors** panel. Drag it from the **Place Actors** panel into your Level Viewport.

Click image for full size.

## Selecting the Child Actor to Show

The following sections describe the different ways you can choose which child of the Switch Actor you want to show.

### In the Unreal Editor

Select the Switch Actor in your **World Outliner**. In the **Details** panel, find the **Switch Actor > Selected Option** setting. This dropdown lists the names of all the child Actors parented by your Switch Actor.

Click image for full size.

Select the option that you want to be visible.

### In Blueprint

The Switch Actor offers a Blueprint API that you can use to work with its selected child. If you drag right from a reference to a Switch Actor in a Blueprint graph, you'll find these nodes listed under the **Switch Actor** category:

Click image for full size.

| Node | Name | Description |
| --- | --- | --- |
| ![Get Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c51648bc-6e57-446c-a511-8af27f6eb216/05-get-options.png "Get Options") | **Get Options** | Returns an array of references to all the child Actors currently parented by this Switch Actor. |
| ![Get Selected Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cffbecb-95d5-4587-bfe4-709ecf697da3/06-get-selected-option.png "Get Selected Option") | **Get Selected Option** | Returns the index of the child Actor that is currently shown. |
| ![Select Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba2b8436-c8bb-4242-8602-acd54cadd30d/07-select-option.png "Select Option") | **Select Option** | Changes the Switch Actor to select the child with the index you specify. |

The array returned by **Get Options** is not guaranteed to be in the same order as the child Actors that you see in the **World Outliner** or in the **Details** panel for the Switch Actor. In addition, the index number that is returned by **Get Selected Option** and that you specify when you call **Select Option** both identify elements within this array.

### In the Variant Manager

When you bind a Switch Actor to a Variant in the Variant Manager, capture its **Selected Option** property. The **Values** column shows a dropdown that lists the names of all the child Actors parented by your Switch Actor.

Click image for full size.

Select the option that you want to be visible when this Variant is switched on.