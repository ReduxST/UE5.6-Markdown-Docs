# Ribbon Effect

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-ribbon-effect-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-ribbon-effect-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:54

---

Prerequisite Step: This tutorial uses the DefaultRibbonMaterial, which is included in the content for the Niagara plugin. However, you can also use the M\_Balloon material you created in the [Create a Mesh Particle Effect](/documentation/en-us/unreal-engine/how-to-use-a-solid-mesh-to-create-a-balloon-effect-in-niagara-for-unreal-engine) tutorial if you have already completed it.

Simulating natural phenomena is challenging, especially when using sprite or mesh-based particles to simulate smoke or vapor trails. **Ribbon Emitters** are an excellent solution for simulating these objects. In the following tutorial, you will learn how to set up a Niagara Emitter to create a continuous ribbon-style particle effect into the world. Your end result will look like the following.

![Ribbon Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76864bb6-a382-4708-a490-48d10548ac89/ribbon-final.gif)

## Create System and Emitter

Unlike in Cascade, Niagara emitters and systems are independent. The current recommended workflow is to create a system from existing emitters or emitter templates.

1.  First, create a Niagara System by right-clicking in the Content Drawer, and selecting **FX > Niagara System**.
    
    Click image for full size.
    
2.  Select **New system from selected emitters**. Then click **Next**.
    
    Click image for full size.
    
3.  Under **Templates**, select **Simple Sprite Burst**.
    
    Using a template will place an emitter instance in your new system, and that emitter instance will have no inheritance.
    
    Click image for full size.
    
4.  Click the **Plus sign** icon (**+**) to add the selected emitter to the list of emitters to add to the system. Then click **Finish**.
    
    Click image for full size.
    
5.  Name the new system **RibbonSystem**.
    
    ![Name New System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75e77c7e-601e-4b95-9229-a1129d6b4028/05-rename-ribbon-system.png "Name New System")
6.  Drag the **RibbonSystem** into your Level. Double-click to open the system in the Niagara Editor.
    
    When you make a particle effect, it is always a good idea to drag your system into a Level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your Level.
    
7.  The emitter instance in your new system has the default name of **SimpleSpriteBurst**, but you can rename it. Click the name of the emitter instance in the **System Overview**, and the field will become editable. Name the emitter **FX\_Ribbon**.
    
    Click image for full size.
    

## Change Renderer

The **Render** group is last in the stack, but you need to change some things so that the effect displays the way it is supposed to. The original template used a Sprite Renderer, but this effect needs a Ribbon Renderer.

1.  In the **System Overview**, click **Render** to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  To make a ribbon effect, you need a **Ribbon Renderer** module. But the template has a **Sprite Renderer** module. Click the **Trashcan** icon to delete the Sprite Renderer.
    
    Click image for full size.
    
3.  Click the **Plus sign** icon (**+**) for **Render** and select **Ribbon Renderer**.
    
    Click image for full size.
    
4.  The material you want is not displayed by default. Click the dropdown for **Material**, and click **View Options** to open a list of options. Check the boxes for **Show Engine Content** and **Show Plugin Content**. Now you will be able to see the material.
    
    Click image for full size.
    
5.  Click the dropdown for **Material** and select **DefaultRibbonMaterial**.
    
    If you completed the [Create a Mesh Particle Effect](/documentation/en-us/unreal-engine/how-to-use-a-solid-mesh-to-create-a-balloon-effect-in-niagara-for-unreal-engine) tutorial, you can select the **M\_Balloon** material instead. This will give you an opaque ribbon, rather than the translucent one created by the DefaultRibbonMaterial.
    
    Click image for full size.
    

## Edit the Emitter Update Group Settings

First, you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter, and that update each frame.

Even after adding a Ribbon Renderer and editing the settings in the Emitter Update group, you will not see a ribbon appear. This is normal! When you get to the Particle Spawn section of this document, you will start to see the actual ribbon.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Expand the **Emitter State** module. This module controls time and scalability for this emitter. Because you used the **Simple Sprite Burst** template, the **Life Cycle Mode** is set to **Self**. Normally this is used for complete customization of emitter life cycle logic for this specific emitter, but it is not needed for this effect. Click the dropdown and set the **Life Cycle Mode** to **System**. This enables your system to calculate life cycle settings, which usually optimizes performance. By default, the system loops infinitely on a 5 second interval.
    
    Click image for full size.
    
3.  The **Spawn Rate** module creates a continuous stream of particles while the emitter is active. Add the **Spawn Rate** module by clicking the **Plus sign** icon (**+**) for **Emitter Update** and selecting **Spawning > Spawn Rate**.
    
    Click image for full size.
    
4.  Set the **Spawn Rate** to **100**.
    
    Click image for full size.
    

## Edit the Particle Spawn Group Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  Under **Point Attributes**, locate the **Lifetime** parameter. This parameter determines how long particles will display before they disappear. Set the **Lifetime** to **5**.
    
    Click image for full size.
    
3.  For the **Color** parameter, set it to a color of your choosing. You can do this either by typing in RGB values, or by clicking on the swatch to open a color picker.
    
    Click image for full size.
    
4.  Set the **Mass** parameter to **10**. This will affect how the ribbon spreads outward, as well as how quickly it falls.
    
    Click image for full size.
    
5.  Under **Ribbon Attributes**, set the **Ribbon Width** to **10**.
    
    Click image for full size.
    
6.  To make the ribbon spin in a spiral, you can add a **Shape Location** module. Location modules affect the shape of the location where the particles spawn. Click the **Plus sign** icon (**+**) for **Particle Spawn** and select **Location > Shape Location**.
    
    Click image for full size.
    
7.  Under **Shape**, click the dropdown for **Shape Primitive** and select **Ring / Disk**.
    
    Click image for full size.
    
8.  Set the **Ring Radius** to **50**. The Ring Radius determines how large the primary ring shape is.
    
    Click image for full size.
    
9.  Under **Distribution**, click the dropdown for **Ring Distribution Mode** and select **Direct**.
    
    Click image for full size.
    
10.  Now you will add some velocity to the ribbon. Click the **Plus sign** icon (**+**) for **Particle Spawn** and select **Velocity > Add Velocity**.
    
    Click image for full size.
    
11.  Click the dropdown to **Velocity Mode** and select **From Point**.
    
    Click image for full size.
    
12.  Set the **Velocity Speed** to **50**. Now you will see the ribbon start to spiral! This happens because as the position is moving around the Large Radius, the velocity pushes the ribbon outward from the original ring.
    
    Click image for full size.
    

## Edit the Particle Update Group Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  This effect has a single color, so the **Scale Color** module is not needed. Click the **Trashcan** icon to delete it.
    
    Click image for full size.
    
3.  Add the **Acceleration Force** module. This is what makes the spiraling ribbon fall down, simulating gravity. Click the **Plus sign** icon (**+**) for **Particle Update** and select **Forces > Acceleration Force**.
    
    Click image for full size.
    
4.  Set the **Z** value of the **Acceleration** to **\-200**. A positive Z value would make the ribbon spiral upwards; using a negative value makes it drop downward in a parabolic shape.
    
    Click image for full size.
    

## End Result

Congratulations! You have created a Niagara ribbon effect.

![Ribbon Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29663a4b-ee7a-499d-a3bb-0344525dc38e/ribbon-final.gif)