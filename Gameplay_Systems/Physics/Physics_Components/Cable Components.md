# Cable Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cable-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cable-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:44

---

Having the ability to cheaply add cables, ropes, or chains that can sway back and forth as if being gently blown by the wind can add a nice bit of life to your Unreal Engine projects. In the following document, we will look at how you can use the **Cable Component** plugin to create, set up, and control how the cables look, react and even collide with objects in your levels.

## Simulation and Rendering

To perform the actual cable simulation, a technique called **Verlet Integration**, which is well known in game development. The idea is to represent the cable as a series of particles, with **distance constraints** between them. The particles at the ends are **fixed**, moving with whatever they are attached to. The ones in the middle are **free**, falling with gravity. For each step, you update the velocity and position of each particle, and then move them to satisfy the constraints. The **stiffness** of the cable is controlled by the number of times we iterate to enforce the constraints (each step).

Click image for full size.

Now that there is a nice chain of connected particles bouncing around, they need to be rendered. To render a cable, a class called **FCableSceneProxy** was created to represent the render of the cable. Each end of the Sim particles' positions (done on the main thread, inside of TickComponent) is then passed to this proxy via the **SendRenderDynamicData\_Concurrent** function. Next, update is locked on the render thread, and then the index and vertex buffers are updated, making a **tube** mesh. For each vertex on this tube mesh, we need to calculate a position, a Texture UV, and three Tangent Basis vectors. When doing this, **X** will point along the cable, **Z** will point straight out from the cable (the normal) and **Y** is perpendicular to **X** and **Z**. These properties have been exposed to the components, giving you the ability to control the number of sides, the radius of the tube, and how many times the UVs can tile along the cable.

Click image for full size.

## Enabling the Plugin

By default, the Cable Component plugin should be enabled. However, if it is not, you can enable it by first going to the main toolbar and selecting **Edit** > **Plugins**. Then, from the plugins list, go to **Rendering** and make sure the **Cable Component** has a checkmark in the box next to **Enabled**.

Click image for full size.

## Using the Cable Component

In the following section, we will go over the two different ways that you can add cables to your project's levels.

### Using Cable Components from the Place Actors Panel

To use the Cable Component from the Place Actors Panel, do the following:

1.  From the **Main Toolbar**, click **Create** and select **Place Actors Panel**.
    
    ![Access Place Actors Panel from the Create button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c62b747-679d-44c3-8469-5fdc5dba8e9a/04-adding-place-actors-panel.png)
2.  In the search box, type `Cable`. Then drag **Cable Actor** into your level.
    
    Click image for full size.
    
3.  You can now position, rotate, and scale the Cable Actor so that it fits the needs of your level.
    

### Using Cable Components in Blueprints

To use the Cable Component in your Blueprints, create new Blueprint Class.

1.  **Right-click** from your **Content Drawer / Content Browser** and select **Blueprint Class**.
    
    ![Creating new Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bee5051d-0b08-4aa7-bcbd-f0749896b16e/07-creating-new-blueprint.png)
2.  Select **Actor** as a Parent Class for the new Blueprint.
    
    ![Select Actor from the Pick Parent Class Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bca37638-e269-4987-b61e-6f3a5799c247/08-select-actor-as-parent-class.png)
3.  Rename your Blueprint to **BP\_Cable**. Then double-click it to open it in the **Blueprint Editor**.
    
    ![Rename blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d623dfc-0f34-4f64-94e4-07daf242cfe6/09-rename-blueprint.png)
4.  From the **Components** tab, click the **Add** button. In the list, locate and select the **Cable** component
    
    ![Adding Cable component to the Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44810765-7f9c-460b-884e-802f48c1d299/10-adding-cable-component-to-blueprint.png)
5.  With the Cable Component now added, select it in the components list so that you can adjust its properties through the **Details** panel. For now, leave everything as the default, and make sure to **Compile** and **Save** your Blueprint before closing the editor.
    
    To make either side of the cable fall, disable the **Attach Start** or **Attach End** option from the Details panel. This can also be toggled while the game is running to go along with effects.
    
    ![Disabling Attach Start and Attach End](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b36cfb9c-89b4-47f0-8537-e63c2a89e179/11-cable-properties-details-panel.png)
6.  In the Content Drawer, locate the **BP\_Cable** and drag it into your level. Move and rotate it as needed.
    
    ![Dragging Cable Blueprint into the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aaddda08-426a-4baf-9f63-3ea6fcb90f7c/12-drag-cable-blueprint-into-the-level.png)

## Attaching Objects to the Cable ends

You can also attach objects to either end of the cable so that the objects will swing along with the cable. To accomplish this, do the following:

1.  From the Actors Panel, drag a **Cube Actor** into your level. Locate it next to the **BP\_Cable**, that you added before.
    
    ![Dragging the Cube Actor into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c60b906-8a52-463d-96f9-20f62bda5102/13-drag-cube-actor-into-the-level.png)
2.  Make sure that the Cube has its **Mobility** set to **Movable**.
    
    Click image for full size.
    
3.  Locate the Cube you want to attach to the end of the Cable Actor in the **World Outliner**. Then drag the Cube on top of the Cable Actor. After doing this, the following dialogue window will open. ![Drag the cube over the cable actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c11bc05-7153-465d-b70f-39e271b8b6dd/15-drag-the-cube-over-cable.png)
    
4.  Select **Cable End**, and in the viewport, you should see your Cube snaps to the end of the cable.
    
    ![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa02273f-775d-41be-b2e5-f6b1eec2d2d1/cc_attach_before.png)
    
    ![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8baeade-f7d0-4a4e-9ccf-e47eba598416/cc_attach_after.png)
    
5.  Now, select the Cable Actor in the level viewport. Then, in the **Details** panel under the **Cable** section, disable the **Attach End** option.  
    ![Disabling the Attach End option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe31934f-9eb7-4da1-b9b7-09950405d96b/16-disabling-attach-end.png)
    
    You do not have to only use the **Attach Start** and **Attach End** options to attach cables to Actors. You can also specify a Socket that can be used as the attachment point.
    
6.  After disabling **Attach End**, your cable should swing freely in the viewport.
    
    You can dynamically enable or disable the **Attach Start** and **Attach End** options at run time, which can make for some interesting effects.
    

## Collision and Stiffness

Enabling Collision and Stiffness will greatly increase the cost of the Cable Actor. Only enable these features if the cable has to collide with something in the world or if the cable needs some stiffness to help make the effect look better. If none of that is needed, it is best to keep these options disabled to save performance.

The Cable Component does have the option to have the cable collide with the world, controlling how stiff the cable is. To enable this functionality, perform the following steps:

1.  In the Blueprint Editor, go to the Details panel of the Cable Component. Locate the **Cable** section and expand its **Advanced** options.
    
    Click image for full size.
    
2.  Enable both the **Enable Stiffness** and **Enable Collision** options.
    
    ![Enabling Stiffness and Collision](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e6cda95-cd5e-42c1-97f0-f8651bf7b9a5/19-enabling-stiffness-and-collision.png)
3.  Now, when you move the Cable Actor around, or if an object collides with the Cable Actor, it should collide with the object it comes in contact with.
    

## Cable Component Properties Reference

This section contains reference information for each of the properties of the Cable Component:

#### Cable

![Properties in the Cable Section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6882472c-f6ed-4554-a97b-1c43624180c2/21-cable-section-properties.png)

| Property Name | Description |
| --- | --- |
| **Attach Start** | Should we fix the start to something or leave it free. If false, component transform is just used for the initial location of the start of the cable. |
| **Attach End** | Should we fix the end to something (using AttachEndTo and EndLocation), or leave it free. If false, AttachEndTo and EndLocation are just used for the initial location of the end of the cable. |
| **Attach End To** | Actor or Component that defines the end position of the cable. |
| **Component Name** | Name of the component property to attach the cable to. |
| **Attach End To Socket Name** | Socket name on the AttachEndTo component to attach to. |
| **End Location** | End location of cable, relative to AttachEndTo (or AttachEndToSocketName) if specified. Otherwise, relative to the cable component. |
| **Cable Length** | Rest length of the cable. |
| **Num Segments** | How many segments the cable has. |
| **Solver Iterations** | The number of solver iterations controls how 'stiff' the cable is. |
| **Substep Time** | Controls the simulation substep time for the cable. |
| **Use Substepping** | When false, will still wait for **Substep Time** to elapse before updating, but will only run the cable simulation once using all of the accumulated simulation time. |
| **Enable Stiffness** | Add stiffness constraints to cable. |
| **Enable Collision** | 
Perform sweeps for each cable particle at each substep to avoid collisions with the world. Uses the Collision Preset on the component to determine what is collided with. This greatly increases the cost of the cable simulation.

This is currently Experimental.



 |
| **Collision Friction** | If **Collision** is enabled, this option controls how much sliding friction is applied when the cable is in contact. |

### Cable Forces

![Properties in the Cable Forces Section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d54c7560-b290-4600-9cb8-42c9029d6c00/22-cable-forces-section-properties.png)

| Property Name | Description |
| --- | --- |
| **Cable Forces** | Force vector (world space) applied to all particles in the cable. |
| **Cable Gravity Scale** | Scaling applied to world gravity affecting this cable. |

### Cable Rendering

![Properties in the Cable Forces Section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21954c3b-cb08-4b66-aa5c-bcd60deb9740/23-cable-rendering-section-properties.png)

| Property Name | Description |
| --- | --- |
| **Cable Width** | How wide the cable geometry is. |
| **Num Sides** | Number of sides of the cable geometry. |
| **Tile Material** | How many times to repeat the material along the length of the cable. |