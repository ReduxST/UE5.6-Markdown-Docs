# Particle Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-particle-effects-that-emit-light-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-particle-effects-that-emit-light-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:29:02

---

When you give particles the ability to illuminate the world around them, it can add an extra layer of realism to any of your project's visual effects. In the following tutorial, we will take a look at setting up a Niagara emitter so that particles and lights are spawned at the same time. The final result of this tutorial will look like the following.

![Particle Lights Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3decd016-6167-4dfd-9b4f-e04ab3458a41/particle-lights-final.gif)

**Prerequisite step**: This tutorial uses the **M\_Radial\_Gradient** Material, which is found with the **Starter Content**. You should create a new project that includes the Starter Content, or use a project that was created with Starter Content included.

## Create the System and Emitter

Niagara emitters and systems are independent. The current recommended workflow is to create a system from existing emitters or emitter templates.

1.  First, create a Niagara System by right-clicking in the Content Browser, and from the displayed menu select **FX > Niagara System**. The Niagara Emitter wizard displays.
    
    Click image for full size.
    
2.  Select **New system from selected emitters**, then click **Next**.
    
    Click image for full size.
    
3.  Under **Templates**, select **Fountain**.
    
    Click image for full size.
    
4.  Click the **Plus sign** (**+**) icon to add the emitter to the list of emitters to add to the system, then click **Finish**.
    
    Click image for full size.
    
5.  Name the new system **ParticleLights**. Double-click to open it in the Niagara Editor.
    
    ![Name System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b54fc0e2-057b-4704-9b4f-4caf960796c7/05-rename-niagara-system.png "Name System")
6.  The emitter instance in your new system has the default name of **Fountain**. You can rename it, however. Click the name of the emitter instance in the **System Overview**, and the field will become editable. Name the emitter **FX\_ParticleLight**.
    
    Click image for full size.
    
7.  Drag your **ParticleLight** system into your Level.
    

When you make a particle effect, it is always a good idea to drag your system into a Level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your level.

## Edit the Emitter Update Group Settings

First, you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Emitter State** module. Because you used the Fountain template, the Life Cycle Mode is set to Self. Click the dropdown and set the Life Cycle Mode to System. This enables your system to calculate the lifecycle settings, which usually optimizes performance.
    
    Click image for full size.
    
3.  The **Spawn Rate** module creates a continuous stream of particles while the emitter is active. This module is already present in the Fountain template. Set the **Spawn Rate** to **500**.
    
    Click image for full size.
    

## Edit the Particle Spawn Group Settings

Next, you will edit the modules in the Particle Spawn group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Initialize Particle** module. This module collects several related parameters together in one module, minimizing clutter in your stack. Under **Point Attributes**, locate the **Lifetime Mode** dropdown and set to **Random**. This parameter determines how long particles will display before they disappear. For this effect, you will use a dynamic input called **Random Ranged Float** to randomize how long the particles display. Random Ranged Float is already applied to the Lifetime parameter in the Fountain template. Set the **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Lifetime Mode** | Random |
    | **Minimum** | 1.75 |
    | **Maximum** | 2.5 |
    
3.  Also under **Point Attributes**, locate the **Color** parameter. This sets the initial color of the particles when they spawn. Set the **RGB** fields to the following values.
    
    The Unreal Engine Color Picker normalizes RGB color values to an integer between 0 and 1. However if you set a color value greater than 1, it becomes emissive color. The particles will glow that color when the system is placed in the Level.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Red** | 0.1 |
    | **Green** | 0.3 |
    | **Blue** | 50 |
    
4.  Under **Sprite Attributes**, locate the **Sprite Size** parameter. To add some randomness to the size of the fountain particles, adjust the Sprite Size Mode. Click on the dropdown menu and select Random Uniform. This adds **Minimum** and **Maximum** fields to the Value. Set the **Sprite Size** **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Sprite Size Mode** | Random Uniform |
    | **Minimum** | 2.5 |
    | **Maximum** | 8.0 |
    
5.  **Sphere location** controls the shape and origin of where sprites spawn. You can set the size of the sphere shape by indicating a radius. The **Sphere Location** module is included in the Fountain template. Set the **Sphere Radius** to **15**.
    
    Click image for full size.
    
6.  The Fountain template also contains the **Add Velocity in Cone** module. This adds movement to the particles when they spawn. The point of the cone is at the particle spawn point, and you can set **X**, **Y**, and **Z** values to determine in which direction the cone expands. The **Velocity Strength** has a dynamic input called **Random Ranged Float** applied. Set the **Minimum** and **Maximum** values to the following. Leave the other settings at their default values.
    
      
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Minimum** | 300 |
    | **Maximum** | 600 |
    

## Edit the Particle Update Group Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  The **Gravity Force** module simulates how gravity affects objects. The **Drag** module applies drag to the particles, which slows them down. The default settings for Gravity Force and Drag work for this effect, so you can leave them that way.
    
3.  Without setting up collision, the particles in your effect will just fall through the floor or any other solid objects in the level. To add a **Collision** module, click the **Plus sign** (**+**) icon for **Particle Update** and select **Collision > Collision**.
    
    Click image for full size.
    
4.  The **Collision** module is inserted at the bottom of the stack, after the **Solve Forces and Velocity** module. This causes an error. Click **Fix Issue** to move the Collision module and resolve the error.
    
    Click image for full size.
    
5.  Leave the default settings for the **Collision** module in place.
    

## Add the Light Renderer

Now you will add the Light Renderer to the fountain effect.

1.  In the **System Overview**, click the **Render** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Click the **Plus sign** (**+**) icon for **Render**, and select **Light Renderer**.
    
    Click image for full size.
    
3.  Set the **Radius Scale** to **5.0**. This determines how far from the particle spawn point the light spreads.
    
    Click image for full size.
    
4.  The **Color Add** values enable you to change the color of the light emitted by the effect. These values are labeled with **X**, **Y**, and **Z**; however they correspond to RGB values, with **X=Red**, **Y=Green**, and **Z=Blue**. To match the light color with the particle color, set the values to the following.
    
    | Setting | Value |
    | --- | --- |
    | **Red** | 0 |
    | **Green** | 0 |
    | **Blue** | 15 |
    

## End Result

Congratulations! You have created an effect that includes a particle light, and that emits light in your scene.

![Particle Lights Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c359195-4e0b-44f8-9898-bd354bb2462b/particle-lights-final.gif)