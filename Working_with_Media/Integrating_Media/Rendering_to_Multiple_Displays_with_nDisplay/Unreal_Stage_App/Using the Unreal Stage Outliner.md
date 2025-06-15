# Using the Unreal Stage Outliner

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-stage-outliner-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-stage-outliner-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:13

---

## The Outliner

The Outliner can optionally be displayed at any time and will list out all of the ICVFX content within the scene and show anything that is currently selected.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57a02346-a8cf-46ca-adf5-b49bea9d89fc/outliner-1.gif)

## Outliner Tools

The Outliner menu bar offers the following tools for managing ICVFX content.

### Filtering

As with the Outliner in desktop Unreal Engine, the list of content can be filtered by type to more easily find a desired actor, especially in larger and more complex scenes.

There is also a 'search by' to find content by name.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f78c8b8-4221-43b3-8169-a60774e0394f/outliner-2.gif)

### Visibility

The visibility button in Unreal Stage toggles the Actor Hidden in Game property, which will hide the selected content from view. Hidden content will no longer be visible in nDisplay on the LED volume, but it is still available for further manipulation (such as making adjustments without disrupting other work on-stage, or finding it to make it visible again) through the Editor and in-app. Hidden content will display as italicized in the Outliner to distinguish it from content that is visible.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/093c053c-ccce-4dad-8eb6-4799e3984531/outliner-3.gif)

### Multi-Select

Multi-selection mode can be toggled on and off via the Outliner. When on, selecting content will add it to the selection to create a selection set instead of changing the selection from one actor to another.

If multi-selecting content with different visibility states (ex. one visible, one hidden), Unreal Stage will treat the selection as visible. This means that tapping the visibility button will hide all selected actors on the LED Volume.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b24feba-255d-4cce-b6da-d1c8465bb20b/outliner-4.gif)

### Ellipsis Menu

-   Additional utility operations can be found in the ellipsis menu:
-   Focus Selected
-   The Editor Preview will be zoomed and panned to focus on the selected actor.
-   Duplicate Selected
-   Delete Selected
-   Rename Selected

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4809dce-4f3d-4dce-bf84-383638a329f9/outliner-5.gif)

### Swipe Operations

Actors in the Outliner can also be swiped left and right for quicker and easier access to key operations:

-   Swipe Right
-   Toggle Visibility
-   Swipe Left
-   Delete Selected

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1f3c74d-9f74-41d5-98cf-11545aedbb1e/outliner-6.gif)