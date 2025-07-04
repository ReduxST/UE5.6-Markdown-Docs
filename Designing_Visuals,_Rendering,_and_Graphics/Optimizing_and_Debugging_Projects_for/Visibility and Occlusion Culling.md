# Visibility and Occlusion Culling

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:26

---

Unreal Engine provides methods of culling for visibility and occlusion. These culling methods are useful for optimizing game performance. Each method works to reduce the number of visible Actors in the Level by setting whether they should be drawn to the screen or not. Some of these methods (such as [View Frustum](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#viewfrustum) and [Hardware Occlusion Queries](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#hardwareocclusionqueries)) can work simultaneously or are better suited to specific devices and platforms (such as [Round Robin Occlusion](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#roundrobinocclusionforvr) for virtual reality).

## How Culling Works

To get a sense of what Unreal Engine offers by default without any setup, we'll look specifically at View Frustum culling and Hardware Occlusion Queries.

The general idea of visibility and occlusion culling methods is to reduce the number of visible objects at any given time with the goal of gaining performance.

For example, if we start with only what the camera can see from its position, there are only a handful of objects visible (Scene View). However, we know that is not entirely the case because there are a lot of objects around that make up the scene that just are not visible from this position (Top Down Scene View).

Scene View

Top Down Scene View

The objects outside of the camera's field of view (the view frustum) aren't visible, and can be culled (objects outlined in red).

![Scene View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3763eb52-9920-4cdb-aa94-227288e65480/sceneviewbase.png)

![Scene View with | View Frustum Culled Objects Removed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/035f4536-c514-4abf-ac47-a7637ffde718/sceneview_viewfrustumculled.png)

Culled objects outside of the camera's view frustum are no longer rendered, leaving only a handful of objects within this view that are occluded by another object that need to be checked for visibility. So, during this pass, a query will be sent to the GPU to test each of these object's visibility state. Those that are occluded by another are culled from view (objects outlined in blue).

![Scene View with | only objects in the View Frustum](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d935140-811d-4d5c-a8d3-6b621649b0cb/sceneviewwithonlyoccludedobjects.png)

![Occluded Objects within | the View Frustum Culled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/270e1d44-45a6-40b7-997e-6556059a53fc/sceneview_occludedobjectsremoved.png)

All objects that are outside of the view frustum or that are occluded are now culled from view. The final scene view now matches the objects we know to be visible in the scene from the camera's position.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae447558-0f06-4b44-a930-73d29fa7f264/vis_finalsceneview.png "Vis_FinalSceneView.png")

Unreal Engine provides a number of culling methods, each with their own advantages and disadvantages where some are available for specific platforms.

For additional information, see [Culling Methods](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#cullingmethods) below.

### Testing Visibility with an Actor's Bounds

Each Actor placed in a Level has a set of bounds using a box and a sphere that is used for various things in the Engine. One of those being specifically to test whether an it is visible or not. The bounds of an Actor is made up of two parts: a sphere and a box. The bounding sphere is used for fast collision detection with a simple distance test, and, more often than not, it's greater in size than the object it contains. On the other hand, the bounding box is a closer match to the shape of the object and provides more accurate results.

Visualize bounds of Actors in the Level Viewport by selecting **Show > Advanced > Bounds**. Alternatively, in the Skeletal Mesh Editor you can select **Character > Bounds** and in the Static Mesh Editor, select **Bounds** in the main toolbar.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de92f6cc-01ab-4e16-9971-9611bc6f6aac/actorbounds.png "ActorBounds.png")

An Actor with its bounds (sphere and box) displayed.

Each Static Mesh and Skeletal Mesh has its own bounding box and sphere that automatically scales to the size of the geometry when imported, or when scaled or rotated in the viewport.

You can edit an Actor's bounds using the following ways:

-   By setting the **Bounds Scale** from its **Details** panel when it's selected in a Level or in a Blueprint. The **Bounds Scale** uniformly scales the bounds of an Actor, acting as a multiplier of the original scale values.
    
    Click image for full size.
    
-   By opening the Static Mesh or Skeletal Mesh Editors to apply non-uniform scaling for **Positive Bounds Extension** and **Negative Bounds Extensions** using the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58ba56f1-8514-442d-b082-385d1c8869c7/actoreditorboundsextension.png "ActorEditorBoundsExtension.png")

Increasing an Actor's bounds can potentially impact performance and shadow quality by keeping the Actor from being culled sooner than it would otherwise have been.

## Culling Methods

A culling method is used to track the visibility state of each Actor in your level. The scene's data is culled and tested against whichever method(s) are being employed by your project.

The following culling methods are applied in this order based on their cost:

-   [Distance](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#distance)
-   [View Frustum](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#viewfrustum)
-   [Precomputed Visibility](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#precomputedvisibility)
-   [Dynamic Occlusion](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#dynamicocclusion)

Unreal Engine uses View Frustum culling and Hardware Occlusion Queries (Dynamic Occlusion) by default for any project. If your project has a lot of Actors this can come at a cost to GPU performance, especially in instances where there are a lot of Actors visible within the scene view.

### Distance

Distance culling methods, like per-Actor settings and [Cull Distance Volumes](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#culldistancevolumes), render or don't render Actors based on the Actor's distance from the camera.

#### Per-Actor Instance

Each Actor in the level has its own settings for draw distance that can be set using the **Details** panel. There, you can set a minimum and maximum draw distance from the camera (in Unreal Units) for which this Actor should be rendered.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca1bfe44-bff1-46f4-9155-a2e53fdae9c4/peractordistancecullingsettings.png "PerActorDistanceCullingSettings.png")

Set the following with the Actor's draw distance settings:

-   The **Minimum Draw Distance** an Actor should be visible from the camera. It is the closest you can get to an Actor before it is no longer rendered.
-   The **Maximum Draw Distance** an Actor should be visible from the camera. It is the farthest you can get from an Actor before it is no longer rendered.
-   And you can view (but not edit) the **Current Maximum Draw Distance**. It displays the stored cull distance set by a [Cull Distance Volume](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#culldistancevolumes), if one exists.

#### Cull Distance Volumes

**Cull Distance Volumes** use an array of distances and sizes to set whether an Actor is rendered or not when within the volume. This culling method is ideal for large outdoor levels where you would have buildings or structures of some type with detailed interiors where you'd wanted to cull those objects that are too small to consider important at far distances.

For additional information, see [Cull Distance Volumes](/documentation/en-us/unreal-engine/cull-distance-volumes-in-unreal-engine).

### View Frustum

**View Frustum** culling uses the visible screen area of the camera's field of view (FOV) to cull objects not within this space. The view frustum is a pyramidal shape that includes a near and far clipping plane which defines the closest and farthest any object should be visible within this space. All other objects are removed to save processing time.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3240e7c-664c-432c-8df4-72b408f86a17/viewfrustumdiagram.png "ViewFrustumDiagram.png")

1.  The **Near Clipping Plane** is the closest point to the camera that objects will be visible.
2.  The **Camera Frustum** is the pyramidal shaped representation of the visible viewing area between the near and far clip planes.
3.  The **Far Clipping Plane** is the farthest point from the camera that objects will be visible.

Visualize the view frustum while editing in the Level Viewport by selecting   **Show > Advanced** and enable **Camera Frustum**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e5dd46f-54e1-4eb6-842f-07a2e60b7b15/viewfrustumscenecamerafrustum.png "ViewFrustumSceneCameraFrustum.png")

Camera frustum visualization enabled.

For additional information, see the [How Culling Works](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#howcullingworks) section above.

### Precomputed Visibility

**Precomputed Visibility Volumes** store the visibility state of non-movable Actors in cells placed above shadow casting surfaces. This culling method generates visibility data offline (during a lighting build) and works best for small to medium-sized levels. Precomputed visibility is ideal for lower-end hardware and mobile devices. For such hardware and devices, when considering performance costs, you'll gain the most by trading rendering thread costs that are more expensive for runtime memory ones where there is more flexibility with regards to performance.

For additional information, see [Precomputed Visibility Volumes](/documentation/en-us/unreal-engine/precomputed-visibility-volumes-in-unreal-engine).

### Dynamic Occlusion

The dynamic occlusion system comes with several culling methods to choose from. Each of these methods track the visibility states of Actors in a level within the camera's view frustum (or field of view) that are occluded by another Actor. Queries are issued to the GPU or CPU to check the visibility state of each Actor.  A heuristic is used to reduce the number of visibility checks needed, in turn, increasing overall culling effectiveness and performance.

Unreal Engine uses the scene depth buffer when issuing occlusion queries. It enables longer view distances since it relies on approximate distances rather than a maximum draw distance (or far clipping plane). Using the depth buffer enables Actors which are movable or non-movable to occlude or be occluded by another Actor, including those using materials with opaque or masked blend modes.

#### Hardware Occlusion Queries

The primary dynamic occlusion method employed is **Hardware Occlusion Queries**, which issues visibility checks to the GPU each frame as a query per-Actor. The Actor's visibility is read back one frame later—which can sometimes have the adverse effect of causing them to "pop" in if the camera is moving very fast. The cost of hardware occlusion scales with the number of queries performed on the GPU. Use Distance and Precomputed Visibility methods to reduce the number of queries performed each frame by the GPU.

Hardware occlusion queries are enabled by default and will work on any platform that supports it, including some higher-end mobile devices that support **ES 3.1** or higher on [iOS](/documentation/en-us/unreal-engine/ios-ipados-and-tvos-support-for-unreal-engine) and **Vulkan** on [Android](/documentation/en-us/unreal-engine/android-support-for-unreal-engine). Devices that do not support hardware occlusion queries can disable it from the **Project Settings** under **Rendering > Culling** by unchecking **Occlusion Culling** or by setting the following console variable in a device config file:

```
      `r.AllowOcclusionQueries=0`

Copy full snippet
```
r.AllowOcclusionQueries=0

For additional information on the cost of dynamic occlusion, see [Performance Statistics](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#performancestatistics)  below.

##### Hierarchical Z-Buffer Occlusion

**Hierarchical Z-Buffer** (HZB) occlusion works just as Hardware Occlusion Queries does, except that it is more conservative in the way that it culls objects, meaning fewer objects are culled as a result. It uses a Mip mapped version of the Scene Depth render target to check the bounds of an Actor. It requires fewer texture fetches when sampling from a lower MIP, also.

HZB Occlusion can be enabled by using the following console command:

```
      `r.HZBOcclusion=1`
Copy full snippet
```
r.HZBOcclusion=1

#### Round Robin Occlusion for VR

**Round Robin Occlusion** is one of the dynamic occlusion query methods to improve stereo rendering performance by alternating between one eye each frame instead of both. There is an added frame of latency to occlusion data which could result in incorrect rendering in the the periphery with the trade off being that Round Robin Occlusion saves an entire frame's worth of queries. The trade off in savings can help most with scenes that are draw call or visibility bound.

Enable Round Robine Occlusion in your .ini config file or at runtime using the following console variable:

```
     `vr.RoundRobinOcclusion=1`
Copy full snippet
```
vr.RoundRobinOcclusion=1

## Performance Statistics

No matter the size of your game, one of the most important development passes to do is performance optimization. Culling objects from your scene is a good way to go about doing that. The statistics window enables you to look at various stats reflective of how visibility and occlusion culling are performing.

For example, for Precomputed Visibility, you would want to keep an eye on how much memory is being used at runtime to load culled object data. For Hardware Occlusion Queries, you'd want to check how many primitives are being sent to the GPU during any given frame if you're experiencing performance issues, like hitching or sluggishness.

Call the stats window by entering **stat initviews** into the console window.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac11539c-7b29-4d90-8e3a-2148b15f9bcc/statinitviews.png "StatInitViews.png")

The stats displayed are broken up into two sections: **Cycle Counters** and **Counters**. The Cycle Counter stats focus on the number of rendering cycles in milliseconds (ms) that it took to process primitives. There you'll focus on the **View Visibility**, **Occlusion Cull**, **View Relevance**, and **Frustum Cull**. The Counter stats add all the primitives that have been processed in the current view.

Keep the following in mind when testing visibility and occlusion culling:

-   Occlusion culling is disabled in **Wireframe** view mode.
-   Use the hotkey **G** to switch to gamemode view while working in the viewport to see some culling methods, like Cull Distance Volumes or Precomputed Visibility Volumes.
-   For the most accurate results, use Stat InitViews statistics when in **Play-In-Editor** (PIE) or **Standalone Game**. Geometry for the Actors that represent Lights, Cameras, and others will be included when calculating visibility and occlusion culling results.
-   Keep an eye on **Visible Static Mesh Elements** because it is the single biggest contributor to rendering thread time and should be carefully watched and optimized.

| Stat Name | Description |
| --- | --- |
| Cycle Counters |   |
| **View Visibility** | The amount of frame time spent to process Actor visibility queries. |
| **Occlusion Cull** | The amount of frame time spent to query the scene for Actors within the view frustum that were occluded by other Actors. |
| **Frustum Cull** | The amount of frame time spent to query if an Actor's bounds were within the view frustum. |
| **Decompress Occlusion** | The amount of frame time it took to load the precomputed visibility. |
| Counters |   |
| **Processed Primitives** | The total number of Actors that are being processed in the scene. |
| **Frustum Culled Primitives** | The number of primitives culled when not within the view frustum FOV. |
| **Occluded Primitives** | The number of Actors that are occluded by other Actors from within the view frustum FOV. |
| **Occlusion Queries** | The number of scene occlusion queries sent to the GPU based on the number of Actors visible within the view frustum. |
| **Visible Dynamic Primitives** | The number of dynamic primitives in the scene that have their mobility set to Movable, like Particle Systems and Foliage instances. |
| **Visible Static Mesh Primitives** | The number of visible meshes that have their mobility set to Static within the scene. |

## Debugging Culling

Below are debugging options you can use for visibility and occlusion culling.

### Visualizing Occluded Actors

You can use a visualization command while working in the Editor to check if an Actor is occluded.

```
     `r.VisualizeOccludedPrimitives 1`

Copy full snippet
```
r.VisualizeOccludedPrimitives 1

When enabled, a green bounding box is drawn around any occluded Actor.

If you have a lot of Actors in your Level, this visualization may not be a useful debugging method without hiding some parts of your Level and their contained Actors.

![Visualized Occluded Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca7a33c6-bf70-4251-96a7-6a4dfc1870c9/visoccludedactors1.png)

![Hidden Geometry to | show occluded Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50269d6b-ce10-4155-bb8e-00a1b384fcf9/visoccludedactors2.png)

In this example, note that only Actors fully occluded by the walls and doors are occluded. The ones on the right visible through the hole in the wall are not fully occluded.

### Freezing Rendering of the Scene

You can "freeze" the rendering state for Actors in your Level while working in the Editor so that you can freely move around within the Level viewport and inspect occlusion results.

Enter the command `FreezeRendering` from the view you want, like the example below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df4ccbd5-efff-4976-aeca-a4c654a806b8/freezerendering.png "FreezeRendering.png")

Once entered, freely move around the scene to see the occlusion result. When moving the view to be behind the wall, objects fully occluded are not rendered and the Actors that were not fully occluded still are.

![Normal Scene View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/945afd8e-b9a2-4b5a-8942-6872e197e5ad/freezerenderingstate2.png)

![Freeze Rendering from | original camera view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bf45cd2-b635-49f6-bf39-1b933c8c7998/freezerenderingstate1.png)

Use the following commands to freeze rendering states for other types of Actors:

| Console Command | Description |
| --- | --- |
| **FreezeRendering** | Pauses / Unpauses the current rendering state of occluded and visible Actors in the Level based on the camera view. |
| **Foliage.Freeze** | Pauses the current rendering state of occluded and visible painted foliage clusters in Level based on the camera view. |
| **Foliage.Unfreeze** | Unpauses the rendering state of occluded and visible painted foliage clusters in the Level. |
| **FX.FreezeParticleSimulation** | Pauses / Unpauses any CPU sprite particle simulations in the Level. |
| **FX.FreezeGPUSimulation** | Pauses / Unpauses any GPU sprite particle simulations in the Level. |

### Using Game View Mode

You can use **Game View** mode to get a sense of what the game will look like while you are working in the Editor. Using this view mode gives you the visual of your game during any play mode, like Play-in-Editor (PIE) mode or Standalone Game, while still enabling you to move around the world and edit objects freely.

Enable Game View using the keyboard shortcut **G** or use the viewport dropdown menu and select **Game View** while working in the Editor.

![Editor View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bce56cc-9de4-416f-bb70-d159830eea75/gameview1.png)

![Game View ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/798bd856-c9d9-41d0-8f47-4bd1b80c2de0/gameview2.png)

When **Game View** is enabled, Actor icons are hidden (like they would be in-game), such as those for Lights and Particle Systems. If you're using [Cull Distance Volumes](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#culldistancevolumes) or [Precomputed Visibility Volumes](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine#precomputedvisibility) (and are in the cell), you'll immediately see the culling results of those volumes depending on their culling aggressiveness.