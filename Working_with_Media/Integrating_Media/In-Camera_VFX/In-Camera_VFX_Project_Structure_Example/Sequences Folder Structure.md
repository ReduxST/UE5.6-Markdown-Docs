# Sequences Folder Structure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sequences-folder-structure-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequences-folder-structure-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:29

---

![The recommended Media folder structure in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1bbcba5-60c4-4d26-ad66-ec8906996db7/cb_sequences.png)

The **Sequences** folder contains all **Level Sequences** and **Animations**, grouped by sequence abbreviation (CE, CP, and SJ in the example shown).

The **Edits** subfolder contains edits that apply to the entire project's sequences taken together. Each individual sequence folder also has an **Edits** subfolder, which applies specifically to that sequence only.

This sample uses the format `(Sequence Code)_(Setup)_(Camera or Anim Pass)_(Take)`. However, this is only an example take-naming convention. Use whatever naming system for your takes that makes sense for your project. The important point is for the naming system to be consistent.

-   Edits
    
    -   EDIT\_Origin\_00\_01
        
    -   EDIT\_Origin\_0A\_07
        
-   CE (Sequence Abbreviation)
    
    -   Takes - Sorted by shot name and take number
        
        -   CE\_00\_0A\_01
            
            -   LS\_CE\_00\_0A\_01
                
            -   SNAP\_CE\_00\_0A\_01
                
            -   CE\_00\_0A\_01\_Subscenes
                
                -   LS\_Actor01\_CE\_00\_0A\_01
                    
                -   LS\_Actor02\_CE\_00\_0A\_01
                    
            -   Animations
                
                -   A\_CE\_00\_0A-01\_Actor02
    -   Shots
        
    -   Previs
        
    -   Techvis
        
    -   Edits
        
        -   EDIT\_CE\_00\_01
            
        -   EDIT\_CE\_0G\_99
            
    -   Sublevels
        
        -   CE\_Lighting
            
        -   CE\_Chr
            

A diagram showing the recommended Sequences folder structure for your project in the Content Browser.