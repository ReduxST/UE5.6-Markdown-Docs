# Sprite Smoke

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:55

---

A commonly used visual effects (VFX) technique is rendering Texture and Materials to 2D camera-facing planes, which are called *sprites*. In the following tutorial, you will set up a Niagara Emitter to work with sprites. When you place the Niagara System containing the Niagara Emitter into a Level, you will see the effect displayed in that Level.

**Prerequisite Steps:**

This how-to uses the **M\_smoke\_subUV** Material, which can be found with the **Starter Content**. If you have not done so already, make sure that this Material or the Starter Content has been added to your project.

## Project Setup

1.  First, make a new folder in the Content Browser to hold the assets for your effect. Make sure you are at the top level (Content), then right-click in the **Content Browser** and select **New Folder**. Name your folder something like **SpriteEffect**.
    
    If you are going to create multiple Niagara effects in your project, you might want to create a folder called NiagaraFX (or something similar), and then create a sub-folder for your sprite effect.
    
2.  Before you can create this effect, you need to make or locate a material to use for the sprites in our emitter. For this example, you will use a material from the Starter Content. It is possible to pull in this material without locating it or moving it anywhere, but in some cases you might want to make a copy of the original and put that either in the folder for your effect, or in a separate Materials folder you have previously created. To do so, follow these steps:
    
    1.  Type `m_smoke` in the search bar of the Content Browser. You should see the **M\_smoke\_subuv** material in your search results.
        
        Click image for full size.
        
    2.  To put a copy of it in another folder, just click and drag that material to the desired folder, and in the popup menu select either **Move Here** or **Copy Here**. **Moving** it will delete the original material in its previous location, and move it to the new location. **Copying** it will create a copy in the new location, while leaving the original in its original location. If you want to create your own material for the sprite, see pages in the **Materials** section of our documentation.
        

## Create the System and Emitter

Next you will create a Niagara system, and inside it an emitter. The system is a container within which you can put one or more emitters. The emitter is the source of new particles that are generated.

1.  First, create a **Niagara System** by right-clicking in the Content Browser, and from the displayed menu select **FX > Niagara System**. The Niagara System wizard displays.
    
    Click image for full size.
    
2.  Select **New system from selected emitters**. Then click **Next**.
    
    Click image for full size.
    
3.  Under **Template**, select **Simple Sprite Burst**. Click the **Plus sign** icon (**+**) to add the emitter to the list of emitters to add to the system. Then click **Finish**.
    
    Click image for full size.
    
4.  Name the new system **SmokeSystem**. Double-click to open it in the Niagara Editor.
    
5.  The emitter instance in your new system has the default name of **SimpleSpriteBurst**. You can rename it, however. Click the name of the emitter instance in the System Overview, and the field will become editable. Name the emitter **FX\_Smoke**.
    
    Click image for full size.
    

## Change Renderer Settings

1.  In this guide, you will go through the Emitter module groups as they appear in the stack. However, until you set your material in the Renderer you won't see anything in your preview or in your Level. So first, in the **System Overview** select the **Sprite Renderer** to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  This is where you select the material for our effect. Since the material is a SubUV material, you need to tell the renderer how many images are in the image grid. Set the following properties to the following values.
    
    Click image for full size.
    
    | Property Name | Value |
    | --- | --- |
    | **Material** | M\_smoke\_subUV |
    | **Sub Image Size** | X: 8.0, Y: 8.0 |
    | **Sub UV Blending Enabled** | Checked |
    
3.  Drag the **SmokeSystem** into your Level.
    
    When you make a particle effect, it is always a good idea to drag your system into your Level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your Level.
    

## Edit the Emitter Update Group Settings

First you will edit the modules in the Emitter Update group. These are behaviors that apply to the emitter, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  You want to create a constant column of smoke, not a burst of smoke. Click the **Trashcan** icon to delete the **Spawn Burst Instantaneous** module.
    
    Click image for full size.
    
3.  Add the **Spawn Rate** module to the **Emitter Update** group by clicking the **Plus sign** icon (**+**) and selecting **Spawn Rate**.
    
    Click image for full size.
    
4.  In the **Spawn Rate** module, set the Spawn Rate to **50**. This will give us a good-sized puffy shape made of smoke. This is a good start to your effect.
    
    Click image for full size.
    
5.  For now, while you are building the effect, you want to set the simulation to run on an infinite loop. This gives you more time to evaluate how the settings are affecting the effect. In the **Emitter State** module, click the dropdown for **Life Cycle Mode** and select **Self**. Then click the dropdown for **Loop Behavior**, and select **Infinite**.
    
    Click image for full size.
    

## Particle Spawn Group Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Initialize Particle** module. This module collects several related parameters together in one module, minimizing clutter in your stack. Under **Point Attributes**, locate the **Lifetime** parameter. This parameter determines how long particles will display before they disappear. You want a little randomness in the Lifetime parameter to better simulate real smoke. Set **Lifetime Mode** to **Random**, **Lifetime Min** to **2**, and **Lifetime Max** to **3**.
    
    Click image for full size.
    
    | Property Name | Value |
    | --- | --- |
    | **Lifetime Mode** | Random |
    | **Minimum** | 2.0 |
    | **Maximum** | 3.0 |
    
3.  You are going to adjust the size of the sprite particles, to continue making the smoke effect more realistic. The original bundle of particles is rather small, so you are now going to increase the size. You will also make the size a little random, so the sprite particles overlap and make a more consistent smoke effect. Under **Sprite Attributes**, locate the **Sprite Size** parameter and make sure it is enabled. Set **Sprite Size Mode** to **Random Uniform**. Enter the following values for **Minimum** and **Maximum**.
    
    Click image for full size.
    
    | Property Name | Value |
    | --- | --- |
    | **Sprite Size Mode** | Random Uniform |
    | **Uniform Sprite Size Min** | 75 |
    | **Uniform Sprite Size Max** | 200 |
    
4.  You now have a larger mass of smoke. Now you are going to add some rotation, to add more variation to the particles' shape. Additionally, you will add randomness to the rotation to increase the variation. Set the dropdown next to **Sprite Rotation Mode** to **Direct Normalized Angle (0-1)**. This means the rotation angle is calculated as a number between 0 and 1 instead of degrees.
    
    Click image for full size.
    
5.  Now click the dropdown arrow next to **Sprite Rotation Angle**, and select **Dynamic Inputs > Random Range Float**. This adds **Minimum** and **Maximum** fields to the Normalized Angle. The particles will rotate a random number of degrees when they spawn.
    
    Click image for full size.
    
6.  Set the **Minimum** and **Maximum** values as shown below.
    
    Click image for full size.
    
    | Property Name | Value |
    | --- | --- |
    | **Minimum** | 0.25 |
    | **Maximum** | 0.5 |
    
7.  So now you have a fairly good size cloud of smoke, but it is just spinning in place. You want the smoke particles to start moving as soon as they spawn. So now you will add some initial velocity. Add the **Add Velocity** module to the Particle Spawn group by clicking the **Plus sign** (**+**) icon and selecting **Velocity > Add Velocity**.
    
    Click image for full size.
    
8.  Click the dropdown arrow next to **Velocity** and select **Dynamic Inputs > Random Range Vector**. This adds **Minimum** and **Maximum** fields to the Velocity. Again, the slight randomness adds variation and naturalness to the effect.
    
    Click image for full size.
    
9.  Set the Velocity **Minimum** and **Maximum** values as shown below.
    
    Click image for full size.
    
    | Property Name | Value |
    | --- | --- |
    | **Minimum** | X: 0, Y: 0, Z: 50 |
    | **Maximum** | X: 1, Y: 1, Z: 200 |
    
10.  Shape location controls the shape and origin of where sprites spawn. By adding a **Shape Location** module, you can have the sprites spawn in different shape primitives. Add the **Shape Location** module to the Particle Spawn group by clicking the **Plus sign** (**+**) icon and selecting **Location > Shape Location**.
    
    Click image for full size.
    
11.  Set **Shape Primitive** to **Sphere**. By indicating a radius, you can set the size of the sphere shape. Set the **Sphere Radius** to 64. Make sure the **Sphere Distribution** is set to **Random**.
    
    Click image for full size.
    
12.  The sprite material that we are using for this smoke effect uses a sprite sheet, which has multiple images that are designed to be strung together and animated. When you do not account for this, your renderer will only use the first sprite on the sheet. You can add a **SubUV Animation** module to solve this problem. Click the **Plus sign** (**+**) icon for Particle Spawn and select **Sub UV > SubUV Animation**.
    
    Click image for full size.
    
13.  In the **Sub UV Animation** module, click the dropdown for **SubUV Animation Mode** and select **Linear**. For **Start Frame** type **0**, and for **End Frame** type **63**. The sprite sheet has an 8x8 grid of images, so the total number of images is 64.
    
    Click image for full size.
    

## Particle Update Group Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to particles, and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  The velocity you added in Particle Spawn gave the particles some movement when they initially spawn. Now you want to add movement over time, and you want the smoke to rise. Now you will add movement over time, and make the smoke rise. Add the Acceleration Force module by clicking the **Plus sign** (**+**) icon for **Particle Update** and selecting **Forces > Acceleration Force**.
    
    Click image for full size.
    
3.  Leave the **X** and **Y** values set to **0**, and the **Z** value to **500**. This will give the smoke significant upward movement over time. You can adjust this setting, or even remove this module, depending on the type of smoke effect you want to create.
    
    Click image for full size.
    
4.  If you want to be able to reuse the smoke emitter in your system, you can save it as a separate asset. Click the **Gear** icon to open the **Emitter Settings** menu, and select **Create Assset From This**. The result is an independent Niagara Emitter asset.
    
    Click image for full size.
    
5.  Then click the **Save** button to apply and save the changes.  
    ![Save System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6ef8822-6eea-478b-a3c0-4b90704d87a2/31-save-file.png)
    

## End Result

Congratulations! You have created a simple smoke effect using sprites.

![Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7e8c89c-60c1-4a96-bb24-84ce4fafad87/final-sprite-effect.gif)