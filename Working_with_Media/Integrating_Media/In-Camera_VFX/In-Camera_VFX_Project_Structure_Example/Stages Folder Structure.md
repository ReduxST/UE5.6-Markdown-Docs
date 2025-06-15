# Stages Folder Structure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/stages-folder-structure](https://dev.epicgames.com/documentation/en-us/unreal-engine/stages-folder-structure)  
**Processed:** 2025-06-14 16:52:01

---

![The recommended Stages folder structure in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb5edce1-0553-4f69-a373-1cd4fd48f6e3/cb_stages.png)

The **Stages** folder contains the **nDisplay Configurations** which describe the topology of the LED volume or volumes used and all related files.

The files in this section are linked to the **Envs** folder files, as they will all be combined for the final In-Camera VFX persistent levels.

-   EpicLA
    
    -   EpicLAStage\_P - Main Stage persistent level
        
    -   WarpMeshes - Meshes that make up the volume
        
        -   EpicLA\_C1
            
            -   SM\_EpicLA\_C1
                
            -   MI\_EpicLA\_C1\_(Description)\_A
                
            -   T\_EpicLA\_C1\_(Description)\_A
                
    -   Configs
        
        -   NPC\_EpicLA\_(Description)
            
        -   EpicLA\_(Description).cfg - `.cfg` files are not visible in the content browser
            

A diagram showing the recommended Stages folder structure for your project in the Content Browser.