# Animation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:07:34

---

## Animation

### Compression

| **Section** | **Description** |
| --- | --- |
| **Compress Commandlet Version** | 
The compression version for the recompress commandlet.

Increase this value if you want to trigger a full recompression of all animations. Otherwise, only newly imported animations will be recompressed.



 |
| **Key End Effectors Match Name Array** | List of bone names to treat with higher precision, in addition to any bones with sockets. |
| **Force Recompression** | 

If enabled, this setting will forcibly recompress every animation.

Disable this setting before checking in your project, otherwise the Engine will recompress all animations each time the project is opened, affecting the performance negatively for all users of this project.



 |

### Performance

| **Section** | **Description** |
| --- | --- |
| **Enable Performance Log** | If true, recompression will log performance information. |
| **Strip Animation Data on Dedicated Server** | If true, animation track data will be stripped from dedicated server cooked data. |
| **Tick Animation on Skeletal Mesh Init** | 
When this property is enabled, an Animation-Tick will occur upon the initialization of a Skeletal Mesh, which is a behavior known as Zero-Ticking.

This property is disabled by default.

Zero-Ticking Animations during a Skeletal Mesh initialization was the default behavior for all versions of Unreal Engine before 4.19.



 |

### Custom Attributes

| **Section** | **Description** |
| --- | --- |
| **Bone Timecode Custom Attribute Name Settings** | 
Names that identify bone custom attributes representing the individual components of a timecode and a subframe along with a take name.

These will be included in the list of bone custom attribute names to import.



 |
| **Bone Custom Attributes Names** | 

List of custom attributes to import directly on their corresponding bone.

The meaning field is used to contextualize the attribute name and customize tooling for it.



 |
| **Bone Names With Custom Attributes** | List of bone names for which all custom attributes are directly imported on the bone. |
| **Attribute Blend Modes** | 

Custom Attribute-specific blend types (by name).

You can choose from the following options:

-   **Override**
-   **Blend**



 |
| **Default Attribute Blend Mode** | Default Custom Attribute blend type. |
| **Transform Attribute Names** | Names to match against when importing FBX node transform curves as attributes (can use `?` and `*` wildcards). |

### Mirroring

| **Section** | **Description** |
| --- | --- |
| **Mirror Find Replace Expressions** | Find and Replace Expressions used for mirroring. |