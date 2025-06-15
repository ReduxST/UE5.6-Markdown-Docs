# Niagara Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:25

---

## Goals

The Niagara Quick Start is designed to get you acquainted with creating visual effects (VFX) in Unreal Engine using Niagara. You will create a puff of smoke effect and attach it to your character's footsteps. It will look like the following.

## Objectives

-   Set up your project with meshes and materials for use with Niagara.
    
-   Create a basic smoke effect using a Niagara system.
    
-   Attach the smoke effect to a character's run animation.
    

## 1 - Setting Up Your Project

For the duration of this guide, use the **Blueprint Third Person Template** project with **Starter Content** enabled. If you have not created a project in Unreal Engine, see [Create a Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine).

1.  Launch **Unreal Engine** from the **Epic Games Launcher**.
    
2.  Click **Games**, then select the **Third Person Template**. Enable **Starter Content**.
    
3.  If needed, **Browse** to a new **Project Path**.
    
4.  Give your project a **Project Name**.
    
5.  Click **Create** to create your project.
    

[![Create a New Project](https://dev.epicgames.com/community/api/documentation/image/826b5938-ed12-4443-9e4a-9201f9fc2cd1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/826b5938-ed12-4443-9e4a-9201f9fc2cd1?resizing_type=fit)

*Click image for full size.*

Before you start creating your Niagara effect, you need to set up your project with some basic materials and assets that you will be using in the rest of this guide. After you complete this section, you will have everything you need to create your Niagara effect.

### Create or Import a Mesh Shape

The first thing you need for your project is a mesh shape for your effect. The shape you want to create or import is a **cloud**. There are a few ways of bringing in a mesh object into Unreal Engine:

-   Create your model in the 3D software of your choice, then export it as an **.fbx** file to easily import it into Unreal Engine.
    
-   Browse for a free cloud model on a site like [Sketchfab](https://sketchfab.com/), then import it into Unreal Engine.
    
-   Model the cloud directly in Unreal Engine using the [Modeling Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/getting-started-with-modeling-mode) tools.
    

Create or download a cloud model similar to the following.

[![Cloud Model by gaelinix](https://dev.epicgames.com/community/api/documentation/image/c880567a-334b-4077-8cea-8eeec22567d8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c880567a-334b-4077-8cea-8eeec22567d8?resizing_type=fit)

Click image for full size.

The cloud asset used in this tutorial is from [Sketchfab](https://sketchfab.com). This model is called **CLOUD high poly**, created by and copyrighted to **gaelinix**. This model is licenced under the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/).

You can [download the model here](https://sketchfab.com/3d-models/cloud-high-poly-7f3c3f525f8e42d3b99dcfe3abbc5e54).

You can also model your own cloud. Even if you do not have access to a high-end 3D modeling application like 3DS Max or Maya, you can use an open-source 3D modeling application such as [Blender](http://blender.org).

Once you have the model created or downloaded, create a place to store that model in the **Content** folder for easy organization.

1.  In the Content Browser, right-click and select **New Folder** to create a folder for your assets. Name it **Cloud**.
    
    [![Create Cloud Folder](https://dev.epicgames.com/community/api/documentation/image/15176259-13d5-4e2b-9112-ba133d0d7c64?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/15176259-13d5-4e2b-9112-ba133d0d7c64?resizing_type=fit)
    
    Click image for full size.
    
2.  Drag and drop your 3D model into the Content Browser to import it into your project.
    

For more information on how to import your model into Unreal Engine, see [Importing Content](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine).

### Create and Configure a Material

When you imported your cloud model, Unreal Engine may have created a **Material** for that model automatically. If not, you must create your own.

1.  Right-click in the Content Drawer and select **Material**. You can skip this step if Unreal Engine imported a material when you imported the model.
    
    [![Create Material](https://dev.epicgames.com/community/api/documentation/image/53950d39-6cd0-40ac-8c7b-5b6e6492e9b6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/53950d39-6cd0-40ac-8c7b-5b6e6492e9b6?resizing_type=fit)
    
    Click image for full size.
    
2.  Name the new material **CloudMaterial**.
    
    [![Rename Material](https://dev.epicgames.com/community/api/documentation/image/a76e2b0e-4e63-4a39-89dd-5e60689aa900?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a76e2b0e-4e63-4a39-89dd-5e60689aa900?resizing_type=fit)
    
    Click image for full size.
    
3.  Double-click the material to open it in the **Material Editor**.
    
4.  With the main Material node selected, locate the **Material** section in the **Details** panel. Change the **Blend Mode** to **Translucent**. Check the box for **Two Sided**. Leave the other settings at their default.
    
    [![Set Material Blend Mode](https://dev.epicgames.com/community/api/documentation/image/92a5eed1-c1be-493f-bb8c-44fa93ab9474?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/92a5eed1-c1be-493f-bb8c-44fa93ab9474?resizing_type=fit)
    
    Click image for full size.
    
5.  If you imported a model and you are using that material, there may already be something connected to the **Base Color** of the material. Delete this, as you will use the Niagara system's **Particle Color** setting to drive the material's color instead. If your material has nothing connected to **Base Color**, you can skip this step.
    
    [![Delete the Base Color Node](https://dev.epicgames.com/community/api/documentation/image/6cccc812-2cf5-46d6-891d-ace3774bcb62?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6cccc812-2cf5-46d6-891d-ace3774bcb62?resizing_type=fit)
    
    Click image for full size.
    
6.  Right-click in the graph and type `particle` in the search bar. Select **Particle Color** to add the node.
    
    [![Create a Particle Color Node](https://dev.epicgames.com/community/api/documentation/image/306d65d9-e31c-400b-bc81-ae157b38b9a4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/306d65d9-e31c-400b-bc81-ae157b38b9a4?resizing_type=fit)
    
    Click image for full size.
    
7.  Plug the top output of the Particle Color node into the **Base Color** input on the main Material Node.
    
    [![Connect Particle Color to Base Color](https://dev.epicgames.com/community/api/documentation/image/eb80b526-89ec-4b0a-b8b0-62e9784da22e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eb80b526-89ec-4b0a-b8b0-62e9784da22e?resizing_type=fit)
    
    Click image for full size.
    
8.  If you imported a model, it may have automatically created a **Texture Sample** node and connected it. If there isn't one, create your own. You can do this by holding **T** and clicking inside the Node Graph.
    
    [![Create a Texture Sample Node](https://dev.epicgames.com/community/api/documentation/image/f5f4336c-21f8-4a54-8cd2-935dbd706d2b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f5f4336c-21f8-4a54-8cd2-935dbd706d2b?resizing_type=fit)
    
    Click image for full size.
    
9.  You will add some noise from the **Starter Content** to the texture to make it appear more like smoke. With the Texture Sample node selected, locate the **Material Expression Texture Base** section in the **Details** panel. Next to **Material**, click the dropdown, then type **Noise** in the search bar. Select the **T\_Perlin\_Noise\_M** texture.
    
    [![Set Texture to Noise](https://dev.epicgames.com/community/api/documentation/image/9259196e-00a9-458d-ba32-8f8662db885d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9259196e-00a9-458d-ba32-8f8662db885d?resizing_type=fit)
    
    Click image for full size.
    
10.  Right-click in the graph and type `dynamic` in the search bar. Select **Dynamic Parameter** to add that node.
    
    [![Create a Dynamic Parameter](https://dev.epicgames.com/community/api/documentation/image/7f0f4de6-0de3-4c72-a621-c0d3f48d86c3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7f0f4de6-0de3-4c72-a621-c0d3f48d86c3?resizing_type=fit)
    
    Click image for full size.
    
11.  With the Dynamic Parameter node selected, locate the **Material Expression Dynamic Parameter** section in the **Details** panel. In **Array 0**, change the name to **Erode**.
    
    [![Set Erode Parameter](https://dev.epicgames.com/community/api/documentation/image/38c8eba0-cc81-4650-9111-1f7f5c364827?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/38c8eba0-cc81-4650-9111-1f7f5c364827?resizing_type=fit)
    
    Click image for full size.
    
12.  Right-click in the graph and type `step` in the search bar. Select **Value Step** to add that node.
    
    [![Add Value Step Node](https://dev.epicgames.com/community/api/documentation/image/d3d61887-ca67-4ea5-8ea2-5889cb963ff5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d3d61887-ca67-4ea5-8ea2-5889cb963ff5?resizing_type=fit)
    
    Click image for full size.
    
13.  Drag off the **R** output of the Texture Sample node, and plug it into the **Gradient** input of the Value Step node.
    
    [![Connect Texture Sample to Gradient](https://dev.epicgames.com/community/api/documentation/image/ce2dab89-527e-4f25-9a6f-d09edb8c578e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce2dab89-527e-4f25-9a6f-d09edb8c578e?resizing_type=fit)
    
    Click image for full size.
    
14.  Drag off the **Erode** output of the Dynamic Parameter node, and plug it into the **Mask Offset Value** input of the **Value Step** node.
    
    [![Connect Erode to Mask Offset Value](https://dev.epicgames.com/community/api/documentation/image/3eb87ce2-30bc-46f2-9684-35c1b3b81b26?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3eb87ce2-30bc-46f2-9684-35c1b3b81b26?resizing_type=fit)
    
    Click image for full size.
    
15.  Drag off the **Results** output of the Value Step node, and plug it into the **Opacity** input of the main Material node.
    
    [![Final Material Setup](https://dev.epicgames.com/community/api/documentation/image/39bb627e-0d1f-433b-8430-b277b26f9f4d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39bb627e-0d1f-433b-8430-b277b26f9f4d?resizing_type=fit)
    
    Click image for full size.
    
16.  Click **Apply** and **Save**, then close the Material Editor.
    

#### Section Result

You have now imported a mesh model of a cloud. You have also set up the material. You are now ready to create the Niagara effect.

## 2 - Creating Your Effect

### Create the System

Next you will create your Niagara system.

1.  To create a new Niagara system, right-click in the **Content Browser** and click **FX > Niagara System**.
    
    [![Right-click in the Content Browser and click FX - Niagara System](https://dev.epicgames.com/community/api/documentation/image/571b025a-d974-444b-a711-d0c0f249441e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/571b025a-d974-444b-a711-d0c0f249441e?resizing_type=fit)
    
2.  Click the **Template** category on the left-hand side and select the **Simple Sprite Burst** system. Click **Create**.
    
    [![Select the Simple Sprite Burst system and click Create](https://dev.epicgames.com/community/api/documentation/image/bcf58e7d-6886-43f6-a3fc-51065014afbd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bcf58e7d-6886-43f6-a3fc-51065014afbd?resizing_type=fit)
    
3.  Name the system **FX\_DustCloud**. Double-click to open it in the Niagara Editor.
    
    [![Name the system FX_DustCloud and open it in the Niagara Editor](https://dev.epicgames.com/community/api/documentation/image/842b0b49-5151-4c0d-9a04-61d87cf159f1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/842b0b49-5151-4c0d-9a04-61d87cf159f1?resizing_type=fit)
    
4.  The emitter instance in your new system has the default name of **SimpleSpriteBurst**. You can rename it, however. Double-click the name of the emitter instance in the **System Overview**, and the field will become editable. Name the emitter **FX\_DustCloud**.
    

[![Rename the Emitter](https://dev.epicgames.com/community/api/documentation/image/493df0dd-dd57-461e-85cf-c5e1c1cf528f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/493df0dd-dd57-461e-85cf-c5e1c1cf528f?resizing_type=fit)

Click image for full size.

If you only have one emitter in your Niagara System, renaming it is optional. However, if you create a Niagara system with more than one emitter, naming them is important for organization and clarity.

### Configure the Render Group

The Emitter is set up as a vertical stack, broken up into groups. The default groups in the emitter are:

-   Emitter Spawn
    
-   Emitter Update
    
-   Particle Spawn
    
-   Particle Update
    
-   Render
    

To find out more about Emitter Groups and how they work, see the [Niagara Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine) page.

Because you are using a 3D model to generate the effect, you need to set up the Render group first in order to see the preview.

1.  In the **System Overview**, select **Render** to open the Render group in the **Selection** panel.
    
    [![Select Render Group](https://dev.epicgames.com/community/api/documentation/image/1181bbaf-2ec5-4ab2-a272-6706bb45adc5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1181bbaf-2ec5-4ab2-a272-6706bb45adc5?resizing_type=fit)
    
    Click image for full size.
    
2.  Because you are using a 3D model, you need a Mesh Renderer and not a Sprite Renderer. Click the **Trashcan** icon to delete the Sprite Renderer. **Selection** panel.
    

[![Delete Sprite Renderer](https://dev.epicgames.com/community/api/documentation/image/174d694d-7d72-435e-a806-ea3d8226c397?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/174d694d-7d72-435e-a806-ea3d8226c397?resizing_type=fit)

Click image for full size.

1.  With the Render group selected, in the **Details** panel, click the **Plus sign** icon (**+**). Select **Mesh Renderer** from the list to add this module to the Render group.
    
    [![Add Mesh Renderer](https://dev.epicgames.com/community/api/documentation/image/9fa0c32f-a5e2-4345-81a9-03ed38d6be2a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9fa0c32f-a5e2-4345-81a9-03ed38d6be2a?resizing_type=fit)
    
    Click image for full size.
    
2.  For **Facing Mode**, click the dropdown and select **Velocity**.
    
3.  Click the triangle next to **Meshes** to expand the array. This array is where you can add one or more mesh objects to the renderer. Click the dropdown next to **Index (0)** in the array, then select the mesh you imported in the **Project Setup** section.
    
    [![Add Mesh Renderer](https://dev.epicgames.com/community/api/documentation/image/2bf03b00-aa5a-40d5-a718-3408f9276479?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bf03b00-aa5a-40d5-a718-3408f9276479?resizing_type=fit)
    
    Click image for full size.
    
4.  Click to the checkbox **Enable Override Materials**. You can then specify the material to apply to the mesh. The default is **0 Array elements**. Click the **Plus sign** (**+**) icon to add an array element.
    
    [![Enable Material Overrides](https://dev.epicgames.com/community/api/documentation/image/99615c93-e510-4085-859d-65ae0ed2d0b8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/99615c93-e510-4085-859d-65ae0ed2d0b8?resizing_type=fit)
    
    Click image for full size.
    
5.  Click the dropdown next to **Explicit Mat**, then select the material you made in the Project Setup section.
    
    [![Set the Material](https://dev.epicgames.com/community/api/documentation/image/f575ecaa-8d1e-4a10-a434-2881c4a816f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f575ecaa-8d1e-4a10-a434-2881c4a816f7?resizing_type=fit)
    
    Click image for full size.
    
6.  From the **Content Browser**, drag your Niagara system into your Level. Position it near the foot of the Player Character, so you can check the size and shape of the effect in relationship to the character.
    

When you make a particle effect, it is always a good idea to drag your system into your level. This gives you a chance to see every change and edit in context.

#### Section Result

After completing this section, you have a Niagara system and an emitter instance, and you have dragged the system into the Level so you can preview it next to the Player Character. In the next part, you will edit the settings in the Niagara system to create the dust cloud effect.

## 3 - Editing the Module Settings

The Niagara Editor displays each emitter as a stack, with several groups of settings. You will edit the modules in each group one at a time.

This effect does not have any modules in the Emitter Spawn group, so you will skip that section. For more information on the different groups and what they do, see the [Niagara Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine) page.

### Configure the Emitter Update Group

First you will edit the modules in the Emitter Update group. Modules placed in this group will update every frame as the system ages.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    [![Select the Emitter Update Group](https://dev.epicgames.com/community/api/documentation/image/a017f021-65aa-40f1-8975-17640b4da360?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a017f021-65aa-40f1-8975-17640b4da360?resizing_type=fit)
    
    Click image for full size.
    
2.  Expand the **Emitter State** module. By default, the **Life Cycle Mode** should be set to **Self**.
    
3.  Change the **Emitter State** settings to the following values. This will give you a dust poof that appears once and then dissipates.
    
    [![Set the Life Cycle Settings](https://dev.epicgames.com/community/api/documentation/image/a7c47f3f-c935-4b92-8eca-ce07225339c1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a7c47f3f-c935-4b92-8eca-ce07225339c1?resizing_type=fit)
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | 
    **Life Cycle Mode**
    
     | 
    
    Self
    
     |
    | 
    
    **Inactive Response**
    
     | 
    
    Complete
    
     |
    | 
    
    **Loop Behavior**
    
     | 
    
    Once
    
     |
    | 
    
    **Loop Duration Mode**
    
     | 
    
    Fixed
    
     |
    | 
    
    **Loop Duration**
    
     | 
    
    1
    
     |
    
4.  Expand the **Spawn Burst Instantaneous** module. Set the **Spawn Count** to **10**. A spawn count of 10 gives us a dust cloud that is big enough to be visible, but small enough to be plausible.
    

[![Set the Spawn Count](https://dev.epicgames.com/community/api/documentation/image/d59e0cef-9bec-4314-a777-d2ce277c2664?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d59e0cef-9bec-4314-a777-d2ce277c2664?resizing_type=fit)

Click image for full size.

### Configure the Particle Spawn Group

Next, you will edit the modules in the Particle Spawn group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    [![Select the Particle Spawn Group](https://dev.epicgames.com/community/api/documentation/image/dabb86b5-8dd0-4ae9-98e8-e24836751c73?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dabb86b5-8dd0-4ae9-98e8-e24836751c73?resizing_type=fit)
    
    Click image for full size.
    
2.  Expand the **Initialize Particle** module. Under **Point Attributes**, locate the **Lifetime Mode** dropdown. Use the dropdown to select **Random**. This adds **Minimum** and **Maximum** fields to the Lifetime value. This will add some variation in how long each particle displays. Set the Minimum and Maximum fields to the following.
    
    [![Set the Lifetime Settings](https://dev.epicgames.com/community/api/documentation/image/81fb3ca7-f73f-4250-9fc6-1f29edd51d37?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/81fb3ca7-f73f-4250-9fc6-1f29edd51d37?resizing_type=fit)
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | 
    **Minimum**
    
     | 
    
    .4
    
     |
    | 
    
    **Maximum**
    
     | 
    
    .6
    
     |
    
3.  Locate the **Color** setting. In the example, the **Color** is set to a light tan color that looks like dust. Click on the color swatch, then use a color picker to choose a color. This value is saved to **Particle Color**, that you already connected to the material in the Project Setup step.
    
    [![Set the Particle Color](https://dev.epicgames.com/community/api/documentation/image/b9139bae-22ae-4d59-9c1a-6c37ea69015f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b9139bae-22ae-4d59-9c1a-6c37ea69015f?resizing_type=fit)
    
    Click image for full size.
    
4.  You will add some variation to the size of the particles by adding a random factor to the mesh scale. Under **Mesh Attributes**, locate the **Mesh Scale Mode** dropdown. Select **Random Uniform**. Set the following values for **Mesh Uniform Scale Min** and **Mesh Uniform Scale Max**.
    
    [![Set the Mesh Size](https://dev.epicgames.com/community/api/documentation/image/fa1dc0b2-3dab-49f6-8f6d-8d922c1bfc3c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fa1dc0b2-3dab-49f6-8f6d-8d922c1bfc3c?resizing_type=fit)
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | 
    Mesh Uniform Scale Min
    
     | 
    
    1.0
    
     |
    | 
    
    Mesh Uniform Scale Max
    
     | 
    
    2.0
    
     |
    
5.  With the **Particle Spawn** group selected, click the **Plus sign** icon (**+**) to add a new module to this group. Select **Orientation > Initial Mesh Orientation**. This contains rotation settings for your particle mesh. You want to add some rotation to the shape so it is less uniform. This will make the dust cloud look a little more natural.
    
    [![Add the Initial Mesh Orientation Module](https://dev.epicgames.com/community/api/documentation/image/1179b14f-3a36-4b31-b2b0-efffc77cd9d3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1179b14f-3a36-4b31-b2b0-efffc77cd9d3?resizing_type=fit)
    
    Click image for full size.
    
6.  Under **Rotation**, click to enable initial rotation in the module. Click the downward arrow next to **Rotation**, then select **Dynamic Inputs > Random Ranged Vector**.
    
    [![Set Rotation to Random Range Vector](https://dev.epicgames.com/community/api/documentation/image/4b7e9b64-390f-4c81-8d9f-8109ef839b37?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4b7e9b64-390f-4c81-8d9f-8109ef839b37?resizing_type=fit)
    
    Click image for full size.
    
7.  Minimum and maximum values generate a random factor to the initial rotation. Leave the **Minimum** and **Maximum** values at their default.
    
    [![Set Rotation values](https://dev.epicgames.com/community/api/documentation/image/0a9e0924-c3f2-4c6b-87e0-437f8f344df2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0a9e0924-c3f2-4c6b-87e0-437f8f344df2?resizing_type=fit)
    
    Click image for full size.
    
8.  With the **Particle Spawn** group selected, click the **Plus sign** icon (**+**) to add a new module. Select **Location > Shape Location**. The Shape Location module lets you set a region in which new particles are created when they are born.
    
    [![Add Shape Location Module](https://dev.epicgames.com/community/api/documentation/image/ec363c5b-7abe-4d7e-b959-e1a0d60cafc1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ec363c5b-7abe-4d7e-b959-e1a0d60cafc1?resizing_type=fit)
    
    Click image for full size.
    
9.  For this example, set **Shape Primitive** to **Cylinder**. You can experiment with different shapes in future examples depending on the look you want to achieve. For now, you want the dust cloud to stay close to the ground, so change the **Cylinder Height** to **1**. You do not want the dust cloud to be too much bigger than the foot, so change the **Cylinder Radius** to **10**.
    
    [![Set Shape Location Settings](https://dev.epicgames.com/community/api/documentation/image/a26d70b8-ef6e-4e33-81e9-3683ff881016?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a26d70b8-ef6e-4e33-81e9-3683ff881016?resizing_type=fit)
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | 
    Shape Primitive
    
     | 
    
    Cylinder
    
     |
    | 
    
    Cylinder Height
    
     | 
    
    1.0
    
     |
    | 
    
    Cylinder Radius
    
     | 
    
    10.0
    
     |
    
10.  With the **Particle Spawn** group selected, click the **Plus sign** icon (**+**) to add a new module to this group. Select **Velocity > Add Velocity**. When you add velocity in the Particle Spawn group, it adds an initial velocity to the particles at the moment of their birth, at the specified speed.
    
    [![Add an Add Velocity Module](https://dev.epicgames.com/community/api/documentation/image/aa377287-cbe3-41f0-9239-a301ee9a65fa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aa377287-cbe3-41f0-9239-a301ee9a65fa?resizing_type=fit)
    
    Click image for full size.
    
11.  Set the **Velocity Mode** to **From Point**. This will apply velocity radially outwards from the origin point of the Niagara system. Set the **Velocity Speed** to **20**. you do not want the particles to spread too far, just enough to represent dust that is disturbed by the runner's footsteps. You can adjust this value as needed to achieve the look you like.
    
    [![Set the Add Velocity Settings](https://dev.epicgames.com/community/api/documentation/image/adf701c7-274e-475a-8c7e-be194e1b918f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/adf701c7-274e-475a-8c7e-be194e1b918f?resizing_type=fit)
    
    Click image for full size.
    
12.  With the **Particle Spawn** group selected, click the **Plus sign** icon (**+**) to add a new module to this group. Select **Forces > Acceleration Force**. You are going to use this to give the dust cloud a small amount of upward momentum, so the dust cloud spreads out and up from the character's footstep.
    
    [![Add the Acceleration Force Module](https://dev.epicgames.com/community/api/documentation/image/c16b4071-661b-4f6a-99a1-39caf75fcb8d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c16b4071-661b-4f6a-99a1-39caf75fcb8d?resizing_type=fit)
    
    Click image for full size.
    
    An error displays after you add a velocity or force module, because added modules are always positioned at the bottom of the group's stack. That positioning places them after the **Solve Forces and Velocity** module. All velocity and force modules need to be placed above the solver to be properly computed.
    
13.  Click **Fix Issue** to resolve this error. Alternatively, You could manually move the module above Solve Forces and Velocity by dragging it up in the stack.
    
    [![Solve Forces and Velocity Warning](https://dev.epicgames.com/community/api/documentation/image/d72e366c-90b3-4185-8db2-87cd86068468?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d72e366c-90b3-4185-8db2-87cd86068468?resizing_type=fit)
    
    Click image for full size.
    
14.  In the Acceleration Force module, set the **Acceleration** to **X:0, Y:0, and Z:200**. Now the dust cloud spreads out and up, but the upward momentum is a little too much. In the Particle Update step, you will add drag to slow down the upward momentum of the dust particles on each frame.
    

[![Set the Acceleration Settings](https://dev.epicgames.com/community/api/documentation/image/0e2a6cd8-76a7-4457-9db1-ad1230dce923?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0e2a6cd8-76a7-4457-9db1-ad1230dce923?resizing_type=fit)

Click image for full size.

### Configure the Particle Update Group

Finally, you will edit the settings in the Particle Update group. These behaviors are calculated on each particle every frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    [![Select the Particle Update Group](https://dev.epicgames.com/community/api/documentation/image/6ec88753-fad0-452f-aa2e-970b377884eb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6ec88753-fad0-452f-aa2e-970b377884eb?resizing_type=fit)
    
    Click image for full size.
    
2.  Click the **Trashcan** icon to delete the **Scale Color** module. You will not need it for this effect.
    
    [![Delete the Scale Color Module](https://dev.epicgames.com/community/api/documentation/image/9a0c355a-2585-4cea-9715-32e92b9c59a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a0c355a-2585-4cea-9715-32e92b9c59a2?resizing_type=fit)
    
    Click image for full size.
    
3.  With the **Particle Update** group selected, click the **Plus sign** icon (**+**) to add a new module. Select **Materials > Dynamic Material Parameters**. This is how you will connect to the Erode Dynamic Parameter in your Material.
    
    You can drag to reorder modules in the emitter in the System Overview. However, you cannot reorder modules in the Selection panel.
    
    [![Add the Dynamic Material Parameters Module](https://dev.epicgames.com/community/api/documentation/image/46cfe10e-daa4-425a-9343-7e11380fce4b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/46cfe10e-daa4-425a-9343-7e11380fce4b?resizing_type=fit)
    
    Click image for full size.
    
4.  In the **Dynamic Material Parameters** module, you see the **Erode** parameter you set up in your material. Click the downward arrow for Erode, and select **Dynamic Inputs > Float from Curve**.
    
    [![Set Erode to Float From Curve](https://dev.epicgames.com/community/api/documentation/image/b7a1e14e-64cc-4e9c-a25d-6e9bf6f57601?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b7a1e14e-64cc-4e9c-a25d-6e9bf6f57601?resizing_type=fit)
    
    Click image for full size.
    
5.  In the curve editor, click the **Drop Off** template to apply that style to the curve. This will make the material fade out over time.
    
    [![Apply the Drop Off Template to Float From Curve](https://dev.epicgames.com/community/api/documentation/image/638240a6-82a5-4dfe-ab0f-76b6b066d765?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/638240a6-82a5-4dfe-ab0f-76b6b066d765?resizing_type=fit)
    
    Click image for full size.
    
6.  With the **Particle Update** group selected, click the **Plus sign** icon (**+**) to add a module to this group. Select **Forces > Drag**.
    
    An error displays after you add a velocity or force module, because added modules are always positioned at the bottom of the group's stack. That positioning places them after the Solve Forces and Velocity module. Click **Fix Issue** to resolve this error.
    
    [![Add Drag Module](https://dev.epicgames.com/community/api/documentation/image/3a0a7714-8e96-4f6d-a571-81aef4859f23?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3a0a7714-8e96-4f6d-a571-81aef4859f23?resizing_type=fit)
    
    Click image for full size.
    
7.  In the Drag module, set the **Drag** to **8**. The **Drag** setting interacts with the acceleration force and keeps the dust cloud's upward movement from seeming too unrealistic.
    

[![Set the Drag Settings](https://dev.epicgames.com/community/api/documentation/image/17f74636-8779-4c69-8aff-b29060b9c7d7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/17f74636-8779-4c69-8aff-b29060b9c7d7?resizing_type=fit)

Click image for full size.

#### Section Result

You have created the dust effect, and you should be able to see it in your level, next to the Player Start model. If the effect does not look right to you, you can adjust the various module settings until you like the look of the effect.

## 4 - Attaching the Niagara Effect to a Character

Now you are going to add this effect to a character's run animation. In this example, you will attach the effect to the generic **Quinn** character included in the Third Person template. However, you can use these steps to add a Niagara effect to any character you have set up in Unreal Engine.

1.  In the **Content Drawer**, navigate to **Content > Characters > Mannequins > Animations > Quinn**. Double-click the **MF\_Run\_Fwd** animation to open it in the **Animation Editor**.
    
    [![Open Run Animation](https://dev.epicgames.com/community/api/documentation/image/9f6410e1-a94e-4efd-8f0f-f12e4b7f2d89?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9f6410e1-a94e-4efd-8f0f-f12e4b7f2d89?resizing_type=fit)
    
    Click image for full size.
    
2.  In the **Animation timeline**, click **Pause** to pause the looping animation. Use the scrub pointer to find the moment the character's right foot hits the ground. You are going to put your dust effect right at that spot.
    
    [![Scrub Playhead to Foot Impact Time](https://dev.epicgames.com/community/api/documentation/image/23af2c2b-3a09-4e83-8465-b4838cdf1463?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/23af2c2b-3a09-4e83-8465-b4838cdf1463?resizing_type=fit)
    
    Click image for full size.
    
3.  Locate the **Notifies** section. With a notify, you are marking the animation with a location for an effect. To keep your timeline organized, create a new track to put the Niagara events on. Click on **Track**, then select **Add Notify Track.** Name it **Niagara**.
    
    [![Add Notify Track](https://dev.epicgames.com/community/api/documentation/image/e35820de-44ff-4c67-a3d6-0622eda672f4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e35820de-44ff-4c67-a3d6-0622eda672f4?resizing_type=fit)
    
    Click image for full size.
    
4.  You will see a line that runs down from the scrub bar in the timeline. Right-click where the playhead intersects with the Niagara notify track. Select **Add Notify > Play Niagara Particle Effect**. A marker is placed at that point in the animation, with the default label PlayNiagaraEffect.
    
    [![Add Niagara Particle Effect Notify](https://dev.epicgames.com/community/api/documentation/image/3e7bf7e7-87f3-4dda-a52d-23f8c1246cde?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3e7bf7e7-87f3-4dda-a52d-23f8c1246cde?resizing_type=fit)
    
    Click image for full size.
    
5.  With the **PlayNiagaraEffect** notify selected, locate the **Anim Notify** section in the **Details** panel. This is where you select the Niagara System you want to add to the animation. Click the dropdown next to **Niagara System**, and select the **FX\_DustCloud** system you created in Niagara. The label on the notify changes to **FX\_DustCloud**.
    
    [![Set the Niagara System in Notify](https://dev.epicgames.com/community/api/documentation/image/1da2a7cd-f5cd-4b6b-8661-5d52eb9269f3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1da2a7cd-f5cd-4b6b-8661-5d52eb9269f3?resizing_type=fit)
    
    Click image for full size.
    
6.  Repeat the above steps for the left foot. You can also copy and paste Notifies directly in the timeline. To refine the look further, you can offset the location of the cloud to match the position of each foot where it hits the ground. With the **Anim Notify** selected, locate the **Location Offset** values. Adjust the values as needed.
    
    [![Set the Location Offset in Notify](https://dev.epicgames.com/community/api/documentation/image/ba4c28d5-fc52-408e-92ae-846d14bdb28c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ba4c28d5-fc52-408e-92ae-846d14bdb28c?resizing_type=fit)
    
    Click image for full size.
    
7.  Click **Play** in the Timeline to see a preview of the effect, and refine values as needed.
    
8.  Close the Animation Editor. In the **Level Editor**, click the **Play** button to preview the level. Run around and see your effect in action.
    

#### Section Result

You have attached the Niagara effect to your character's run animation. Congratulations!

### Refining the Look of the Smoke Cloud

You may want to continue tweaking the values to get the final look that you want. Here are some ideas of things you can try to go back and play around with, now that your scene is set up:

-   Try adjusting the color in the **Initialize Particle** module.
    
-   Add a **Scale Mesh Size** module to the **Particle Update** group. Set the **Scale Factor** to **Vector from Curve**, and play around with different shapes to change the size of the cloud over time.
    
-   Refine the size of the model in the **Mesh Renderer**.
    
-   Refine the location of the cloud in the **Anim Notify**.
    

## 5 - Reviewing the End Result

You have finished making the effect in the Quick Start guide. It should look similar to the following.

## 6 - On Your Own

Now that you have created a basic effect and attached it to a character, you can try some other related tutorials to do more with this character. You can also make more effects in Niagara.

-   You can use a [Ribbon](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-ribbon-effect-in-niagara-for-unreal-engine) to create a trail behind your character as it runs.
    
-   You can check out our [Animation tutorials](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-workflow-guides-and-examples-in-unreal-engine) to learn how to create or modify additional animations for your character.
    
-   You can learn how to use [Animation Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) to do even more with your character.