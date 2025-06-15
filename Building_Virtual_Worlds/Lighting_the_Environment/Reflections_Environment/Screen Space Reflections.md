# Screen Space Reflections

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:59

---

**Screen Space Reflection** is an effect which is enabled by default that alters the appearance of objects on the surface of **Materials**. There are only a handful of options that can be tweaked for this effect which are outlined below.

| Property | Description |
| --- | --- |
| **Intensity** | Enable/Fade/Disable the Screen Space Reflection feature by percentage (avoid numbers between 0 and 1 for consistency). |
| **Quality** | 0=Lowest Quality while 100=Maximum Quality (50 is the default to provide better performance). |
| **Max Roughness** | Used to determine what roughness we fade the Screen Space Reflections (0.8 works well, smaller can run faster). |