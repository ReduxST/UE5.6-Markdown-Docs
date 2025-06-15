# Beam Effect

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-beam-effect-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-beam-effect-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:44

---

Prerequisite Step: This how-to uses the DefaultRibbonMaterial, which is included in the content for the Niagara plugin. However, you can use the M\_Balloon material used in the [Create a Mesh Balloon Effect](/documentation/en-us/unreal-engine/how-to-use-a-solid-mesh-to-create-a-balloon-effect-in-niagara-for-unreal-engine) how-to if you have already completed that tutorial.

In Niagara, the Ribbon Renderer is used along with specific modules that indicate that the ribbon is being used as a beam. In this guide, you will learn how to create a beam that simulates lightning.

## Create System and Emitter

In Niagara, systems and emitters are independent. The current recommended workflow is to create a system from existing emitters or emitter templates.

1.  First, create a Niagara System by right-clicking in the Content Browser, and selecting **FX > Niagara System**.
    
    Click image for full size.
    
2.  Select **New system from selected emitters**. Then click **Next**.
    
    Click image for full size.
    
3.  Under **Templates**, select **Static Beam**. Click the plus sign (**+**) to add this template. Then, click **Finish**.
    
    Click image for full size.
    
4.  Name the new system **BeamSystem**. Double-click to open it in the Niagara Editor.
    
    ![Name System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b657211-c690-4e79-a2f8-d7b0f39c8a0d/04-rename-system.png "Name System")
5.  Drag your \*\*BeamSystem into your Level.
    
    Click image for full size.
    
    When you make a particle effect, it is always a good idea to drag your system into a Level. This gives you a chance to see every change and edit in context. Any changes you make to the system automatically propagate to the instance of the system in your Level.
    
6.  The emitter instance in your new system has the default name of **StaticBeam**, but you can rename it. Click the name of the emitter instance in the System Overview, and the field will become editable. Name the emitter **FX\_Beam**.
    
    Click image for full size.
    

## Change Renderer Settings

The **Render** group is last in the stack, but you need to change some things so that the effect displays the way it is supposed to.

1.  In the **System Overview**, click **Render** to open it in the **Selection** panel.
    
    Click image for full size.
    
    The emitter template in this system already has a ribbon renderer included. You will add specific modules later in this guide to indicate that the ribbon is used as a beam.
    
2.  The Material used for this renderer is the **DefaultRibbonMaterial**. If you want to use a different material, you can click the dropdown to search for and select that Material.
    
3.  If you scroll past the settings in the **Ribbon Rendering** section, you will find a section called **Tessellation**. In that section, set the **Curve Tension** to **.5**. This will affect how spikey the lightning effect is. You can raise or lower that value to vary your effect.
    
    Click image for full size.
    

## Edit the Emitter Update Group Settings

First, you will edit the modules in the **Emitter Update** group. These are behaviors that apply to the emitter, and that update each frame.

1.  In the **System Overview**, click the **Emitter Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  The **Static Beam** emitter template has the **Life Cycle Mode** set to **Self** by default. This means the life cycle and loop behavior of the emitter is set directly, instead of being handled by the System. For this effect, you will add some randomness to the **Loop Duration** by adding a float to the value. Click the dropdown arrow for **Loop Duration**, and select **Dynamic Inputs > Random Ranged Float**. This adds **Minimum** and **Maximum** fields under Loop Duration.
    
    Click image for full size.
    
3.  Set the Loop Duration Minimum and Maximum values to the following.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Minimum** | .1 |
    | **Maximum** | .2 |
    
4.  The first module that indicates this effect uses a beam is the **Beam Emitter Setup** module. Since you started with the Static Beam template, this module is already included. For **Beam Start** and **Beam End**, leave the position at its default. Check the boxes to enable **Absolute Start** and **Absolute End**.
    
    The start position of the beam is defined by the position of the Niagara system in the scene. The end position is defined by the static coordinates set in Beam End, which you can change by editing the values directly. At the end of the tutorial you will learn how to connect the end point of the beam to an actor.
    
    Click image for full size.
    
5.  To add an arc or curve to the effect, check the box to enable **Use Beam Tangents**. This displays the **Beam Start Tangent** and **Beam End Tangent** settings. Click the **Reset to Default** (small yellow arrow) icon for **Beam Start Tangent** to change the value to **Multiply Vector by Float**.
    
    Click image for full size.
    
6.  Set the Beam Start Tangent **Vector** and **Float** to the following values.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Vector** | **X**: 0, **Y**: 0, **Z**: 1 |
    | **Float** | .5 |
    |   |   |
    
7.  Set the Beam End Tangent Vector and Float to the following values.
    
    Click image for full size.
    
    | Setting | Value |
    | --- | --- |
    | **Vector** | **X**: 0, **Y**: 0, **Z**: 1 |
    | **Float** | 1 |
    |   |   |
    
8.  In the **Spawn Burst Instantaneous** module, set the **Spawn Count** to **35**.
    
    Click image for full size.
    

## Edit the Particle Spawn Group Settings

Next, you will edit the modules in the **Particle Spawn** group. These are behaviors that apply to particles when they first spawn.

1.  In the **System Overview**, click the **Particle Spawn** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  In the **Initialize Particle** module, locate the **Lifetime** parameter. This parameter determines how long particles will display before they disappear. Set the **Lifetime** to **.2**. This short Lifetime will cause the beam to flicker, which will make the lightning more realistic.
    
    Click image for full size.
    
3.  The **Spawn Beam** module is the second beam-specific module. You do not need to set anything with this module, it just needs to be present.
    
4.  The third beam-specific module is the **Beam Width** module. The Beam Width is set to **Float from Curve**. Select the **Ramp Up Down** template to apply this shape to the curve.
    
    Click image for full size.
    
5.  Below the Curve diagram you will see some additional settings. Set the **Scale Curve** to **5**.
    

## Edit the Particle Update Group Settings

Now you will edit the modules in the **Particle Update** group. These behaviors apply to an emitter's particles and update each frame.

1.  In the **System Overview**, click the **Particle Update** group to open it in the **Selection** panel.
    
    Click image for full size.
    
2.  In the **Color** module, set the **RGB** values to the following.
    
    Click image for full size.
    
3.  To break up the curve and make the beam crackle and jump like lightning, add the **Jitter Position** module by clicking the **Plus sign** (**+**) icon for **Particle Update** and selecting **Location > Jitter Position**.
    
    Click image for full size.
    
4.  To make the **Jitter Position** module work correctly, you need an Update Beam module. Add the **Update Beam** module by clicking the **Plus sign** (**+**) icon for **Particle Update** and selecting **Beam > Update Beam**. In the **System Overview**, drag the **Update Beam** module to a position above the **Jitter Position** module in the stack.
    
    Click image for full size.
    
5.  Now go back to the **Jitter Position** module. The default setting for **Jitter Amount** is **10**, and the default for **Jitter Delay** is **.25**. However, if you decrease the **Jitter Delay** to **.1** you will start to see the beam bend with an angular, jagged motion. With the value at **.1** you can still see the original arc shape under the jagged beam, which is not ideal. To fix this, you have to set the Jitter Delay to a negative number. Set the **Jitter Delay** to **\-.01**. Set the **Jitter Amount** to **15**.
    
    Click image for full size.
    

## Adjusting the Beam's End Position

You can set the Start and End positions of the beam in the **Beam Emitter Setup** module, which is in the **Emitter Update** group. By default, the end position of the beam is set to a static world location value, which you can edit manually by adjusting the value.

However, it could be useful to be able to link that end position to an actor in your scene. This way, when you want to edit the end position of the beam, you simply move that actor. One way of doing this would be to use Blueprints. Another, more simple way, would be to use a Scratch Pad to set a dynamic input.

1.  Click the **Beam Emitter Setup** module to select it in the **Selection** panel.
    
    Click image for full size.
    
2.  Click the dropdown arrow next to **Beam End**, then search for **scratch** and select **New Dynamic Scratch Input**.
    
    Click image for full size.
    
3.  This will open a scratch pad with a basic setup. It consists of an input, a Map Get that you can use to pull in some values, and an output. Right-click on the default input and select **Remove Pin** as this default input will not be needed.
    
4.  Click on the plus sign (**+**) to add a new pin. Search for **actor** and select **Make New > Actor Component Interface**. This will add a section to the **Details Panel** in the **Level Editor** when you select your Niagara object, so that you can select the object you would like to link it to.
    
    Click image for full size.
    
5.  Drag the pin from **New Actor Component Interface** and release. Select **Get Transform**. This will provide the transformation information of the object it's linked to.
    
    Click image for full size.
    
6.  Connect the Position value to the Output.
    
    Click image for full size.
    
7.  The system automatically adds a **Position -> Vector3f** node. This helps to transform vecctors to the proper format for large world coordinates. You can organize your canvas to make sure they don't overlap.
    
    Click image for full size.
    
8.  Now that the scratch is complete, in order for the changes to propogate back out into the Niagara system, you must hit **Apply**.
    
    Click image for full size.
    
9.  In the Niagara Editor, select again the **Beam Emitter Setup** module. You will notice now there is a **New Actor Component Interface** linked to the **Beam End**. Click on the dropdown arrow, then select **Make** > **Read from new User parameter**. This will create a new user parameter that you will be able to set from outside the Niagara system.
    
    Click image for full size.
    
10.  By default, the system creates a User Parameter with the name of the object and the name of the parameter, so it's quite long. If you'd like to rename this, go to the Parameters panel.
    
    Click image for full size.
    
11.  Double-click to rename **New Actor Component Interface\_Beam End** to something shorter, such as **Beam\_End**.
    
    Click image for full size.
    
12.  Save your Niagara System and close the editor to return to the **Level Editor**. You should see the beam system that you had dragged in the level earlier. You can already manipulate the start position of the beam by moving the Niagara system's start point. However the end point is fixed. What we will do next is to attach it to an object in the scene.
    
13.  First, create a basic sphere to link the end point to. From the **Create** menu, select **Shapes > Sphere**.
    
    Click image for full size.
    
14.  In the **Outliner**, select your sphere and double-click to rename it to **Sphere\_BeamEnd**.
    
    Click image for full size.
    
15.  In the **Outliner**, select your Niagara system **BeamSystem**. In the **Details** panel, scroll down to the **Override Parameters** section. Here, you should see the **Beam\_End** user parameter that you set up when you created the scratch module. Select the dropdown menu for **Source Actor**, then select **Sphere\_BeamEnd**. Alternatively, you can use the eye dropper to select any object in your level. Now, when you move that object, the beam end position moves with it.
    
    Click image for full size.
    

## End Result

Congratulations! You have created a beam effect that simulates lightning. In the video below, you can see an example of the lightning beam effect. You can use beams for all kinds of visual effects: lasers, weapon rays, tesla coils and so on.

![Beam Effect Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d12014b-dc44-43ae-83b3-55fc366761f3/beam-effect-final.gif)