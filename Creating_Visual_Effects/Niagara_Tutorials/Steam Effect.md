# Steam Effect

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-steam-effect-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-steam-effect-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:58

---

**Prerequisite Steps:**

This How-To uses the M\_smoke\_subUV Material, which can be found with the Starter Content. If you have not done so already, make sure that your project includes the Starter Content. This how-to also uses the FX\_Smoke emitter created in [Create a Sprite Particle Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine).

## Create the Steam Emitter and System

Niagara emitters and systems are independent. The current recommended workflow is to create a system from existing emitters or emitter templates. However, since you are duplicating an existing emitter, the process will be slightly different.

1.  Create a new folder for this How-To in the **Content** folder for your project.
2.  Locate the FX\_Smoke emitter you saved when working through [Create a Sprite Particle Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-beam-effect-in-niagara-for-unreal-engine). Right-click on the emitter, and select **Duplicate Emitter**.
    
    Click image for full size.
    
3.  Drag this duplicate emitter to the folder you created in step 1. In the popup context menu, select **Move**.
4.  Rename the copied emitter **FX\_Steam**.
    
    ![Rename Emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f4c4c21-be74-435b-9f25-a7c7785ddeed/ue5_02-rename-emitter.png "Rename Emitter")
5.  Now create a system for your steam effect. Right-click on your new steam emitter, and select **Create Niagara System**.
    
    Click image for full size.
    
    There are multiple ways to create new Niagara systems. Because you are starting with an emitter you have already created, the method used here quickly creates a system containing that emitter. However, as you saw in the Create a Sprite Particle Effect how-to, there are emitter and system wizards that give you many other options for creating and setting up a Niagara system.
    
6.  Name the system **Steam**.
    
    ![Name System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60c11b39-58f9-4dc7-8182-2df7a288ab4d/ue5_04-name-system.png "Name System")
7.  Open your Level in the Level Editor, if it isn't open already. Drag the Steam system into your level.
    
    Click image for full size.
    
      
    
    When you make a particle effect, it is always a good idea to drag your system into your level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your level.
    

## Edit the Emitter Update Settings

First you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter itself, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Emitter State** module.This module controls time and scalability for this emitter. Because you used the Simple Sprite Burst template, the **Life Cycle Mode** is set to **Self**. Normally this is used for complete customization of emitter life cycle logic for this specific emitter, but it is not needed for this effect. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate life cycle settings, which usually optimizes performance. By default, the system loops infinitely on a 5 second interval.
    
    Click image for full size.
    
3.  Expand the **Spawn Rate** module. Change the **Spawn Rate** setting to **30**.
    
    Click image for full size.
    

## Edit the Particle Spawn Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Initialize Particle** module. Under **Point Attributes**, expand **Lifetime**. Change the Minimum and Maximum values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Minimum** | 3.0 |
    | **Maximum** | 7.0 |
    |   |   |
    
3.  Expand **Color**. Change the **RGB** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Red** | 1.0 |
    | **Green** | 1.0 |
    | **Blue** | 1.0 |
    |   |   |
    
4.  Under **Sprite Attributes**, expand **Sprite Size**. Change the **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Minimum** | 100 |
    | **Maximum** | 200 |
    |   |   |
    
5.  Open the **Add Velocity** module. Change the Velocity **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Minimum** | X: 16, Y: -5.0, Z: 35 |
    | **Maximum** | X: 32, Y: 5.0, Z: 50 |
    |   |   |
    
6.  Open the **Sphere Location** module. Change the **Sphere Radius** value to **20**.
    
    Click image for full size.
    

## Edit the Particle Update Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Acceleration Force** module. Set the Acceleration **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Minimum** | X: 25, Y: -10.0, Z: 15 |
    | **Maximum** | X: 55, Y: 10.0, Z: 25 |
    |   |   |
    
3.  Open the **Scale Color** module. Click on the **Pulse Out** curve template to apply that shape to the curve.
    
    Click image for full size.
    
4.  Just click on the template that matches that curve.
    
    Click image for full size.
    
5.  Click the **Plus sign** icon (**+**) in the **Particle Update** group, and select **Forces > Drag** to add the **Drag** module.
    
    Click image for full size.
    
6.  Because Niagara adds new modules to the bottom of the group's stack, you will get an error stating "The module has unmet dependencies." That is because the Drag module was placed after the **Solve Forces and Velocity** module. Click the **Fix Issue** button to move the module and resolve the error.
    
    Click image for full size.
    
7.  Set the **Drag** to **.8**.
    
    Click image for full size.
    

## End Result

After following these steps, the Steam system in your level will produce a steam effect similar to the one in the image below.