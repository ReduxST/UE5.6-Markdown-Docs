# How To Perform AR Hit Testing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-perform-ar-hit-testing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-perform-ar-hit-testing-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:13

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78368ca8-c8cc-49ab-ad85-b2f9c9cb5457/ar_hittesting.png)

For this guide, we are using the **Handheld AR** template.

In the following How To, we will take a look at how the example project created by the **Handheld AR** template demonstrates standard hit testing and tracked object hit testing. Hit testing (line tracing) is not new to Unreal Engine, or Blueprints. However, it's important to recognize that hit testing in the Unreal world, and augmented reality require different approaches. The example project contains a standard pattern for hit testing in the Unreal world, and in augmented reality on handheld devices. 

Other AR devices, such as AR headsets, will require a different approach than discussed in the below How To.

## Steps

### Create a New Handheld AR Project

1.  Open the Project Browser and create a new **Handheld AR** Blueprint project, or open an existing augmented reality project.  
    If you need assistance creating a new augmented reality project, see the [Handheld AR Template Quickstart](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine) documentation.
2.  Open the **BP\_ARPawn** Blueprint class.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e96af19c-b379-46cb-9de4-7410c24d8e39/ar_blueprintarpawnclass.png)
3.  Select the **Event Graph** tab.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4011563b-0cb7-44ed-90ce-7df9b6cce5c3/ar_blueprintarpawneventgraph.png)

### Hit Testing Against Tracked Geometry vs World Objects

The example project demonstrates the use of **Line Trace For Objects** and **Line Trace Tracked Objects** in the context of a normal workflow. **Line Trace For Objects** is being used to check for a hit against Unreal World objects, while **Line Trace Tracked Objects** is being used to check for a hit against tracked objects (augmented reality tracked geometry). Line tracing is not new to Unreal Engine, but the new **Line Trace Tracked Objects** function allows the detection of the additional tracked geometry in the world.

As the below example shows, we check for world objects first. We do this because spawned world objects are often rendered closer to the origin of the line trace, so the user will see them before the tracked geometry. If we tested tracked geometry first, we'd miss the thing we were trying to touch every time.

  

Click for full image.

  

-   **Test If User Touched World Object**  
    This is the standard use of the **Line Trace For Objects** function (in **World Hit Test**), checking against an array of potential Unreal world objects, and returning "true" or "false". In this case, if the return value is "true", **AR Hit Result** is called, updating one of **Debug Menu** items. If the return value is "false", then the execution path moves along to new augmented reality function **Line Trace Tracked Objects**. 
    
    Click for full image.
    
    Click for full image.
    
-   **Test If User Touched Tracked Geometry, Spawn Object**  
    **Line Trace Tracked Objects** is a new augmented reality function for line trace testing against tracked objects (geometry perceived by the augmented reality tracking system). **Line Trace Tracked Objects** returns a list of results sorted by distance from camera. In this case, if the return value is *greater than 0* (we hit a tracked object), then **AR Hit Result** is called, updating one of the **Debug Menu** items, and **Spawn Actor BP Placeable** is called, creating a pawn at the *tracked* location that was hit. If the return value contains no hit results (we did not hit a tracked object), **AR Hit Result** is called, updating one of the **Debug Menu** items. 
    
    Click for full image.
    

Although many of this project's actions end up updating the app's **Debug Menu**, that is specific to this particular project. You can, of course, use the hit data from a line trace in any manner that's required. The difference here is that **Line Trace Tracked Object** provides the ability to detect and react to the augmented reality tracked geometry.

### Explore Other AR Functions

Exploring a project based on the **Handheld AR** Blueprint template provides an opportunity to examine the actual use of the various augmented reality functions in context. There are dozens of new augmented reality functions, so take some time to dig into the project and explore the implementation details. 

A good place to start exploring the project and the new augmented reality functions is to open the **Content Browser**, navigate to **Content\\HandheldARBP\\Blueprints\\UI** and open the **BP\_DebugMenu** asset in the **Blueprint Editor**.