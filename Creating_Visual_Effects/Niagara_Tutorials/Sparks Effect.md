# Sparks Effect

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-sparks-effect-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-sparks-effect-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:57

---

**Prerequisite Steps:**

This tutorial uses the **M\_smoke\_subUV**, **M\_Spark**, and **M\_Radial\_Gradient** materials, which can be found with the Starter Content. If you have not done so already, make sure that your project includes the Starter Content. This tutorial also uses the FX\_Smoke emitter created in the how-to [Create a Sprite Particle Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine).

To create the Sparks effect included in the Starter Content, you will need to make three Niagara emitters: one for the fountain of sparks, one for the spark at the center, and one for the small stream of smoke rising from the fountain of sparks.

The final effect will look like the following.

![Sparks Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97c48336-0fda-427a-b0cb-500f32cdd9a7/sparks-final.gif)

You will start with the smoke emitter, because you can create it using a copy of an existing emitter.

## Create the Smoke Emitter and the Sparks System

Niagara emitters and systems are independent. The current recommended workflow is to create a system from existing emitters or emitter templates.

1.  Create a new folder for this tutorial in the Content folder for your project.
    
2.  Make a copy of the **FX\_Smoke** emitter you created in [Create a Sprite Particle Effect in Niagara](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine).
    
    Click image for full size.
    
3.  Drag this duplicate emitter to the folder you created in step 1. In the popup context menu, select **Move**.
    
4.  Rename the copied emitter **FX\_Sparks\_Smoke**.
    
    ![Rename Emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3c38527-23ab-40a7-9b90-638363cfb35c/02-rename-smoke-emitter.png)
5.  Now create a system for your spark effect. Right-click on your new smoke emitter, and select **Create Niagara System**.
    
    Click image for full size.
    
    There are multiple ways to create new Niagara systems. Because you are starting with an emitter you have already created, the method used here quickly creates a system containing that emitter. However, as you saw in the Create a Sprite Particle Effect tutorial, there are emitter and system wizards that give you many other options for creating and setting up a Niagara system.
    
6.  Name the system **SparksSystem**.
    
    ![Name System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/156d8a14-5d21-4494-8f7e-4512994a569e/04-rename-system.png "Name System")
7.  Open your Level in the Level Editor, if it isn't open already. Drag the **SparksSystem** tile from the **Content Drawer** into your Level.
    
    When you make a particle effect, it is always a good idea to drag your system into your level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your level.
    
    Click image for full size.
    

### Smoke Emitter - Edit the Emitter Update Settings

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Emitter State** module. This module controls time and scalability for this emitter. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate life cycle settings, which usually optimizes performance. By default, the system loops infinitely on a 5 second interval.
    
    Click image for full size.
    
3.  Open the **Spawn Rate** module. Change the **Spawn Rate** setting to **20**.
    
    Click image for full size.
    

### Smoke Emitter - Edit the Particle Spawn Settings

Next, you will edit the modules in the Particle Spawn group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Initialize Particle** module. Under **Point Attributes**, expand **Lifetime**. Change the **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Lifetime Mode** | Random |
    | **Minimum** | 2.0 |
    | **Maximum** | 3.0 |
    
3.  Locate the **Color** parameter. Change the **RGB** values to the following.
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Red** | 0.3 |
    | **Green** | 0.3 |
    | **Blue** | 0.3 |
    
4.  Under **Sprite Attributes**, expand **Sprite Size**. Set the Sprite Size Mode to **Non-Uniform**. Set the **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Sprite Size Mode** | Random Uniform |
    | **Minimum** | 20.0 |
    | **Maximum** | 40.0 |
    
5.  Open the **Add Velocity** module. Change the Velocity **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Velocity | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | 0.0 | 1.0 |
    | **Y** | 0.0 | 1.0 |
    | **Z** | 25.0 | 35.0 |
    
6.  Open the **Shape Location** module. Change the **Sphere Radius** value to **5**.
    
    Click image for full size.
    

### Smoke Emitter - Edit the Particle Update Settings

Now you will edit the modules in the Particle Update group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Scale Color** module. Click to deselect the box next to **Scale RGB**. Above the curve for **Scale Alpha**, click the **Smooth Ramp Down** template to apply that shape to the curve.
    
    Click image for full size.
    
3.  Open the **Acceleration Force** module. Set the **Acceleration** values to **X: 0, Y: 0, Z: 20**.
    
    Click image for full size.
    

At this stage in the process, you have finished configuring the first emitter in the system. It should look similar to the following.

![Sparks Effect First Emitter Configured](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67c1748f-aefe-452a-81e0-b71823715883/sparks-stage-1.gif)

## Add the Spark Burst Emitter to the System

Next, you will create the spark burst at the center of the effect.

1.  Right-click in the **System Overview** of your SparkFountain system. Click **Add Emitter**, and a list of existing emitters will display. From the list of emitters, select the **Simple Sprite Burst** template.
    
    Click image for full size.
    
2.  The default name for the template emitter is **SimpleSpriteBurst**, but you can rename it. Click on the emitter name, and the field becomes editable. Name the new emitter **FX\_SparkBurst**.
    
    Click image for full size.
    

### Spark Burst Emitter - Edit Render Settings

The **Render** group is last in the stack, but you need to change the material so that the effect displays the way it is supposed to.

1.  In the **System Overview**, click the **Render** group to open it in the **Selection** pane.
    
    Click image for full size.
    
2.  Under **Sprite Renderer**, click the dropdown for **Material**, and select the **M\_Spark** material from the Starter Content.
    
    Click image for full size.
    

### Spark Burst Emitter - Edit the Emitter Update Settings

First, you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Remove the **Sprite Burst Instantaneous** module by clicking the **Trashcan** icon.
    
    Click image for full size.
    
3.  Open the **Emitter State** module. This module controls time and scalability for this emitter. Because you used the Simple Sprite Burst template, the **Life Cycle Mode** is set to Self. Normally this is used for complete customization of emitter life cycle logic for this specific emitter, but it is not needed for this effect. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate life cycle settings, which usually optimizes performance. By default, the system loops infinitely on a 5 second interval.
    
    Click image for full size.
    
4.  Click the **Plus sign** (**+**) for Emitter Update, and select **Spawning > Spawn Rate**.
    
    Click image for full size.
    
5.  Open the **Spawn Rate** module. Set the **Spawn Rate** to **50**.
    
    Click image for full size.
    

### Spark Burst Emitter - Edit the Particle Spawn Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Under **Point Attributes**, set the **Lifetime** to **.2**.
    
    Click image for full size.
    
3.  Set the **Mass Mode** to **Random** and the **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Mass Mode** | Random |
    | **Minimum** | 0.6 |
    | **Maximum** | 1.0 |
    
4.  Under **Sprite Attributes**, expand **Sprite Size**. Set the **Sprite Size Mode** to **Random Non-Uniform**. Set the Sprite Size **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Sprite Size | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | 10.0 | 30.0 |
    | **Y** | 10.0 | 25.0 |
    
5.  Click the box next to **Sprite Rotation** to enable it. Set the **Sprite Rotation Mode** to **Direct Angle (Degrees)**. Click the dropdown next to the Value field, and select **Dynamic Inputs > Random Range Float**.
    
    Click image for full size.
    
6.  Set the **Minimum** and **Maximum** to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Minimum** | \-10.0 |
    | **Maximum** | 30.0 |
    
7.  Click the **Plus sign** (**+**) for Particle Spawn, and select **Velocity > Add Velocity**.
    
    Click image for full size.
    
8.  Open the **Add Velocity** module. Click the dropdown next to the value, and select **Dynamic Inputs > Random Range Vector**.
    
    Click image for full size.
    
9.  Set the Velocity **Minimum** and **Maximum** to the following:
    
    Click image for full size.
    
    | Velocity | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | 0.0 | 5.0 |
    | **Y** | 0.0 | 5.0 |
    | **Z** | 0.0 | 5.0 |
    
10.  Click the **Plus sign** (**+**) for Particle Spawn, and select **Location > Shape Location**.
    
    Click image for full size.
    
11.  Open the **Shape Location** module. Set the **Sphere Radius** to **5**.
    
    Click image for full size.
    

### Spark Burst Emitter - Edit the Particle Update Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Scale Color** module. For **Scale RGB**, set the **RGB** values to the following. Under **Scale Alpha**, select the **Smooth Ramp Down** template.
    
    Click image for full size.
    
    | Color | Value |
    | --- | --- |
    | **R** | 2.0 |
    | **G** | 6.0 |
    | **B** | 25.0 |
    
3.  Click the **Plus sign** icon (**+**) for **Particle Update**, and select **Size > Scale Sprite Size**. You can also type `scale` in the search bar, as shown below.
    
    Click image for full size.
    
4.  Open the **Scale Sprite Size** module. Click the dropdown next to the **Scale Factor** value field, and select **Dynamic Inputs > Random Range Vector 2D**. You can also type `random` in the search bar.
    
    Click image for full size.
    
5.  Set the Scale Factor **Minimum** and **Maximum** to the following:
    
    Click image for full size.
    
    | Scale | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | 1.0 | 3.5 |
    | **Y** | 2.5 | 5.0 |
    

At this stage in the process, you have finished configuring the second emitter in the system. It should look similar to the following.

![Sparks Effect Second Emitter Configured](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c155889-beba-4138-b283-d21a2b3974c9/sparks-stage-2.gif)

## Add the Radial Sparks Emitter to the System

1.  Right-click in the **System Overview** of your SparkFountain system. Click **Add Emitter**, and a list of existing emitters will display. From the list of emitters, select the **Simple Sprite Burst** template.
    
    Click image for full size.
    
2.  The default name for the template emitter is **SimpleSpriteBurst**, but you can rename it. Click on the emitter name, and the field becomes editable. Name the new emitter **FX\_Sparks\_Radial**.
    
    Click image for full size.
    

### Radial Sparks Emitter - Edit Render Settings

The **Render** group is last in the stack, but you need to change the material so that the effect displays the way it is supposed to.

1.  In the **System Overview**, click the **Render** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Click the dropdown for **Material**, and select the **M\_Radial\_Gradient** material from the Starter Content. To locate it, type `radial` in the search bar, as shown below.
    
    Click image for full size.
    
3.  Click the dropdown for **Alignment** and select **Velocity Aligned**.
    
    Click image for full size.
    

### Radial Sparks Emitter - Edit the Emitter Update Settings

First, you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Remove the **Sprite Burst Instantaneous** module by clicking the **Trashcan** icon.
    
    Click image for full size.
    
3.  Open the **Emitter State** module. This module controls time and scalability for this emitter. Because you used the **Simple Sprite Burst** template, the **Life Cycle Mode** is set to **Self**. Normally this is used for complete customization of emitter life cycle logic for this specific emitter, but it is not needed for this effect. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate life cycle settings, which usually optimizes performance. By default, the system loops infinitely on a 5 second interval.
    
    Click image for full size.
    
4.  Click the **Plus sign** icon (**+**) for **Emitter Update**, and select **Spawning > Spawn Rate**.
    
    Click image for full size.
    
5.  Open the **Spawn Rate** module. Set the **Spawn Rate** to **500**.
    
    Click image for full size.
    

### Radial Sparks Emitter - Edit Particle Spawn Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Open the **Initialize Particle** module. Under **Point Attributes**, expand **Lifetime**. Set the Lifetime Mode to **Random** and the **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Lifetime Mode** | Random |
    | **Minimum** | 0.2 |
    | **Maximum** | 0.7 |
    
3.  Expand **Color**. Set the **Color Mode** to **Direct Set** and the RGB values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Red** | 2.0 |
    | **Green** | 8.0 |
    | **Blue** | 20.0 |
    | **Alpha** | 1.0 |
    
4.  Expand **Mass**. Set the **Mass Mode** to **Random** and the **Minimum** and **Maximum** values to the following:
    
    Click image for full size.
    
    | Parameter | Value |
    | --- | --- |
    | **Mass Mode** | Random |
    | **Minimum** | 0.3 |
    | **Maximum** | 0.6 |
    
5.  Under **Sprite Attributes**, set the **Sprite Size Mode** to **Non-Uniform**. Set the following values: **X: 0.25, Y: 0.5**.
    
    Click image for full size.
    
6.  Leave the **Sprite Rotation Mode** and **Sprite UV Mode** as **Unset**.
    
7.  Click the **Plus sign** icon (**+**) for **Particle Spawn**, and select **Mass > Calculate Size and Rotational Inertia by Mass**. You can also type `calc` in the Search bar, as shown below.
    
    Click image for full size.
    
8.  Open the **Calculate Size and Rotational Inertia by Mass** module. Under **Density**, set **Density by Material Type** to **Water**.
    
    Click image for full size.
    
9.  Under **Proportions**, change the **Height** to **0.5** and **Depth** to **0.0**.
    
    Click image for full size.
    
10.  Click the **Plus sign** icon (**+**) for **Particle Spawn**, and select **Velocity > Add Velocity**. You can also type `velocity` in the Search bar.
    
    Click image for full size.
    
11.  Open the **Add Velocity** module. Click on the dropdown menu and select **Dynamic Inputs** then **Random Range Vector**.
    
    Click image for full size.
    
12.  Set the Velocity **Minimum** and **Maximum** to the following.
    
    Click image for full size.
    
    | Velocity | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | \-100.0 | 90.0 |
    | **Y** | \-100.0 | 90.0 |
    | **Z** | 300.0 | 500.0 |
    
13.  Click the **Plus sign** icon (**+**) for **Particle Spawn**, and select **Location > Shape Location**. You can also type `sphere` in the Search bar.
    
    Click image for full size.
    
14.  Open the **Shape Location** module. Set the **Sphere Radius** to **2.0**.
    
    Click image for full size.
    

### Radial Sparks Emitter - Edit the Particle Update Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Click the **Plus sign** icon (+) for **Particle Update**, and select **Velocity > Scale Velocity**.
    
    Click image for full size.
    
3.  Set the **Scale Velocity** to **X: 3.0, Y: 4.0, Z: 1.0**.
    
    Click image for full size.
    
4.  Click the **Plus sign** icon (**+**) for **Particle Update**, and select **Forces > Gravity Force**.
    
    Click image for full size.
    
5.  Open the **Gravity Force** module. Change the **Z** value to **\-4500**.
    
    Click image for full size.
    
6.  Click the **Plus sign** icon (**+**) for **Particle Update**, and select **Forces > Drag**.
    
    Click image for full size.
    
7.  Open the **Drag** module. Set the **Drag** value to **1.7**.
    
    Click image for full size.
    
8.  Click the **Plus sign** (**+**) for **Particle Update** and select **Collision > Collision**. This module will make sure any sparks that hit something like a floor will collide and bounce back.
    
    Click image for full size.
    
9.  Open the **Collision** module. Under **Bounce**, set the **Restitution** value to **0.4**.
    
    Click image for full size.
    
10.  Under **Friction**, set the **Friction** value to **0.2**.
    
    Click image for full size.
    
11.  Remove the **Scale Color** module by clicking the **Trashcan** icon.
    
    Click image for full size.
    
12.  Click the **Plus sign** (**+**) and select **Size > Scale Sprite Size by Speed**.
    
    Click image for full size.
    
13.  Open the **Sprite Size Scale by Speed** module. Set the **Scale Factor** Minimum and Maximum to the following.
    
    Click image for full size.
    
    | Sprite Size Scale by Speed | Minimum | Maximum |
    | --- | --- | --- |
    | **X** | 0 | 0.5 |
    | **Y** | 3 | 6 |
    
14.  Set the **Velocity Threshold** value to **2000**.
    
    Click image for full size.
    

## End Result

Congratulations! After following these steps, the Sparks effect is complete. You can check the final results back in your level, and make any adjustments you like to fine-tune it.

![Sparks Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b632ead6-8f82-4cb4-9f09-e45fa7469010/sparks-final.gif)