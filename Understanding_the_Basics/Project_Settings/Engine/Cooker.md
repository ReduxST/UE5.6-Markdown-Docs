# Cooker

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cooker-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/cooker-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:16:15

---

## Cooker

### Cooker

| **Section** | **Description** |
| --- | --- |
| **Enable Cook on the Side** | Enable cooking via the network in the background of the editor. Launch On uses this setting and requires the device to have network access to the editor. |
| **Enable Build DDC In Background** | Generate DDC data in the background for the desired Launch On platform. This speeds up the Launch On action. |
| **Iterative Cooking for Launch On** | 
Iterative cooking for builds launched from the editor (Launch On).

Enables the `-iterate` flag for Launch On.



 |
| **Iterative Cooking for File Cook Content** | 

Iterative cooking for content cooked via the **File > Cook Content** menu action.

Enables the `-iterate` flag when triggering content cooking from the **File** menu.



 |
| **Cook on the Fly for Launch On** | 

Cooking on the fly when launching from the editor (Launch On).

Enables the `-cookonthefly` flag for Launch On.



 |
| **Cook Progress Display Mode** | 

Controls cooker log output.

You can choose from the following options:

-   **Nothing**
    
-   **Remaining Packages**
    
-   **Package Names**
    
-   **Names and Remaining Packages**
    
-   **Instigators**
    
-   **Instigators and Count**
    
-   **Instigators and Names**
    
-   **Instigators and Names, and Count**.
    



 |
| **Ignore Ini Settings Out of Date for Iteration** | If enabled, iterative cooking ignores `.ini` changes, both in-editor and outside the editor. |
| **Ignore Script Packages Out of Date for Iteration** | If enabled, iteratice cooking ignores changes to the header file source code, both in-editor and outside the editor. |
| **Compile Blueprints in Development Mode** | Defines whether or not to compile Blueprints in development mode when cooking. |
| **Generate Optimized Blueprint Component Data** | 

Generates optimized component data to speed up Blueprint construction at runtime.

This option can increase the overall Blueprint memory usage in a cooked build.

Requires Event-Driven Loading (EDL), which is enabled by default.

You can choose from the following options:

-   **Disabled**
    
-   **Enabled Blueprints Only**
    
-   **All Blueprints**
    



 |
| **Classes Excluded on Dedicated Server** | List of class names to exclude when cooking for a dedicated server. |
| **Modules Excluded on Dedicated Server** | List of module names to exclude when cooking for a dedicated server. |
| **Classes Excluded on Dedicated Client** | List of class names to exclude when cooking for a dedicated client. |
| **Modules Excluded on Dedicated Client** | List of module names to exclude when cooking for a dedicated client. |
| **R-Values that Need to Be Versioned** | List of `r.` console variables that need to be versioned. |

### Textures

| **Section** | **Description** |
| --- | --- |
| **ASTC Compression Quality vs Speed (0-3, 0 is faster)** | Quality of 0 means fastest, 3 means best quality. |
| **ASTC Compression Quality vs Size (0-4, 0 is smallest)** | Quality of 0 means smallest (12x12 block size), 4 means best (4x4 block size). |
| **ASTC Texture Compressor** | 
Specifies which compressor to use for ASTC textures.

You can choose from the following options:

-   **Intel ISPC**
    
-   **ARM**
    



 |
| **ASTC HDR Profile** | 

Specifies whether to allow ASTC HDR profile using ARM encoder.

The HDR format is only supported on some devices, for example: Apple A13, Mali-G72, Adreno (TM) 660.



 |

### Editor

| **Section** | **Description** |
| --- | --- |
| **Allow Cooked Content in the Editor** | If true, the editor will be able to open cooked Assets (limited to a subset of supported Asset types). |