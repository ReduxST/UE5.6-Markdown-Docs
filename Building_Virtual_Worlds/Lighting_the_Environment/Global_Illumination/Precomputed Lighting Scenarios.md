# Precomputed Lighting Scenarios

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-precomputed-lighting-scenarios-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-precomputed-lighting-scenarios-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:38

---

**Unreal Engine** has support for using different **Precomputed Lighting Scenarios** in levels. This allows a single level to store and display multiple lighting setups, giving you the flexibility of dynamic lighting, but at the fixed cost of pre-computed lighting. Having the ability to change between different Precomputed Lighting Scenarios is of particular importance for Virtual Reality (VR) or Architectural Visualization projects that require high quality renderings with the benefits of fast performance measures. As you read through this reference, you'll learn how to use Precomputed lighting in your projects.

![Day Scenario](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e92c2dfb-71cd-4bcc-9cfe-3cb688632e3f/01-pcls-day.png)

![Night Scenario](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63c3ea7b-77e2-4125-97dc-a1f8f6b21ae7/02-pcls-night.png)

In the above image; the Directional Light, Sky Light, and Skybox have been placed in a Lighting Scenario level called **Day Scenario**. The Spotlights for the streetlights have been placed in a different Lighting Scenario level called **Night Scenario**.

## Feature Limitations

While Precomputed Lighting scenarios have a lot of advantages, there are some disadvantages and limitations that you'll need to be aware of while using them. In the following section, you'll go over some of these limitations and how you can avoid (or work around) them.

-   Only one Lighting Scenario level should be visible at any time in a game.
-   When a Lighting Scenario level is present, Lightmap data from all Sublevels will be placed inside of it so that only the Day Scenario Lightmaps are loaded when it's daytime. As a result, Lightmaps will no longer be streamed by Sublevels.
-   Sublevel Lightmap data is stored in the Lighting Scenarios BuiltData package. Registering Reflection Captures from other Sublevels modifies the active lighting scenario's BuiltData. Loading a sublevel twice and only loading a lighting scenario's BuiltData once will produce the following error:
    
    ```
    	`Error: Reflection capture /Game/Environments/Levels/Your_Level_Name.level_name:PersistentLevel.SphereReflectionCapture_1.NewReflectionComponent uploaded twice without reloading its lighting scenario level.`
    Copy full snippet
    ```
    Error: Reflection capture /Game/Environments/Levels/Your\_Level\_Name.level\_name:PersistentLevel.SphereReflectionCapture\_1.NewReflectionComponent uploaded twice without reloading its lighting scenario level.
    
    The Lighting scenario level must be loaded once for each time the reflection capture is uploaded.
    

## Using Lighting Scenarios

To use Lighting Scenarios in your project, you will need to do the following:

1.  First go to **Window** > **Levels** to open up the **Levels Manager**.
    
    ![Open Levels Manager window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad2a828c-67d6-4882-bb1d-941cd745bbb1/03-pcls-open-levels-window.png)
2.  With the **Levels Manager** open, right-click on a Sub level in the **Levels** menu, go to **Lighting Scenario**, and select the **Change to Lighting Scenario** option to make the level a **Lighting Scenario** level.
    
    ![Changing Level Lightning Scenario option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6106928-e071-41f4-9a2e-83c210d29019/04-pcls-lightning-scenario-options.png)
    
    When a **Lighting Scenario** level is visible, its Lightmaps will be applied to the world.
    
3.  Make sure the Level Streaming method is set to Blueprint by right-clicking on the Sublevel, going to **Change Streaming Method**, and selecting **Blueprint** (if it's not already selected).
    
    ![Selecting Level Streaming Method option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a3dc01c-5644-4a10-bfcf-2f30c2e46139/05-pcls-streaming-method-options.png)
4.  Now place any light or [Static Meshes](/documentation/en-us/unreal-engine/static-meshes) your project needs into either of the lighting levels and then build each level's lighting as you would with any other level.
    
    ![Building Lightning of the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f68a5e4-2bcb-46e3-b5ce-89bbe0ff9fc7/06-pcls-build-lightning.png)
5.  Once the lighting has finished building, open up the Blueprint of the **Persistent Level** and then add a **Load Stream Level (by name)** node, connecting it to the **Event Begin Play** node.
    
    ![Add Load Stream Level node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d1112a4-b8aa-4af2-aff6-0fcd9ada0b55/07-pcls-load-stream-level-node.png)
6.  Connect the **Event Begin Play** node to the **Load Stream Level** node and then input the name of the Level you want to load. Also, make sure to check both **Make Visible After Load** and **Should Block on Load** to make sure you can see the newly loaded level.
    
    ![Adjust Blueprint script for streaming](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98bf2a02-0533-4306-ac81-8d9464b9aff7/08-pcls-adjust-bp-script.png)
7.  Press the **Play** button to launch the project and when the first level loads, it should now be using the Day level lighting. To use Night level lighting, you can use the same setup, but you'll need to change the level name to your night time level (instead of the day time level).
    
    ![Day Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/897c10b6-a0c3-4734-95ce-2226f5084634/01-pcls-day.png)
    
    ![Night Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/054fa7ce-2535-4e22-88bf-a05a99bc6477/02-pcls-night.png)
    

Although there are some notable limitations, using Precomputed Lighting Scenarios can provide your project with many benefits; such as improved performance and the ability to change to baked lighting (to meet your project's needs).