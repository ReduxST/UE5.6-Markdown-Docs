# Blueprint

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-project-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-project-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:10:44

---

## Blueprint Project Settings

### Blueprints

| **Section** | **Description** |
| --- | --- |
| **Force All Dependencies to Recompile (deprecated)** | 
Disables faster compiles for individual Blueprints if they have no function signature changes.

This setting has been deprecated and should not be used. You can't force all dependencies to compile when no changes are detected.



 |
| **Compiler Messages Disabled Except in Editor** | List of compiler messages that have been suppressed outside of full, interactive editor sessions for the current project. This is useful for silencing warnings that were added to the engine after the project was created and are going to be addressed as they are found by content authors. |
| **Compiler Messages Disabled Entirely** | 

List of compiler messages that have been suppressed completely. You should only supress compiler messages when using blueprints that you can't update and are raising non-critical warnings.



 |

### Actors

| **Section** | **Description** |
| --- | --- |
| **Validate Unloaded Soft Actor References** | 
If enabled, the editor will load packages to look for soft references to Actors when deleting or renaming Actors. This can be slow in large projects.

Disable this option to improve performance, but note that this will increase the chance of breaking Blueprints and sequences that use soft Actor references.



 |

### Experimental

| **Section** | **Description** |
| --- | --- |
| **Enable Child Actor Expansion in Tree View** | Enable the option to expand Child Actor components within component tree views. |
| **Default Child Actor Tree View Mode** | 
Default view mode to use for child Actor components in a Blueprint Actor's component tree hierarchy.

You can choose from the following options:

-   **Component Only:** Show only the outer component as a single component node.
-   **Component with Child Actor:** Include the child Actor hierarchy attached to the outer component as the root node.
-   **Child Actor Only:** Show only as a child Actor hierarchy (do not show the outer component node as the root).



 |
| **Namespaces to Always Include** | 

The list of namespaces to always expose in any Blueprint for all project users.

This setting requires Blueprint namespace to be enabled in **Editor Preferences**.



 |

### Play

| **Section** | **Description** |
| --- | --- |
| **Base Classes to Allow Recompiling During Play in Editor** | Any Blueprint deriving from one of these base classes will be allowed to recompile during Play-in-Editor (PIE). This setting exists both as an editor preference and project setting, and will take effect if enabled from either one of these panels. |