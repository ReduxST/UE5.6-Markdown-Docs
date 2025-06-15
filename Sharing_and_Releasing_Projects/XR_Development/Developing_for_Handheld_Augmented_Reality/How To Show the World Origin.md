# How To Show the World Origin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-show-the-world-origin-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-show-the-world-origin-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:21

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dba58806-80f1-4241-8dd9-f0e79631c8b5/ar_worldorigingraphic.png)

For this guide, we are using the **Handheld AR** template.

In the following How To, we will take a look at how the example project created by the **Handheld AR** template demonstrates drawing the world origin. Knowing where the augmented reality system (ARKit/ARCore) has placed the world origin, can be useful information when troubleshooting. Devices often decide what they consider World Location 0,0,0 (World Origin) based on unpredictable factors, potentially making it difficult to debug issues with the location, movement or spawning of content where tracked geometry transform information is not referenced. This becomes a bigger problem when working with baked lighting, as static content expects the World Origin to be in a specific spot.

## Steps

### Open an AR Project

1.  Open the **Project Browser** and create a new **Handheld AR** Blueprint project, or open an existing augmented reality project. If you need assistance creating a new augmented reality project, see the [Handheld AR Template Quickstart](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine) documentation.
    
2.  Open the **Find in Blueprints** menu item.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b77e62a-9a36-4db0-bc45-2d5930cfd85c/ar_findinblueprintsmenu.png)
3.  Search for **Debug Draw World Origin**. In the results, double-click the **Debug Draw World Origin** function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2926f9a-c2af-4723-ae01-6b331279b9e7/ar_blueprintsearch_debugdrawworldorigin.png)

### Show World Origin

The example project demonstrates a simple method of drawing the world origin. Drawing the world origin is a useful debugging exercise to help determine what the augmented reality system has determined as the world origin. As shown below, the world origin always starts at **0.0, 0.0, 0.0**.

#### Debug Draw World Origin

-   **Draw Debug String** - This function is placing the text string "WORLD ORIGIN" at the world origin (0.0, 0.0, 0.0) location.
    
-   **Draw Debug Arrow(s)** - These functions are drawing short arrows along X, Y, and Z axes respectively, starting from the world origin (0.0, 0,0, 0,0).
    

### Explore Other AR Functions

Exploring a project based on the **Handheld AR** Blueprint template provides an opportunity to examine the actual use of the various augmented reality functions in context. There are dozens of new augmented reality functions, so take some time to dig into a new project and explore the implementation details demonstrated.

A good place to start exploring the project and the new augmented reality functions is to open the **Content Browser**, navigate to **Content\\HandheldARBP\\Blueprints\\UI** and open the **BP\_DebugMenu** asset in the **Blueprint Editor**.