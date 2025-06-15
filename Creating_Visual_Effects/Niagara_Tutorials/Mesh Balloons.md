# Mesh Balloons

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-a-solid-mesh-to-create-a-balloon-effect-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-a-solid-mesh-to-create-a-balloon-effect-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:29:24

---

Spawning a Static Mesh instead of a [camera-facing sprite](/documentation/en-us/unreal-engine/how-to-create-a-smoke-effect-using-sprite-particles-in-niagara-for-unreal-engine) can increase the realism of the effects you are creating. In the following tutorial, we will show how to set up a Niagara Emitter to spawn Static Meshes instead of sprites.

**Prerequisite Step:** This tutorial uses an imported balloon mesh. You can find free meshes online by doing a simple search. Otherwise, you can practice by using the **Shape\_Sphere** static mesh, which is found with the **Starter Content**. If you have not done so already, make sure that you have added your own mesh for the balloon to this project, or add the Starter Content to your project.

## Create a Material

The effect in this guide is meant to look like a cloud of balloons being released. To enhance this effect, you will make a simple material that makes the mesh look like a rubber balloon.

1.  Right-click in the Content Browser and under Create Basic Asset select **Material**.
    
    Click image for full size.
    
2.  Name the new Material **Balloon\_Material**. Double-click it to open in the Material Editor.
    
    Click image for full size.
    
3.  In the **Palette** panel, type `Particle` in the search bar. Select **Particle Color** and drag it into the Graph to add a Particle Color node.
    
    Click image for full size.
    
4.  Drag off the **RGB output** and connect the wire to the **Base Color** input on the **Material** node.
    
    Click image for full size.
    
5.  While holding down the **1** key, click in the Graph. This creates a **Constant** node. Copy and paste it twice, for a total of **three Constant nodes**.
    
    Click image for full size.
    
6.  Connect the output on one **Constant** node to the **Metallic** input on the **Material** node.
    
    Click image for full size.
    
7.  You can set the **Value** of a selected constant in the **Details** panel, under **Material Expression Constant**. This material is not metallic, so leave the **Metallic** constant's value at **0**.
    
    Click image for full size.
    
8.  Connect the output on the second **Constant** node to the **Specular** input on the **Material** node.
    
    Click image for full size.
    
9.  With the **Specular** constant node selected, set the Specular **Value** in the **Details** panel to **0.7**. This will give the material a slightly reflective surface.
    
    Click image for full size.
    
10.  Connect the output on the third Constant node to the **Roughness** input on the **Material** node.
    
    Click image for full size.
    
11.  With the **Roughness** constant node selected, set the Roughness **Value** in the **Details** panel to **0.2**. This will create a mostly smooth surface.
    
    Click image for full size.
    
      
    

Your final result for the Material should look like the image below.

![Material Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e050e40-df69-4bfe-b0c8-b4cbc06fa6b5/12-final-material-result.png)

## Create the System and Emitter

Niagara emitters and systems are independent. The current recommended workflow is to create a system from existing emitters or emitter templates.

1.  First, create a Niagara System by right-clicking in the Content Drawer and selecting **FX > Niagara System**. The Niagara Emitter wizard displays.
    
    Click image for full size.
    
2.  Select **New system from selected emitters**. Then click **Next**.
    
    Click image for full size.
    
3.  Under **Templates**, select **Fountain**.
    
    Click image for full size.
    
4.  Click the **Plus sign** (**+**) icon to add the emitter to the list of emitters to add to the system. Then click **Finish**.
    
    Click image for full size.
    
5.  Name the new system **Balloon\_System**. Double-click to open it in the Niagara Editor.
    
    Click image for full size.
    
6.  The emitter instance in your new system has the default name of **Fountain**, but you can rename it. Click the name of the emitter instance in the **System Overview**, and the field will become editable. Name the emitter **Balloons**.
    
    Click image for full size.
    
7.  Drag your **MeshSystem** into your Level.
    
    Click image for full size.
    
    When you make a particle effect, it is always a good idea to drag your system into a Level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your level.
    

## Change the Renderer

The Render group is last in the stack, but you need to change some things so that the effect displays the way it is supposed to. In this case, the template contains a Sprite Renderer, and this effect needs a Mesh Renderer.

1.  In the **System Overview**, click **Render** to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  To make a mesh particle effect you need a **Mesh Renderer** module, but the template has a **Sprite Renderer** module. Click the **Trashcan** icon to delete the Sprite Renderer.
    
    Click image for full size.
    
3.  Click the **Plus sign** (**+**) icon for Render and select **Mesh Renderer**.
    
    Click image for full size.
    
4.  Click the dropdown for **Particle Mesh** and select your mesh. If you imported your own balloon model, select that. Or to test, you can select **Shape\_Sphere** from the sample material.
    
    Click image for full size.
    
5.  Your mesh may be too small or too big to show up well in your level. If needed, adjust the size here. Your mesh may have a default material applied to it. By enabling Override Materials, you can use the custom material you created instead. Click to enable **Override Materials**, then click the **Plus sign** (**+**) icon to add an element to the array.
    
    Click image for full size.
    
6.  Click the dropdown for **Explicit Mat**, and select the material you created earlier, **Balloon\_Material**.
    
    Click image for full size.
    

## Edit Emitter Update Group Settings

First, you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Emitter State** module. Because you used the Fountain template, the Life Cycle Mode is set to **Self**. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate the lifecycle settings, which usually optimizes performance.
    
    Click image for full size.
    
3.  The **Spawn Rate** module creates a continuous stream of particles while the emitter is active. This module is already present in the Fountain template. Set the **Spawn Rate** to **100**.
    
    Click image for full size.
    

## Edit Particle Spawn Group Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Initialize Particle** module. This module collects several related parameters together in one module, minimizing clutter in your stack. Under **Point Attributes**, locate the **Lifetime** parameter. This parameter determines how long particles will display before they disappear. For **Lifetime Mode**, select **Random**. Set the **Minimum** and **Maximum** values to the following.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Minimum** | 2.0 |
    | **Maximum** | 4.0 |
    
3.  Locate the **Color** parameter. You can choose to have all your balloons be one solid color, or use one of the other modes to add some variety. In this example, you can set the **Color Mode** to **Random Range**. This will create your balloons in random colors that fall in a range between two set colors. Change the **RGB** values until you achieve the look you like. The colors you set here are applied to the material you created earlier. In this example, the colors are set to red and blue.
    
    Click image for full size.
    
    | Setting | Color Minimum | Color Maximum |
    | --- | --- | --- |
    | **Red** | 1.0 | 0.0 |
    | **Green** | 0.0 | 0.0 |
    | **Blue** | 0.0 | 1.0 |
    
4.  Under **Sprite Attributes**, set **Sprite Size Mode**, **Sprite Rotation Mode**, and **Sprite UV Mode** to **Unset**. Since you are using a mesh, these attributes are not needed for this effect.
    
    Click image for full size.
    
5.  When you first set your mesh, you may have resized it at that time. But you may want some variation in the size, so some balloons are larger than others. Under **Mesh Attributes**, set **Mesh Scale Mode** to **Random Uniform**. Set the **Mesh Uniform Scale Min** to **0.7** and **Mesh Uniform Scale Max** to **1.0**. If you used a sphere instead of a balloon mesh, you may want to set the **Mesh Scale Mode** to **Random Non-Uniform** to give some irregularity to the shape of your spheres.
    
    Click image for full size.
    
6.  The **Add Velocity in Cone** module is not needed for the effect you are making. You don't want the balloons to spread out in a cone shape. Click on the trash can to remove this module from your stack.
    
    Click image for full size.
    
7.  The **Add Velocity** module will give the particles movement as soon as they spawn. Add the Add Velocity module to the Particle Spawn section by clicking the **Plus sign** (**+**) icon and selecting **Add Velocity**.
    
    Click image for full size.
    
8.  Because this effect is meant to look like balloons being released, some randomness to the speed of the particles is needed. Click the downward arrow next to the **Velocity** value fields, and select **Random Range Vector**. This adds minimum and maximum velocity fields so that each balloon can be assigned a velocity value from within this range, adding randomness.
    
    Click image for full size.
    
9.  Set the Velocity **Minimum** and **Maximum** values to the following. This gives the effect a small amount of movement on the X and Y axes, and a larger amount of movement on the Z axis.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Minimum** | **X**: 15, **Y**: 25, **Z**: 50 |
    | **Maximum** | **X**: 30, **Y**: 30, **Z**: 100 |
    
10.  The **Sphere Location** module module controls the shape of the location where sprites spawn. You can have the sprites spawn in a sphere shape, and you can set the size of the sphere shape by indicating a radius. Set the **Sphere Radius** to **200**. This spreads the particles out more, as balloons would do when released.
    
    Click image for full size.
    

## Edit Particle Update Group Settings

Now you will edit the modules in the Particle Update group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Typically, you would use the **Gravity Force** module to simulate how gravity affects objects. You can also use it more generally to add acceleration to your particles. Set the Gravity Force **X, Y and Z** values to the following.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **X** | 10 |
    | **Y** | 10 |
    | **Z** | 40 |
    
3.  The **Drag** module applies drag to the particles, which slows them down. Set the **Drag** to **1.0**.
    
    Click image for full size.
    
4.  The **Scale Color** module is part of the Fountain template, but this effect does not require it. Click the **Trash can** icon to remove the Scale Color module.
    
    Click image for full size.
    

## End Result

Congratulations! You've made a mesh particle effect in Niagara. You learned how to create a material, apply the particle color to that material, and use a static mesh as your particles. Continue to explore the options in the modules to refine the effect.

![Balloon Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2d48d1f-b64a-4f6c-a8f3-e73f52f172dc/balloon-final.gif)