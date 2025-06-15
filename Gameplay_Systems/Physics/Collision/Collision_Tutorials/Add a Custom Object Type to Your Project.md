# Add a Custom Object Type to Your Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-custom-object-type-to-your-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-custom-object-type-to-your-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:46

---

There will be times where 6 Object Response Channels and 2 Trace Response Channels simply are not granular enough for what you want to create. This is what the Collision Editor in your Project Settings is for. You can access them from the **Edit Menu** -> **Project Settings** -> **Collision**:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2559c1a6-8123-4448-b2fa-7328a639a959/col_projectsettings_1.png)

From here you can add new Object Response Channels and Trace Response Channels. Click the **New Object Channel...** or **New Trace Channel...** button, provide a name, select a **Default Response**, and click **Accept**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e68ec20-6838-4ee6-b582-b71ef339e00b/col_customchannel.png)

You can have up to 18 Custom Object Response Channels or Custom Trace Response Channels.

### Presets

Custom Presets can also be set here by expanding the **Preset** Category and clicking the **New...** button.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83b6c074-b963-421e-9216-f0f914349eae/col_custompresets.png)

From here you can name your preset, enable or disable collision, select your preset's Object Type, and finally define the behavior of each Response Channel for the selected Object Type.