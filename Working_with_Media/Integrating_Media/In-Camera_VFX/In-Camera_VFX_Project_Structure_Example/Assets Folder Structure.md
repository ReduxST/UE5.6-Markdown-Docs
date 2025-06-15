# Assets Folder Structure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/assets-folder-structure-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/assets-folder-structure-in-unreal-engine)  
**Processed:** 2025-06-14 16:08:18

---

![The recommended Assets folder structure in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a040f757-9210-4b38-9ca9-b69a508a8270/cb_assets.png)

The **Assets** folder typically contains all Assets for creating Characters, Environments, and FX - Meshes, like Materials, Textures, Blueprints, and other source files. Level Assets are not included here.

Each subfolder contains the appropriate source files for that Asset. For example, the Chr folder contains Character Asset subfolders, one per Character used. Each contains that Character's source Assets, that is, Blueprints, Skeletal Meshes, Skeletons, Animations, Materials, and so on.

The following list is how the Assets were categorized for the [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine) project, expanded to include a few Asset types that were not used in that project. It's unlikely for any given project to use all possible Asset types.

-   Vegetation
    
    -   Tree\_A
        
        -   SM\_Tree\_A
            
        -   MI\_Tree\_A
            
        -   T\_Tree\_A\_BaseColor
            
-   Rocks
    
    -   Rock\_A
        
        -   BP\_Rock\_A
            
        -   SM\_Rock\_A
            
        -   MI\_Rock\_A
            
        -   T\_Rock\_A\_BaseColor
            
    -   Rock\_B
        
    -   Pebble\_A
        
-   Chr
    
    -   Backpacker\_A
        
        -   BP\_Backpacker\_A
            
        -   SK\_Backpacker\_A
            
        -   SKEL\_Backpacker\_A
            
        -   MI\_Backpacker\_A
            
        -   T\_Backpacker\_A\_BaseColor
            
        -   ABP\_Backpacker\_A\_Livelink
            
        -   ABP\_Backpacker\_A\_Game
            
        -   Animations
            
            -   A\_Backpacker\_A\_Run
                
            -   A\_Backpacker\_A\_Idle
                

A diagram showing the first part of the recommended Asset folder structure for your project in the Content Browser.

-   FX
    
    -   Birds\_A
        
        -   BP\_Birds\_A
            
        -   FXS\_Birds\_A\_(DescA)\_A
            
        -   FXS\_Birds\_A\_(DescB)\_A
            
        -   Emitters
            
            -   FXE\_Birds\_A\_(DescA)\_A
-   Decals
    
    -   MI\_Caustic\_A\_Decal
        
    -   T\_Caustic\_A\_M
        
-   HDRs
    
    -   HDR\_NightSky\_A
        
    -   HDR\_CitySky\_D
        
-   IES
    
    -   TLP\_Arri750Plus\_A
        
    -   TLP\_Arri750Plus\_B
        
-   OCIO
    
    -   (Stage Name)
        
        -   OCIO\_(Stage)\_A
            
        -   OCIO\_(Stage)\_B
            
        -   LUTS
            
            -   (Description).spi1d (file explorer only)
            
            OpenColorIO `.spi1d` files do not show in the Content Browser, only in the File Explorer. Refer to the [OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) documentation for more information.
            
-   MasterMaterials
    
    -   Ground\_A
        
        -   M\_Ground\_A
            
        -   T\_Ground\_A\_BaseColor
            
        -   MI\_WetGround\_A
            
    -   Textures
        
-   Props\*
    
-   Landscapes\*
    
-   Vehicles\*
    
-   Other\*
    

\* Not used for the In-Camera VFX Production Test.

A diagram showing the rest of the recommended Asset folder structure for your project in the Content Browser. It links back to the first part at the top.