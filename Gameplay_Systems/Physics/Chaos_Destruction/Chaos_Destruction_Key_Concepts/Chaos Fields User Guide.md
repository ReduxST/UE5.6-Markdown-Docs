# Chaos Fields User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-fields-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-fields-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:33

---

You can find similar information in video format in the Developer Community site by watching the [Chaos Destruction - Fields](https://dev.epicgames.com/community/learning/tutorials/xdYp/chaos-destruction-fields) tutorials.

**Chaos Fields** use a region of space to control properties of a physics simulation. There are three primary types of fields — Anchor Fields, Strain / Force Fields, and Sleep / Disable Fields.

**Anchor** Fields are construction Blueprints that constrain a portion of a **Geometry Collection** in place during simulation. You can use them to make sure a certain part of the Geometry Collection stays fixed in place no matter what happens in the simulation.

**Sleep / Disable** Fields bring a Geometry Collection to rest when the bone (fractured piece) velocities fall below a specified threshold value. Sleeping bones can be reawakened during the simulation if they come in contact with an active object. Disabled bones cannot be reawakened.

**Strain / Force** Fields apply strain or linear velocity to a Geometry Collection during simulation.

Unreal Engine comes with pre-built Chaos Fields that can be used as-is, or modified by opening them in the **Blueprint Editor**.

To find them, click **Settings > Show Engine Content** in the **Content Browser**.

Go to **Engine > Content > EditorResources > FieldNodes** to find the available Chaos Fields.

![Go to Engine - Content - EditorResources - FieldNodes to find the available Chaos Fields](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8672cb8-7a8d-4518-bffa-18528eaff6c5/destruction-fields-2.png)

## Creating a Geometry Collection

In this section you will create a Geometry Collection so you can learn to use the Chaos Fields during a fracture simulation.

1.  Select a **Static Mesh Actor** in the scene, click the **Mode** dropdown and select **Fracture**.
    
    ![Select the Fracture mode from the Select Mode dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37d69636-3b2c-4cb0-a888-db9af7b63297/destruction-fields-3.png)
    
    This opens the **Fracture Mode** panels that contain all the tools for fracturing your mesh.
    
2.  In the **Generate** section, click **New** to create a new **Geometry Collection**.
    
    ![Click New to create a new Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/accd96fb-82ef-4f85-8cc2-1efb1b76abfa/destruction-fields-5.png)
    
    This asset type will be saved in the **Content Browser** and will be used to create your fractured mesh.
    
    ![Select the directory location, enter a name for your asset and click Create Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee6c843-4225-47b3-8971-b2d1780eab26/destruction-fields-6.png)
    
    1.  (1) Select the **directory location** where the Geometry Collection will be saved.
        
    2.  (2) Enter the name for the Geometry Collection asset.
        
    3.  (3) Click **Create Geometry Collection**.
        
    
    ![Click Save All in the Content Browser to save the new Geometry Collection asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8211751-a324-4d5b-b962-612a06bf1699/destruction-fields-7.png)
    1.  Click **Save All** in the **Content Browser** to save the new Geometry Collection asset.
3.  The Actor you selected in the scene is replaced with the Geometry Collection in the level.
    
    ![The Static Mesh is replaced with the Geometry Collection in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90c3eb79-b0dc-4dbd-9ad0-7fd0b0e838f9/destruction-fields-8.png)
    
    See the [Geometry Collections User Guide](/documentation/en-us/unreal-engine/geometry-collections-user-guide) to learn more about creating Geometry Collections.
    
4.  Use the Fracturing tools to fracture the Geometry Collection. In the example below, we used the **Slice** and **Uniform Voronoi** tools to create 4 Levels in the **Fracture Hierarchy**.
    
    See the [Fracturing Geometry Collections User Guide](/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide) to learn more about fracturing Geometry Collections.
    

## The Anchor Field

Anchor Fields set any Geometry Collection bone that falls within its volume to **Static** during the simulation.

Drag `FS_AnchorField_Generic` to the level and overlap it with a corner of the Geometry Collection.

Select the Geometry Collection and go to the **Details** panel. Scroll down to the **Chaos Physics** section and expand the **Initialization Fields** array. Click the **Index \[0\]** dropdown and select `FS_AnchorField_Generic` from the list.

![Click the Index 0 dropdown and select FS_AnchorField_Generic** **from the list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d06466b-f47e-42bf-95de-586a1684766a/destruction-fields-11.png)

Go to the **Clustering** section and disable the **Enable Clustering** checkbox. This is done for demonstration purposes as it will better show the fracturing of the Geometry Collection.

![Go to the Clustering section and disable the Enable Clustering checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e0a23fa-da42-4893-88ee-d1a9fe6ba6c1/destruction-fields-12.png)

Click the **Play Mode** menu button and select **Selected Viewport** or **Simulate** to see the results.

![The bones on the corner stay anchored in place during the simulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/692f5e7c-35e0-47f6-b0d6-476e54a4809c/destruction-fields-anchor-1.gif)

You can add as many Anchor Fields as you want by following the steps above. In the example below, we added Anchor Field to the top right corner.

![Simulation with two Anchor Fields](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/723ceec8-5b54-4f6a-9b47-6d99ec10e84a/destruction-fields-anchor-2.gif)

You can also use the same Anchor Field on several Geometry Collections at once. In the example below, we used one Anchor Field on two Geometry Collections.

![One Anchor Field used on two Geometry Collections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/345d62a7-1fc2-4abd-87fc-659acb4454fc/destruction-fields-anchor-3.gif)

Anchor Fields come with three **Falloff Shapes** — Box, Sphere, and Plane. These shapes affect how many bones are set to Static and how the effect is implemented.

To change the Falloff Shape, select the Anchor Field and go to the **Details** panel. Scroll down to the **Default** section and click the **Anchor Falloff Shape** dropdown. Select the desired falloff shape.

![Click the Anchor Falloff Shape dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7228573b-fbe8-4464-865d-2816b2a1901e/destruction-fields-14.png)

In the example below, we use a **Sphere** shape for the Anchor Field.

![Example of a sphere shape Anchor Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8c1b50d-e9f9-444d-b351-af06dfb054ec/destruction-fields-anchor-4.gif)

In the example below, we use a **Plane** shape for the Anchor Field.

![Example of a plane shape Anchor Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfed92c5-df66-49d7-991d-9c989cde37a7/destruction-fields-anchor-5.gif)

## The Sleep and Disable Fields

The **Sleep** and **Disable** Fields bring rigid bodies to rest when their velocities go below a given **Threshold** value. Higher Threshold values will stop objects more aggressively.

These Fields are used to improve simulation performance and prevent excess jittering of the Geometry Collection pieces as they collide with each other. They also give you more control over how many rigid bodies are part of the simulation.

Sleeping bodies can be reawakened when they collide with an active object. Disabled bodies are removed from the simulation completely after they come to a resting state. Disabled bodies cannot be reawakened.

This type of field also has a **Kill** option, in addition to Sleep and Disable. This option ignores the Threshold value and immediately stops the body from simulating and removes it from the simulation once it overlaps the Field's volume.

Drag **FS\_SleepDisable\_Generic** into the Level and place it as seen below.

Go to the **Details** panel and scroll down to the **Default** section. Here you can specify the **Threshold** value the field uses to apply its effect. You can also specify the **Field Behavior, Falloff Shape**, and whether you want to show the **Debug** information.

![The options available for the Sleep and Disable fields](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30018885-aa61-4b63-b6dd-ff5e2c12be96/destruction-fields-16.png)

In the example below we enabled the **Debug** option and used two Geometry Collections to show the effects of a Sleep Field. On the left, the **Threshold** value is set to **2**, and on the right, the value has been set to **50**.

![Example of Sleep fields with thresholds of 2 and 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be41f64b-4db6-4304-9cee-5b6a1095f135/destruction-fields-sleep-1.gif)

As you can see, when the first object passes through the volume it goes to sleep. However, it is awakened when it collides with the second object. The higher the Threshold value, the more aggressively the bodies will be set to sleep.

In the examples below, we switched to **Disable** Fields. The Field on the left has a **Threshold** value of **2**, and the Field on the right has a value of **200**.

![Example of Disable fields with thresholds of 2 and 200](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef9ad52c-4f40-4937-a95f-cc60f6262b95/destruction-fields-disable-1.gif)

Notice how the Geometry Collections on the right do not collide with each other after they have been disabled. The higher Threshold value shows the effect more prominently.

Finally, we can use **Kill** Fields to immediately stop any rigid body from simulating. Notice that on the right we show a Static Mesh simulating physics while we use Geometry Collections on the left.

![Example of Kill fields stopping a Geometry Collection and a Static Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd3b3460-817f-450c-90a4-b6c3f47dfcd4/destruction-fields-kill-1.gif)

## The Master Field

### Introduction

The `FS_MasterField` is a pre-built Chaos Field included with Unreal Engine. You can find it by going to **Engine > Content > EditorResources > FieldNodes.**

This Field comes with many options for customization and is used primarily to:

-   Activate rigid bodies by applying external strain that breaks the connection between bones.
    
-   Apply velocity to rigid bodies to make them move and spin in a realistic manner
    

In the example below, we placed a default `FS_MasterField` where it overlaps with a Geometry Collection.

In its default configuration, the Field applies a large amount of external strain which causes the Geometry Collection to fracture. Then, the Field adds radial and angular velocities to the broken pieces to make them spin. Finally, the Field applies noise to add randomness to the effect.

This is the result:

![The FS_MasterField applies strain to the Geometry Collection causing a fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a83adf33-e36a-4b5c-83a2-5422b6b9d03f/destruction-fields-fsfield-1.gif)

You can configure the shape of the Field by clicking the **Field Falloff Shape** dropdown and choosing an option.

![Select the Field Falloff Shape from the dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19ba9561-b05a-40d4-9f9e-a8c303b7de9c/destruction-fields-17.png)

You can also configure the way the Field is applied by clicking the **Activation Type** dropdown and choosing an option.

![Select the Activation Type from the dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0abfaa51-5cc6-4134-86ad-3ca6b0526b06/destruction-fields-18.png)

| **Activation Type** | **Description** |
| --- | --- |
| **Delay** | The field activates after the **Delay Amount**. |
| **OnTick** | The field activates on each tick. |
| **OnTickWithDelay** | The field activates on each tick after the initial **Delay Amount**. |
| **Trigger** | The field is activated by a Blueprint directly. |

You can set the Field's **lifespan** by going to **Advanced Field Settings > Timing and Lifespan** section in the **Details** panel. This is useful when you are creating Fields that need to apply their effects over a short period.

You will learn more about these settings and more in the following sections.

### External Strain

**External Strain** breaks the connections between the bones in a fractured Geometry Collection. You can modify the External Strain options of the Field by going to the **Apply External Strain to Break Node Connections** section in the **Details** panel.

![You can modify the external strain options of the field by going to the Apply External Strain to Break Node Connections section in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efe270b5-5e71-43dd-bcf7-a35234275bf3/destruction-fields-19.png)

| **Option** | **Description** |
| --- | --- |
| **Use External Strain** | If enabled, the Field applies external strain to the assigned Geometry Collections. |
| **Strain Magnitude** | The magnitude of the strain force applied. By default, this value is very high to ensure the applied strain force breaks the bones. If the strain force is lower than the Damage Threshold for the Geometry Collection, the strain will not cause a fracture. |
| **Strain Falloff Type** | Applies a falloff to the strain force within the volume. You can select between **Linear**, **Inverse**, **Square**, and **Logarithmic** falloff types. |
| **Strain** **Falloff** **Min Max** | Sets the falloff values from the center of the volume (Min) to the edge of the volume (Max). A value of 0 represents no falloff, and a value of 1 represents 100% falloff. |
| **Num Strain Hits** | Sets the number of times the Field will be applied. The Field is activated once per hit, so multiple hits allow the user to break multiple cluster levels before any forces are applied. |

#### Strain Magnitude

In the example below, the Field is applying more strain than the Geometry Collection's Damage Threshold, resulting in the bones breaking.

![The Geometry Collection breaks due to the strain applied by the Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79d75b8e-c9c2-40df-beb8-80e14102d978/destruction-fields-fsfield-2.gif)

In this example, we have two different Geometry Collections. The blue Geometry Collections have a Damage Threshold of 200,000, while the orange ones have a Damage Threshold of 500,000. The Field is applying internal strain with a magnitude of 400,000. This results in the blue Geometry Collections breaking, while the orange ones remain intact.

![The field is applying strain to two different Geometry Collections. The blue Geometry Collections have a Damage Threshold below the applied internal strain from the field, which results in fracturing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59ef6753-77b3-44e4-8685-6dcab7cef0ce/destruction-fields-fsfield-3.gif)

#### Strain Falloff Type and Min and Max

You can adjust the **Strain Falloff** by clicking the **Strain Falloff Type** dropdown and selecting an option. You can also adjust the Min and Max falloff values to get a desired result.

In this example, the Field has no falloff applied:

![This Field has no falloff applied](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa2f71f8-c868-46b2-ad2e-df399d5dfe8d/destruction-fields-fsfield-4.gif)

In this example, we applied a **Linear falloff** with a **Max** value of **2**:

![This Field has a Linear falloff with a Max value of 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fe71b5b-b475-42cd-9284-596e2e0a8ff7/destruction-fields-20.png) ![This Field has a falloff with a Max value of 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/417b4991-598f-4c06-8f9c-7f28638058f8/destruction-fields-fsfield-5.gif)

For performance reasons, we recommend avoiding using falloff with external strain. However, external strain falloff can be useful when combined with internal strain to achieve specific effects.

### Internal Strain

Internal Strain, or decay, changes the internal Damage Threshold values of the Geometry Collection. When active, a decay Field will lower the Damage Threshold of the bones inside the volume by the Decay Amount.

This can be used to weaken a Geometry Collection gradually, until it breaks from external strain.

In the example below, we set the **Activation Type** to **OnTick** with a **Delay Amount** of **1 second**. In addition, we enabled the **Use Decay** checkbox and set a **Decay Amount** of **100,000**, with a **Decay Delay** of **1 second**.

The Geometry Collection has a **Damage Threshold** of **500,000**.

These options will reduce the Damage Threshold of the bones within the volume by 100,000 every second, with a falloff towards the edges. Here are the results:

![We enabled Use Decay and set the Decay Amount to 100,000 with a Decay Delay of 1 second](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3783061-c905-4c0d-869a-c85523a61116/destruction-fields-21.png) ![The Field weakens the Geometry Collection until it fractures from external strain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3a6a078-f9da-4c81-a211-ce49796d1b2c/destruction-fields-fsfield-7.gif)

### Activate Rigid Bodies

There are situations where you might want to activate kinematic rigid bodies without using strain.

You can do this by going to the **Advanced Field Settings > Force Dynamic Switching** section under **Field Settings** and enabling the **Force Dynamic Switch** checkbox.

![Activate Kinematic bodies by going to the Advanced Field Settings - Force Dynamic Switching section and enabling the **Force Dynamic Switch** checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79fb323b-e2f0-44e4-a3a8-7eb44b472376/destruction-fields-22.png)

In the example below, the Geometry Collection is set to **Kinematic** and the field is activating the Geometry Collection without applying any strain or velocity.

![IThe field is activating the Geometry Collection without applying any strain or velocity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/391b2ab5-615e-41d6-89d6-5fd58bdb5a57/destruction-fields-fsfield-8.gif)

You can also activate **Static** and **Skeletal Meshes** by enabling the **Activate Tagged Static and Skeletal** checkbox.

![You can activate Static and Skeletal Meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/322388e1-b3a5-4868-abb4-22ba5ed459e4/destruction-fields-23.png)

For each Mesh you want to activate, set its **Mobility** to **Movable** and add the **Actor Tag** '**SM\_Rigids.**' In addition, make sure the Mesh has collision so it can simulate correctly.

![Set the Mobility setting to Movable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8707f27f-d002-4290-b431-6cf068bf2239/destruction-fields-24.png) ![Add the Actor Tag 'SM_Rigids'](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e08da18c-2783-48f4-94d8-fd966a14c947/destruction-fields-25.png) ![Both kinematic rigid bodies are activated by the fields](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7c9e86b-c7b0-442f-9b9e-fb5a55350bdb/destruction-fields-fsfield-9.gif)

### Velocity

#### Radial Velocity

Radial velocity pushes objects away from a point in space by a given magnitude. This point is in the center of the volume by default, but can be changed by the user.

In the example below the radial velocity is applied at the center of the sphere volume.

![The radial velocity is applied at the center of the sphere volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60acb305-7034-4b54-b7bb-8aae7c59089a/destruction-fields-fsfield-10a.gif)

To change the origin of the velocity, go to the **Advanced Field Settings > Velocity Controls** section and change the **Radial Position Offset**. In this example, we offset the origin in the Y Axis by 100 units. This results in the velocity being applied from the edge of the sphere volume, as seen below.

![You can change the Radial Position Offset here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b66b7ac-fb09-4a77-80bf-36b5f3237f96/destruction-fields-26.png) ![The velocity is applied from the edge of the sphere volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd257d32-d27e-46b4-a388-20d60d8a55fa/destruction-fields-fsfield-10b.gif)

You can also apply velocity in a specific direction by going to the **Apply Linear and Angular Velocities** section and enabling the **Use Directional Vector** checkbox.

![You can also apply velocity in a specific direction by going to the Apply Linear and Angular Velocities section and enabling the Use Directional Vector checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15edc0dd-2380-4e3a-8728-df272819cef2/destruction-fields-27.png)

In the example below, we are applying a Directional Magnitude of 800 in the up vector of the Field.

![This Field is applying a Directional Magnitude of 800 in the up vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20c9ce96-089a-4e7a-8061-2246400feb3e/destruction-fields-fsfield-11a.gif)

You can change the velocity direction by rotating the field. In this example, we rotated the field to change the direction of the velocity.

![The Field is rotated to change the velocity direction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36c8c380-a4ae-4a1c-9152-118aa9fbe3a9/destruction-fields-fsfield-11b.gif)

You can manually enter the direction vector by going to the **Advanced Field Settings > Velocity Controls** section and enabling the **Override Directional Vector** checkbox. Then, enter the **Directional Vector Override** value.

![You can manually enter the direction vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf989553-c4e9-49f6-abfa-7056e5ccdf7f/destruction-fields-28.png) ![The Field is applying velocity by using the Directional Vector Override value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad65cc4e-73b9-497d-9fcb-5aff585d1287/destruction-fields-fsfield-12.gif)

#### Angular Velocity

You can apply angular velocity by going to the **Apply Linear and Angular Velocities** section and enabling the **Use Torque** checkbox. You can control the magnitude of the velocity applied by setting the **Torque Multiplier** value.

In the example below, we set the **Torque Multiplier** to **64**.

![Enable the Use Torque checkbox and enter the Torque Multiplier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43b84edb-89ef-4434-acf2-0e0f643b0d80/destruction-fields-29.png) ![This Field is applying Torque with a multiplier of 64](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1f01a0c-8690-4c32-8c37-8c4fd7871434/destruction-fields-fsfield-13.gif)

### Force vs Velocity

The `FS_MasterField` comes with options to apply force or velocity within its volume. By default, the Field applies velocity, which explicitly sets the velocity of objects to the given value without taking into account their mass or volume.

Applying force is more realistic, as it takes into account each object's mass during the simulation. To adjust a Geometry Collection's mass, open the **Geometry Collection asset** from the **Content Browser** and go to the **Collision** section. Enter the desired amount for **Mass**.

![Open the Geometry Collection asset, go to the Collision section and enter the desired amount for Mass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/205cc300-6168-4309-9ebb-368e2a9784ec/destruction-fields-30.png)

Keep in mind that for Geometry Collections, the **Mass** value under the **Physics** section will not be used by the Field. Instead, only the settings in the Geometry Collection asset itself will be considered.

If you are applying force to a Static Mesh or Skeletal Mesh, set the object's mass by going to the **Details** panel and scrolling down to the **Physics** section. Enable **Simulate Physics** and enter the **Mass** value.

![Go to the Details panel and scroll down to the Physics section. Enable Simulate Physics and enter the Mass value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d454d9b8-2e8d-42eb-b197-59e607034984/destruction-fields-31.png)

In the example below, you can see the Field on the left is applying velocity, while the Field on the right is applying force. Inside each field, there are two objects with a mass of 500 and 1000 Kilograms.

As you can see, both objects on the Field that is applying velocity move in the same way even though they have different masses. However, on the Field that is applying force, the objects are affected differently when the same amount of force is applied.

![The field applying velocity does not take into account the object's mass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9c175e6-18b0-4ffa-a5fb-7cc054de36ec/destruction-fields-fsfield-14.gif)

### Falloff

The `FS_MasterField` has a variety of options to control the falloff of velocity applied within its volume. You can change the falloff type by going to the **Apply Linear and Angular Velocities** section and clicking the **Velocity Field Falloff Type** dropdown.

![You can change the falloff type by going to the Apply Linear and Angular Velocities section and clicking the Velocity Field Falloff Type dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f01d1338-085e-4f34-b596-71ec1e95e6b1/destruction-fields-32.png)

**Velocity Field Falloff Types**

| **Falloff Type** | **Description** |
| --- | --- |
| **None** | No falloff function is applied to the Field. |
| **Linear** | The falloff function will be proportional to X, where X represents the distance between the center of the volume and its edges. |
| **Inverse** | The falloff function will be proportional to 1 / X, where X represents the distance between the center of the volume and its edges. |
| **Squared** | The falloff function will be proportional to X \* X, where X represents the distance between the center of the volume and its edges. |
| **Logarithmic** | The falloff function will be proportional to Log(X), where X represents the distance between the center of the volume and its edges. |

When using the Linear falloff type, the field will apply the maximum velocity at the center of the Field, and fade to the minimal value when it reaches the edges of the Field.

In the example below, you can see a Field where the **Minimum Velocity Falloff** is **0**, and the **Maximum Velocity Falloff** is **1**.

![In this Field the Minimum Velocity Falloff is 0, and the Maximum Velocity Falloff is 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ae5590a-0a70-4368-9ca3-4c4f7cf8fc5e/destruction-fields-fsfield-15.gif)

You can adjust the minimum and maximum Falloff values to create different effects. For example, the Field below is using a **Minimum Falloff** value of **\-1**, and a **Maximum Falloff** value of **0**. The negative value pulls objects towards the center, instead of repelling them. This creates the following effect:

![In this Field the Minimum Velocity Falloff is -1, and the Maximum Velocity Falloff is 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc83e814-acb1-43ff-b56e-965abaff4cbe/destruction-fields-fsfield-16.gif)

You can also set the Minimum Falloff and Maximum Falloff values to larger integers to create a ring effect within the volume. In the example below, the **Minimum** **Falloff** value is set to **\-1,** and the **Maximum Falloff** value is set to **1**.

![In this Field the Minimum Velocity Falloff is -1, and the Maximum Velocity Falloff is 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b987c3f-e1f7-4081-a787-d6fbd37889f9/destruction-fields-fsfield-17.gif)

### Noise

The `FS_MasterField` includes the ability to add noise to the velocities and forces applied within its volume. Noise adds randomness to the otherwise predictable velocities applied to objects inside the Field.

To add noise to the Field, go to the **Noise** section in the **Details** panel, and enable the **Use Noise** checkbox. You can set the minimum and maximum noise values multiplied against the velocities inside the Field. You can also set the **Noise Scale Multiplier** which scales the perlin noise used to create randomness.

![To add noise to the Field, go to the Noise section in the Details panel, and enable the Use Noise checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a06dc8f-6825-4198-af08-c6b4378b0443/destruction-fields-33.png)

In the example below, the box Field is applying velocity on Tick without any noise.

![The box Field is applying velocity on Tick without any noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/412c141c-a7df-4345-8633-cd1ca42d5cb3/destruction-fields-fsfield-18.gif)

In the example below, the box Field is applying velocity on Tick with a **Minimum Noise** value of **0.8** and a **Maximum Noise** value of **1**. The **Noise Scale Multiplier** is set to **30**.

![The box Field is applying velocity on Tick with a Minimum Noise value of 0.8 and a Maximum Noise value of 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ab5b01b-56c0-4bd4-9e24-46b7f34237fd/destruction-fields-fsfield-19.gif)