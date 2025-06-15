# Interchange

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/interchange-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/interchange-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:31:32

---

## Interchange

Interchange is a new import system that you can use to import Assets directly into the Level. Currently, this system is in development and will be refined in the next versions of Unreal Engine.

### Interchange

| **Section** | **Description** |
| --- | --- |
| **Pipeline Stacks** | 
All the available pipeline stacks you want to use to import with Interchange.

The chosen pipeline stack executes all the pipelines in order, from top to bottom.

You can reorder the pipelines by clicking and dragging the grip on the left of any pipelines.



 |
| **Default Pipeline Stack** | This tells Interchange which pipeline to select when importing Assets. |
| **Pipeline Configuration Dialog Class** | 

This tells Interchange which pipeline to pop up when you need to configure the pipelines.

You can choose from the following options:

-   **None**
-   **InterchangePipelineConfigurationBase**
-   **InterchangePipelineConfigurationGeneric**



 |
| **Show Pipeline Stacks Configuration Dialog** | 

If enabled, the pipeline stacks configuration dialog will show every time Interchange must choose a pipeline to import or re-import.

If disabled, Interchange will use the `DefaultPipelineStack`.



 |

### Interchange (Experimental)

| **Section** | **Description** |
| --- | --- |
| **Use Interchange when Importing Into Level** | If enabled, will use Interchange when importing Assets into the Level. |
| **Default Scene Pipeline Stack** | This tells Interchange which pipeline to select when importing scenes. |