# Envs Folder Structure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/envs-folder-structure-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/envs-folder-structure-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:23

---

![The recommended Envs folder structure in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e0b8e1b-9668-4491-b200-7c260578dd07/cb_env.png)

The **Envs** folder contains all the assets specifically for your environments (envs).

Since source control only lets you exclusively check out binary assets, such as `.umap` files, each artist working on an environment at the same time must work on their own level. The solution to this is to divide an environment up into multiple [sublevels](/documentation/en-us/unreal-engine/managing-multiple-levels-in-unreal-engine) based on the type of Actors in each.

For example, a lighting artist would work in the lighting sublevel, and an FX artist in the FX sublevel. It is also common to have multiple GEO levels that divide the environment up into regions, each being worked on by a different artist. The number and types of sublevels used should be dependent on the needs of the production.

The files in this section are linked to the **Stages** folder files, as they will all be combined for the final In-Camera VFX persistent levels.

The following are the types of folders used for each environment in the sample project:

-   **Level Asset**: Level Assets follow a (LevelName)\_(Descriptor) structure. The \_P suffix is given to the Persistent Level, which acts as a container for the sublevels. Open this Level Asset to view the full environment composed of all the sublevels.
    
-   **SubLevels**: In this project, each Level was separated into the Caustics, FX, Geo, and Lighting sublevels.
    
-   **Snapshots**: Level Snapshot Assets associated with the Level.
    

For example:

-   CaveEntrance
    
    -   CaveEntrance\_P — Main persistent level
        
    -   SubLevels
        
        -   CaveEntrance\_Geo\_A
            
        -   CaveEntrance\_Lighting\_A
            
        -   CaveEntrance\_FX\_A
            
        -   CaveEntrance\_Anim\_A
            
        -   CaveEntrance\_Vis\_A
            
    -   Snapshots
        
        -   SNAP\_CaveEntrance\_(Description)
-   CavePath
    
-   SpaceJunkyard
    

A diagram showing the recommended Envs folder structure for your project in the Content Browser.