# Collision Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:14:02

---

## Collision

You can have up to 18 custom channels including object and trace channels.

| **Section** | **Description** |
| --- | --- |
| **Object Channels** | 
This is the list of object types for your project.

If you delete an object type that is being used by the game, any uses of that type will revert to `WorldStatic`.



 |
| **Trace Channels** | 

This is the list of trace channels for your project.

If you delete a trace channel that is being used by the game, the behavior of the trace is undefined.



 |
| **Preset** | 

You can modify any of your project profiles.

If you modify the profile, it can change collision behavior. Use caution when changing collision profiles that are already in use.



 |