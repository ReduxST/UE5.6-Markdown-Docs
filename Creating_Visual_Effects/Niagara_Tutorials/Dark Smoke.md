# Dark Smoke

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-dark-smoke-effect-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-dark-smoke-effect-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:49

---

You created a basic sprite effect by completing the [Create a Sprite Smoke Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine) tutorial. In this tutorial, learn how to duplicate an emitter, create a Niagara system from a pre-existing emitter, and make further adjustments to change the look of the smoke.

**Prerequisite Steps:**

This how-to uses the **M\_smoke\_subUV** Material, which can be found with the Starter Content. If you have not done so already, make sure that your project includes the Starter Content. This how-to also uses the **FX\_Smoke** emitter created in the tutorial [Create a Sprite Smoke Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine).

## Create System and Emitter

You can create a Niagara system from scratch by right-clicking in the Content Drawer as has been done in previous tutorials. However, if you already have a saved emitter to use as a starting point, it's also possible to duplicate it and start from there.

1.  Create a new folder for this tutorial in the Content folder for your project.
    
2.  Make a copy of the **FX\_Smoke** emitter you created in [Create a Sprite Particle Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine).
    
    Click image for full size.
    
3.  Drag this duplicate emitter to the folder you created in step 1. In the popup context menu, select **Move**.
    
4.  Rename the copied emitter **FX\_DarkSmoke**. This distinguishes it from the smoke effect created in the [Create a Sprite Smoke Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine) tutorial.
    
    ![Rename the Duplicate Emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b867fab-71dd-4eeb-86ed-78078b238a06/02-rename-emitter.png "Rename the Duplicate Emitter")
5.  Right-click on your new smoke emitter, and select **Create Niagara System**.
    
    There are multiple ways to create new Niagara systems. Because you are starting with an emitter you have already created, the method used here quickly creates a system containing that emitter.
    
6.  Name the system **DarkSmoke**. This is to distinguish it from the smoke effect created in the [Create a Sprite Smoke Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine) tutorial.
    
    ![Rename System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad310be5-9a74-44e3-8cb8-03f6c6ced461/04-dark-smoke-system.png "Rename System")
7.  Drag the DarkSmoke system from the **Content Drawer** into your Level, so you can preview the changes in the context of your project's world.
    
    Click image for full size.
    
    When you make a particle effect, it is always a good idea to drag your system into your Level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your Level.
    
8.  Double-click the **FX\_DarkSmoke** emitter to open it in the Niagara Editor. After you have edited the settings in the emitter, you will need to save the DarkSmoke system also.
    

## Edit the Emitter Update Settings

First you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter itself, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Emitter State** module. This module controls time and scalability for this emitter. Because you used the Simple Sprite Burst template, the **Life Cycle Mode** is set to **Self**.
    
    Normally this is used for complete customization of emitter life cycle logic for this specific emitter, but it is not needed for this effect. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate life cycle settings, which usually optimizes performance. By default, the system loops infinitely on a 5 second interval.
    
    Click image for full size.
    
3.  Open the **Spawn Rate** module. Set the **Spawn Rate** to **25**.
    
    Click image for full size.
    

## Edit the Particle Spawn Settings

Next, you will edit the modules in the Particle Spawn group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Initialize Particle** module. Under **Point Attributes**, expand **Lifetime**. The Lifetime parameter determines how long particles will display before they disappear. Change the **Lifetime Mode**, **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Lifetime Mode** | Random |
    | **Minimum** | 3.0 |
    | **Maximum** | 5.0 |
    
3.  Expand **Color**. You can set the smoke to a single color, or change the **Color Mode** to **Random Range** to get some variability in the color of each particle. Change the RGB values to the following:
    
    Click image for full size.
    
    | Color | Minimum | Maximum |
    | --- | --- | --- |
    | **Red** | 0.5 | 0.205 |
    | **Green** | 0.5 | 0.205 |
    | **Blue** | 0.5 | 0.205 |
    
4.  Under **Sprite Attributes**, expand **Sprite Size**. Make sure **Sprite Size Mode** is set to **Random Uniform**, which gives minimum and maximum values. New particles will be created at a random size between these values. Change the **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Minimum** | 50 |
    | **Maximum** | 90 |
    
5.  Open the **Add Velocity** module. In the previous tutorial, we had set the Velocity to Random Range Vector. This adds Minimum and Maximum values. Each new particle that is created has a random value between these two ranges set for its initial velocity. Change the **Velocity** Minimum and Maximum values to the following:
    
    Click image for full size.
    
    | Value | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | 12 | 32 |
    | **Y** | 0 | 0 |
    | **Z** | 5 | 7 |
    
6.  Open the **Sphere Location** module. New particles are generated within the sphere when they are first created. Change the **Sphere Radius** value to **30**.
    
    Click image for full size.
    

## Edit the Particle Update Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Acceleration Force** module. Set the Acceleration **Z** value to **20**.
    
    Click image for full size.
    
3.  Open the **Scale Color** module. Make sure the **Scale Mode** is set to **RGB and Alpha Separately**. You only want to adjust the alpha values so that the color fades in and then pulses out as the particle ages. **Scale Alpha** should be set to **Float from Curve**. Click on the **Pulse** template in the curve editor to quickly apply this shape to the curve.
    
    Click image for full size.
    

## End Result

After following these steps, the Smoke system in your level will produce a smoke effect similar to the one in the image below.

![Dark Smoke Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9200e9f7-1127-4df7-9431-973296185d5f/dark-smoke-final.gif)