# Cloners and Effectors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:55

---

## Introduction

Motion Design has its own unique integration of the established Niagara particle system. You can use Motion Design to create lively motion graphics by way of creating clones or multiple instances of existing geometry. You can influence a variety of actor properties either as a group or on a granular level.

The core features are powered by Niagara, but working with Cloners and Effectors simplifies that process significantly through streamlined tooling. You can use cloners and effectors for scaling, rotation, and positioning and for procedural noise, so you can randomize and colorize your actors to create unique visual effects.

This overview assumes readers are familiar with the content of the [Motion Design Quick Start](/documentation/en-us/unreal-engine/motion-design-quickstart-guide-in-unreal-engine).

## Where to Find the Tools

First, either enable the **ClonerEffector** plugin, or enable the Motion Design mode (which was covered in the Quick Start guide).

When you enter Motion Design mode, click on **Actors** in the palette to see the two main tools:

-   the **Cloner Actor**
-   the **Effector Actor**

You can also use the **Place Actors** tab, and search for Motion Design Cloner and Effector.

![Place a cloner or effector actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74b43b94-d641-433a-b11d-c2c1e9d838b2/image_0.png)

You can find the Cloner and Effector actors in the **Place Actors** panel here:

![Motion Design actors in the Place Actors panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8fd3c62-2a25-426b-a593-3872974e2153/image_1.png)

## Cloner Actors

Double-clicking on the Cloner Actor from the toolbar in the **Motion Design** mode places the actor in the middle of your level with a default mesh applied to it. You can also click on the Cloner Actor button and click in your viewport to place it. In this case, it uses the DefaultCube, but you can apply any mesh that you want. For example, you can select another shape from the **Motion Design 3D Shapes** palette (also seen in the above screenshot).

Here is an example of mixing and matching the shapes, using sphere and torus meshes instead of the default cube mesh:

![Mixed sphere and torus clone shapes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a4ce105-aa9c-4a78-9e5b-3609e650a05b/image_2.png)

Your Details panel has the following categories:

-   [General](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#general)
-   [Cloner](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#cloner)
-   [Effector](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#effector)
-   [Emission](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#emission)
-   [Physics](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#physics)
-   [Rendering](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#rendering)
-   [Utilities](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#utilities)

### General

The **General** category contains common transforms for positioning your cloner actors. These transforms do not directly affect [layouts](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#layouts).

![Cloner actor General category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/091c57a6-3cf9-4de5-8a22-4d25e9b52870/image_3.png)

| **General Properties** | **Description** |
| --- | --- |
| Transform |   |
| **Location** | Standard location transform, using X, Y, and Z coordinates. |
| **Rotation** | Standard rotation transform, using X, Y, and Z coordinates. |
| **Scale** | Standard scale transform, using X, Y, and Z coordinates. |

### Cloner

The **Cloner** category handles the majority of how your system sorts and presents your clones. This includes how you assign a **Layout** for your cloner, tint them a specific color, and force the cloner to update if changing your settings isn’t resulting in an instant change. It also contains the ability to disable the cloner completely with the **Enabled** toggle.

![Cloner actor Cloner category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4daed39-c93a-4d07-84d6-dc2d574fcb8c/image_4.png)

#### Force Update Cloner

In the event that your cloner system fails to update, this acts as a fallback to ensure proper generation.

#### Seed

The **Seed** property, when used together with the **Range** property enabled, gives variations when changing the value.

In the example below, we modified the **OffsetMax** property to adjust the position of the shapes. Changing the **Seed** randomizes those positions.

Seed value of 0:

![OffsetMax with Seed 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1403f30-e3a8-4215-a8fb-d42bf7241142/image_5.png)

Seed value of 1:

![OffsetMax with Seed 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a289f9d9-0c04-4a2a-b85f-10113b133aa5/image_6.png)

#### Color

You can set the color of your clones using an RGBA value. You can use the Color Picker, or just input your values directly.

#### Advanced

In this sub-category you can set how often your tree refreshes using the **Tree Update Interval**. To reduce system overload, the default value of 0.2 means that your tree does not update every tick. Instead, it updates every 5 ticks, approximately.

![Cloner category Advanced properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8702c306-143b-4a48-b5b7-b5210e7e3339/image_7.png)

The **Visualizer Sprite Visible** toggle shows or hides the cloner widget in your viewport:

![Visualizer sprite visible](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7107eb74-25f9-4739-86f1-2a23b3ab1556/image_8.png)

| **Cloner Properties** | **Description** |
| --- | --- |
| **Force Update Cloner** | Manually forces cloners to update in the event of an error. |
| **Enabled** | Enables using cloners. |
| **Seed** | Used to randomize cloners positions. |
| **Color** | Standard RGBA color selection using the Color Picker |
| Advanced |   |
| **Tree Update Interval** | Determines how often your tree refreshes. |
| **Visualizer Sprite Visible** | Makes the cloner widget visible when enabled. |

#### Layouts

The most important option in this category is the **Layout**. Layouts share similar options like range, step, effectors, lifetime, rendering, and progress. They also have specific options depending on the layout selected.

![Layouts category properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09555871-e3dd-4072-b83d-aef6ecb3edf0/image_9.png)

Setting the Layout changes how the clones arrange themselves. By setting the other properties in the image above, you can spread out the clones with **Spacing** and adjust the number of clones with the **Count** properties.

The available options for arranging the clones using the Layout dropdown are:

-   [Grid](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#grid)
-   [Line](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#line)
-   [Circle](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#circle)
-   [Cylinder](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#cylinder)
-   [Sphere Uniform](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#sphereuniform)
-   [Honeycomb](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#honeycomb)
-   [Mesh](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#mesh)
-   [Spline](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#spline)
-   [Sphere Random](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#sphererandom)

Each **Layout** has different settings and options.

![Layout dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/467b5edf-8906-4c96-adcb-e360c6bc5abb/image_10.png)

##### Grid

The Grid layout sorts the clones into a 3-dimensional grid. You can set parameters for how many clones display on each axis (X, Y, Z), and the clones' spacing. This layout also provides you the option to limit your clones to a constraint, which is a specific shape profile, and to invert the constraint.

![Constraint options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df65989c-822d-45c6-b033-3dd8482ededf/image_11.png) ![Grid layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3188bc6-fe2f-4452-9152-b5f389726092/image_12.png)

Here is an example using the **Constraint** to take on the shape of a sphere:

![Sphere constraint properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01d3225f-4bd1-4223-84b4-cb8da747af0f/image_13.png) ![Grid with sphere constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9477948-2977-48f1-9698-eb5468467144/image_14.png)

Each of those **Grid Layout** options also gives you the ability to **Invert Constraint**.

![Invert Constrait option enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5751808a-0875-43b0-ba3d-0cca269c0802/image_15.png) ![Grid layout with inverted sphere constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b044e4fe-294e-4947-8e9c-ce052bb16d30/image_16.png)

You also have the option to use a texture to constrain your clones:

![Grid with texture constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae3e01ef-72c0-45e8-b9d8-0874b141843a/image_17.png)

| **Grid Layout Properties** | **Description** |
| --- | --- |
| **Count X / Y / Z** | The number of cloners in the grid along the X, Y, or Z axis. |
| **Spacing X / Y / Z** | The space between cloners in the grid along the X, Y, or Z axis. |
| **Constraint** | 
Options are:

-   None (don’t use a constraint)
-   Cylinder
-   Sphere
-   Texture



 |
| **Invert Constraint** | Enable this option to invert the effects of the selected Constraint. Only available when Constraint is set to an option other than None. |

##### Line

The Line layout arranges the cloner actors into a straight line. You can control the number of clones using the **Count** property, and the space between those clones using the **Spacing** property. You can use the **Axis** property to control which direction the clones flow, and the **Rotation** property to cause the clones to curl along a combination of the X,Y, and Z axes.

![Line layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c1670e9-5626-49cf-a080-06b0f82ea27d/image_18.png)

| **Line Layout Properties** | **Description** |
| --- | --- |
| **Count** | The number of cloners in the line. |
| **Spacing** | The spacing between the cloners in the line. |
| **Axis** | The main axis (X, Y, or Z) along which the line is oriented. |
| **Rotation X / Y / Z** | Rotation of the line in degrees towards the X, Y, or Z axis. Does not directly rotate the cloner actors. |

##### Circle

The **Circle** layout arranges the cloner actors into a circle. You can set the clone count with the **Count** property, and the **Radius** of the circle of clones. You can also use the **Angle Ratio** to determine how spaced out the clones will be along the circle. 0 means no spacing between cloners at all, and 1 means clones are spread out evenly along the shape. You can use the **Plane** dropdown to define the plane (XY, YZ, XZ) on which the clones spawn. The **Orient Mesh** toggle forces all clones to face the center of the circle.

![Circle layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e6c8287-8490-487d-abb2-1786cc4ddc13/image_19.png)

You can set the rotation angle of your circle using the **Angle Start** property.

Adjusting the **Angle Ratio** spreads the clones along the circle. If you want the clones to only spread across half of the circle, then here is what a .5 value would look like:

![Using Angle Ratio to create a half-circle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f52eb54-7855-4bb7-987e-87f942abcc37/image_20.png)

Scaling on a single axis property, as opposed to fully linked, results in an oval:

![Circle scaled on a single axis to produce an oval](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbd8ecfc-f7d6-4689-ab30-5d85f0926c7f/image_21.png)

| **Circle Layout Properties** | **Description** |
| --- | --- |
| **Count** | The number of clones in the circle. |
| **Radius** | The radius of the circle. |
| **Angle Start** | Sets the rotation angle of the circle. |
| **Angle Ratio** | Determines how spread out on the circle the clones are. Values range from 0 to 1, with 0 meaning no spacing, and 1 meaning completely even spacing around the whole circle. |
| **Orient Mesh** | Forces clones to face the center of the circle. |
| **Plane** | 
Determines the axes used to define the plane on which the Circle layout clones spawn. Options are:

-   XY
-   YZ
-   XZ



 |
| **Scale X / Y / Z** | Scales the layout circle on the X, Y, or Z axis. Does not scale the cloner actors. |

##### Cylinder

The Cylinder layout arranges the cloner actors into a cylinder. It has mostly the same properties as the Circle layout, with the addition of the Height and Height Count properties.

![Cylinder layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6557195b-1065-4919-b918-3cf8d31b991a/image_22.png)

| **Cylinder Layout Properties** | **Description** |
| --- | --- |
| **Base Count** | The number of clones in the circle that makes up the base of the cylinder. |
| **Height** | The height of the cylinder from the plane that defines its base. |
| **Height Count** | The number of clones in a line from the base to the top of the cylinder. Each one represents a complete circle of clones. |
| **Radius** | The radius of the cylinder. |
| **Angle Start** | Sets the rotation angle of the cylinder. |
| **Angle Ratio** | Determines how spread out on each circle of the cylinder the clones are. Values range from 0 to 1, with 0 meaning no spacing, and 1 meaning completely even spacing around the whole cylinder. |
| **Orient Mesh** | Forces clones to face the center of the cylinder. |
| **Plane** | 
Determines the axes used to define the plane on which the cylinder layout clones spawn. Options are:

-   XY
-   YZ
-   XZ



 |
| **Scale X / Y / Z** | Scales the layout cylinder on the X, Y, or Z axis. Does not scale the cloner actors. |

##### Sphere Uniform

You can set the total **Count** of the clones in the sphere, and the **Radius** of the sphere, which spreads the clones apart evenly.

![Sphere Uniform layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/464621c6-330f-4ec9-b0f2-ef2234c34ccb/image_23.png)

The **Rotation** property rotates the entire sphere along the X, Y, or Z axis:

![Rotating a sphere layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e63d03d-5a2b-4e85-be8c-2910ad4befcd/image_24.gif)

The **Ratio** property sets how much of the sphere will be covered by your clones. A .5 value produces a result like the image below:

![Using the Ratio property to cover half a sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93ca0d5e-4093-4f06-8180-174804f507d5/image_25.png)

The **Orient Mesh** toggle forces all clones to face the center of the sphere.

![Using Orient Mesh to force clone facing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1142586c-a557-4cda-875b-9b0feef4c0a5/image_26.png)

If you set the **Scale** property unevenly for the X, Y, and Z axes, the result is an elliptical spheroid, like the image below:

![Using uneven scaling to create an elliptical spheroid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d5fa982-c1ee-40f3-95a6-177f4dfe95bc/image_27.png)

| **Sphere Uniform Layout Properties** | **Description** |
| --- | --- |
| **Count** | The number of clones in the sphere. |
| **Radius** | The radius of the sphere, which controls how spread out the clones are. |
| **Ratio** | Sets how much of the sphere is covered by your clones. |
| **Orient Mesh** | Forces clones to face the center of the sphere. |
| **Rotation X / Y / Z** | Rotation of the sphere in degrees towards the X, Y, or Z axis. Does not directly rotate the cloner actors. |
| **Scale X / Y / Z** | Scales the layout sphere on the X, Y, or Z axis. Does not scale the cloner actors. |

##### Honeycomb

You can set the axis that the elements clone along using the **Plane** setting. You can control the number of clones using the **Width Count** and **Height Count**, and use the **Width Offset** and **Height Offset** properties to control the clones' positional offset. To space out the clones, use the **Width Spacing** and **Height Spacing** properties.

![Honeycomb layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb4bcc29-f2fe-46bf-be2f-e32ef270844e/image_28.png)

You can twist your **Honeycomb** using the **Twist Factor** setting, and decide which axis to twist along using the Twist Axis property. The value is measured in percentage, with 100% representing a full 180 degree twist.

Twisting along the Y-axis:

![Honeycomb layout twisted along Y axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b9881d2-b2bd-430a-94e1-986c0c9d6cf6/image_29.png)

Twisting along the Z-axis:

![Honeycomb layout twisted along Z axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03034694-f30b-49d8-9edd-d6f148a05d39/image_30.png)

Twisting along the X-axis:

![Honeycomb layout twisted along X axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64f3aabb-af63-4559-864b-dd5e52b3b9b0/image_31.png)

| **Honeycomb Layout Properties** | **Description** |
| --- | --- |
| **Plane** | 
Determines the axes used to define the plane on which the hexagonal layout clones spawn. Options are:

-   XY
-   YZ
-   XZ



 |
| **Width Count** | The number of clones in the layout horizontally. |
| **Height Count** | The number of clones in the layout vertically. |
| **Width Offset** | Controls the horizontal position offset. |
| **Height Offset** | Controls the vertical position offset. |
| **Width Spacing** | Controls the spacing between clones horizontally. |
| **Height Spacing** | Controls the spacing between clones vertically. |
| **Twist Factor** | Controls how much twist to apply to the Honeycomb layout, in percentage. 100% is a 180 degree twist. |
| **Twist Axis** | Determines which axis to use to twist the layout (X, Y, or Z). |

##### Mesh

This layout allows you to populate clones along a static mesh or skeletal mesh. You can select these under the **Asset** property. The example below shows the selected number of clones populating evenly over each of the static mesh’s vertices.

![Mesh layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/119c02f5-d48e-45fa-a594-5514e09c9e4a/image_32.png)

You are able to sample the mesh in a variety of ways:

![Mesh Sample Data options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17338912-7cb4-4cb5-8bec-bfcf2f21b4eb/image_33.png)

Here is an example sampling triangles:

![Mesh sampled using triangles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30aebe93-81f4-4bd0-a4bc-1ffb0625bb86/image_34.png)

Here is an example using a skeletal mesh:

![Using a skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bd99403-ac27-4c0b-9dce-1ff762dde6bb/image_35.png)

| **Mesh Layout Properties** | **Description** |
| --- | --- |
| **Sample Actor** | Identifies the actor used as the mesh source. |
| **Asset** | 
Determines the type of asset. Options are:

-   Static Mesh
-   Skeletal Mesh



 |
| **Count** | The number of clones on the mesh. |
| **Sample Data** | 

Determines how the Motion Design system samples the mesh. Options are:

-   Vertices
-   Triangles
-   Sockets (skeletal mesh only)
-   Bones (skeletal mesh only)
-   Sections



 |

##### Spline

When using the Spline Layout, you can use a spline actor created using the Motion Design toolbox as the Sample Actor, and clone that actor repeatedly along the path of the spline. You can orient the clones to rotate along with the curve using a combination of the **Orient Mesh** toggle, which causes the clones to follow the spline's tangent, and rotating the individual static mesh 90 degrees on the Y axis. The image below shows the result of using such a combination.

![Spline layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9af7d4a3-7423-41e7-8a6c-0160eb01c089/image_36.png)

The image below shows the same actor without the Orient Mesh toggle enabled and default transforms.

![Spline with Orient Mesh disabled and default transforms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1faafd35-c547-47c0-86ce-5424beccb082/image_37.png)

| **Spline Layout Properties** | **Description** |
| --- | --- |
| **Count** | The number of clones on the spline. |
| **SampleActor** | The spline actor used for the clones. |
| **Orient Mesh** | Forces clones to follow the spline's tangent. |

##### Sphere Random

The Sphere Random layout spreads out your mesh clones around the surface of the sphere in a random, chaotic manner. This is controlled by the **Distribution**, **Latitude**, and **Longitude** settings. Enabling **Orient Mesh** causes all the clones to direct themselves around the surface of the sphere along the forward vector. In the example below, the forward vector comes **from** the center of the sphere.

![Sphere Random layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cbb2adf-fd31-45c8-9fff-f8685630c7df/image_38.png)

Without **Orient Mesh** enabled, you will end up with a result like the image below, where all clones will follow the forward vector (the X axis in this example):

![Sphere Random with clones all following forward vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af1aedf6-3e94-441b-a113-326a7af70d3b/image_39.png)

A .5 value for both **Longitude** and **Latitude** forces the clones to cover a quarter of the sphere. You can increase your clone count to a large value (800 in the example shown) to demonstrate this more effectively.

![Longitude and latitude both halved to quarter the sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3959f944-b285-4714-a56b-78fcadae9b58/image_40.png)

Increasing the **Scale** setting reduces the density of your clones by expanding the total area that they cover.

Small Scale value:

![Smaller scale, higher clone density](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77e54574-c841-4131-a1bc-52a19beb63bc/image_41.png)

Larger Scale Value:

![Larger scale, lower clone density](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cf4e7d4-81cd-42ba-9caf-dab229a7badf/image_42.png)

Changing the **Rotation** value rotates the group of clones.

| **Sphere Random Layout Properties** | **Description** |
| --- | --- |
| **Count** | The number of clones in the sphere. |
| **Radius** | The radius of the sphere, which controls how spread out the clones are. |
| **Distribution** | Determines how evenly spread the clones are. |
| **Longitude** | Determines how much the cloners cover the sphere horizontally in degrees. |
| **Latitude** | Determines how much the cloners cover the sphere vertically in degrees. |
| **Orient Mesh** | Enable this to orient all the clones on the surface of the sphere layout. |
| **Rotation X / Y / Z** | Determines the rotation of the sphere in degrees towards the X, Y, or Z axis. Does not directly rotate the cloner actors. |
| **Scale X / Y / Z** | Scales the layout sphere on the X, Y, or Z axis. Does not scale the cloner actors. |

#### Range

![Cloner category Range properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c19ff84-e6d5-4f38-8784-e441a56dd484/image_43.png)

Since every clone is a particle, you can use the **Offset**, **Rotation**, and **Scale** settings to manipulate the initial transforms for the clone. This manipulation can be uniform or non-uniform. You can also randomize the initial placement from the current layout. The image below shows an example of just modifying the **ScaleMin** and **ScaleMax** properties to scale the sphere clones between 0.001 and 2.613.

![Sphere with uniformly scaled clones of different sizes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b99ffd6-ff2a-4597-859c-636355dfd987/image_44.png)

You can disable the ScaleUniformEnabled property to cause the clones to have more random shapes.

![Sphere with non-uniformly scaled clones of different sizes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/779924d6-6754-4a9f-8314-4dac474c8b7b/image_45.png)

| **Range Properties** | **Description** |
| --- | --- |
| **Enabled** | When enabled, cloners use Range features. |
| **OffsetMin X / Y / Z** | Determines the minimum offset on the X, Y, or Z axis. |
| **OffsetMax X / Y / Z** | Determines the maximum offset on the X, Y, or Z axis. |
| **RotationMin X / Y / Z** | Determines the minimum rotation in degrees on the X, Y, or Z axis. |
| **RotationMax X / Y / Z** | Determines the maximum rotation in degrees on the X, Y, or Z axis. |
| **ScaleUniformEnabled** | When enabled, clones scale uniformly. |
| **ScaleMin X / Y / Z** | Determines the minimum scaling on the X, Y, or Z axis. |
| **ScaleMax X / Y / Z** | Determines the maximum scaling on the X, Y, or Z axis. |

#### Step (Cloner)

![Offset transforms using the Cloner category Step property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5078b5f2-71f8-4a8f-9288-e199521a4956/image_46.png)

With the **Step** property, you can set the scale and rotation of your clones in an offset manner. To use the effect, the clone count must be higher than 1. The scale and rotation accumulate per clone.

| **Step Properties** | **Description** |
| --- | --- |
| **Enabled** | When enabled, cloners use the Step feature. |
| **Rotation X / Y / Z** | Determines the rotation in degrees on the X, Y, or Z axis. |
| **Scale X / Y / Z** | Determines the scaling on the X, Y, or Z axis. |

### Emission

The **Emission** category properties provide ways for you to spawn new clones, and then have them despawn, controlling the clone spawn rate, number, and duration.

![Emission category properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3add8e8-b6c7-4d5a-876e-97212d261f84/image_47.png)

#### Spawn

You can use the **Spawn** feature when you want to create dynamic simulations by having your clones respawn after their lifetime expires. If you want your clones to respawn continuously, change the **Emission Mode** from **Once** to **Infinite**, then enable the [Lifetime](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#lifetime) feature. You can edit the aesthetic by changing the **Emission Style** property from **Instant** to **Rate**. The **Emission Rate** property determines how many clones appear per second.

If you only want to spawn a fixed number of clones rather than an unlimited number, you can change the value of the Emission Mode property from **Infinite** to **Multiple** and set the **Emission Count** value to whatever you want.

| **Spawn Properties** | **Description** |
| --- | --- |
| **Emission Mode** | 
Determines whether clones spawn infinitely or a fixed number of times. Options are:

-   **Once**: Clones spawn once.
-   **Infinite**: Clones spawn infinitely.
-   **Multiple**: Clones spawn a fixed number of times.



 |
| **Emission Count** | Determines how many spawn loops for cloners will occur when Emission Mode is set to Multiple. |
| **Emission Interval** | Determines the intervals between cloner spawns. |
| **Emission Style** | 

Determines how quickly clones spawn. Options are:

-   **Instant**: All clones spawn immediately at the start of a loop.
-   **Rate**: Clones spawn over time.



 |
| **Rate** | Determines how many clones spawn per second. Only used when BehaviorMode is set to Rate. |

#### Lifetime

When enabled, the Lifetime options provide a way for you to despawn clones after a period of time.

The image below depicts the beginning of the clones' lifetime.

![Lifetime property clones starting state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eb8ac0c-52d8-41e8-ae45-654f314c4af3/image_48.png)

Clones begin to disappear as time passes.

![Clones disappearing as lifetime ends](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d88088c-dab6-4408-8bdd-a776a4a4b232/image_49.png) ![Example lifetime settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b5c1480-ccb0-4656-990a-838139e96610/image_50.png)

The **Min** and **Max** properties control the minimum and maximum time that a clone is active. Modifying either property restarts the timer.

The **ScaleEnabled** toggle gives you access to the list of prescribed curve **Templates**.

![Lifetime ScaleEnabled options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb4c622d-f891-4e13-a8a9-ca36e6690812/image_51.png)

| **Lifetime Properties** | **Description** |
| --- | --- |
| **Enabled** | Cloners will use Lifetime features when you enable this option. |
| **Min** | The minimum time a cloner will be active. |
| **Max** | The maximum time a cloner will be active. |
| **ScaleEnabled** | When enabled, the curve templates are available. |
| **Templates** |   |
| **Linear Ramp Up** | Lifetime curve template. |
| **Linear Ramp Down** | Lifetime curve template. |
| **Drop Off** | Lifetime curve template. |
| **Ease In** | Lifetime curve template. |
| **Pulse Out** | Lifetime curve template. |
| **Smooth Ramp Up** | Lifetime curve template. |
| **Smooth Ramp Down** | Lifetime curve template. |
| **Ramp Up Ramp Down** | Lifetime curve template. |

#### Progress

You can use the **Progress** settings to hide or reveal clones. It can reveal clones from top to bottom, or bottom to top when the **Invert Progress** option is enabled.

![Emissions category Progress properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2cdfa63-ae72-47c5-a020-58e6635c4e06/image_52.png)

Clones at .5 Progress Value:

![Progress at half](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3a61979-fe69-41ed-bf30-81ec08c29e17/image_53.png)

Clones at .5 Progress Value with **Invert Progress** enabled.

![Inverted progress at half](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5579dd2-ef93-4e1c-a5c6-3a2e77b3b502/image_54.png)

| **Progress Properties** | **Description** |
| --- | --- |
| **Invert Progress** | When enabled, clones are revealed from bottom to top instead of top to bottom. |
| **Progress** | Defines the proportion of the clones that are hidden or revealed. |

### Physics

Because each clone is also a particle, particle physics provides a way for you to have your clones collide with both surfaces and each other.

#### Surface Collision Enabled

By enabling the **Surface Collision Enabled** property, you can have your clones collide with surfaces in your level (in the example below, the floor). The images below provide examples of each case.

Before enabling collision:

![No collision physics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dccecc79-1523-4cfa-bf9d-a25d8f1f0eb1/image_55.png)

After enabling the **Surface Collision Enabled** checkbox, and moving the position of the cloner actor toward the floor:

![Surface collision enabled only, clones collided with surface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d43cb06c-6f0c-493b-b37b-1ad25f7704cf/image_56.png)

Because in the example we used only the Surface Collision Enabled property, moving the clones up again does not cause them to change relative position any further, because they don't collide with each other. The image below shows this effect:

![Surface collision only, clones moved up again](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab36851f-5230-4d23-97b7-a7d389b56b80/image_57.png)

#### Particle Collision Enabled

You can also use the **Particle Collision Enabled** property to have your cloners collide with each other:

![Particle collision enabled, clones colliding with each other](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc3a2f6a-6bd8-45ae-bbe6-ae7abb50ad9e/image_58.png)

You can use the Surface Collision Enabled and Particle Collision Enabled properties together. When you do so, clones react both to colliding with the floor and each other, resulting in a clump like the following image:

![Surface collision and particle collision enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c25f67b2-b5de-46c1-8d57-033a385ae50d/image_59.png)

#### Collision Velocity Enabled / Collision Iterations

When you want to calculate the physics after the collision has occurred, you can take particle interaction even further using the **Collision Velocity Enabled** property.

You can enhance the precision of the interaction with the **Collision Iterations** property, which determines how frequently the collision solver process repeats; higher values mean more precise collisions, but impacts system performance.

![Collision Velocity Enabled and Collision Iterations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6149a75-82c1-453e-a13c-b5e403220810/image_60.png)

#### Collision Grid Size / Collision Grid Resolution

The **Collision Grid Size** and **Collision Grid Resolution** properties directly impact how many of the clones are affected by the collision. A large value, relative to the size of the area you are trying to cover, will affect a higher number of your clones. A low value produces a result similar to the image below. In this example, any clone that falls outside of a 200, 200, 200 grid volume does not have collision physics:

![Particle collision with low collision grid size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d97b65a3-b829-43cc-ab4a-b01ffb04988b/image_61.png)

Adjusting the Collision Grid Size to a higher value provides more volume in which particles collide, resulting in something like the image below:

![Particle collision with high collision grid size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e30ea8f-0103-4346-8c8e-383606b8d74b/image_62.png)

A low Collision Grid Resolution value results in collision physics applied to large chunks of your clones collectively, rather than as individual particles. A higher Collision Grid Resolution results in collision physics calculations applied properly to individual clones.

#### Collision Radius Mode

The **Collision Radius Mode** property determines how the overall radius is calculated for each attached actor. In the example in the image above, there are two actors - the torus and the sphere.

-   **Extent Length**: Calculates from the center of the mesh to the furthest point. This is useful for unevenly sized shapes.
-   **Manual**: Provides a way to define the size of each mesh regardless of the *actual* size of the mesh. This is useful when you want some padding, or to reduce the calculated size regardless of its actual size.
-   **Min Extent**: Calculates the shortest side of the referenced mesh.
-   **Max Extent**: Calculates the longest side of the referenced mesh.

#### Mass Min / Mass Max

**Mass Min** and **Mass Max** define the overall weight of the particle, in kilograms (kg).

| **Physics Properties** | **Description** |
| --- | --- |
| **Surface Collision Enabled** | When enabled, clones collide with surfaces in your level. |
| **Particle Collision Enabled** | When enabled, clones collide with each other. |
| **Collision Velocity Enabled** | When enabled, clones bounce away from collisions with added velocity. |
| **Collision Iterations** | Determines how many collisions are calculated for clones. |
| **Collision Grid Resolution** | Determines how precisely collision physics are applied to clones. |
| **Collision Grid Size X / Y / Z** | Defines the volume in which clones collide, using the X / Y / Z axes. |
| **Collision Radius Mode** | 
Determines how the overall radius is calculated for each attached actor. Options are:

-   Extent Length
-   Manual
-   Min Extent
-   Max Extent



 |
| **Mass Min** | Defines the minimum weight of a particle (clone), in kg. |
| **Mass Max** | Defines the maximum weight of a particle (clone), in kg. |

### Rendering

You can use the cloners’ **Rendering** settings to control the clones' general visibility and orientation after you set all the other details in the other Cloner settings, depending on the values you choose for several additional properties in this category.

#### Mesh Render Mode

There are several different mesh render modes to choose from.

##### Iterate

Iterates through each of the attached meshes.

![Iterate Mesh Render Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d2bc7f3-ef29-4e83-b911-832dcb5dcb96/image_63.png)

##### Random

Arranges the attached meshes randomly.

![Random Mesh Render Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc52f54d-61d0-47ea-acb5-c4f664e64103/image_64.png)

##### Blend

Blends meshes based on the total count and the attached meshes.

![Blend Mesh Render Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62be2886-4a99-4aee-9498-a8c54495c0ad/image_65.png)

#### Mesh Facing Mode

You can determine the direction the clones face using the **Mesh Facing Mode**.

![Mesh Facing Mode options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e998c543-3513-4203-886c-5b958e67448f/image_66.png)

##### Default

The **Default** option uses the forward vector as seen in the example image below. The arrows are all facing the forward vector and will not rotate.

![Default Mesh Facing Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aa16107-cf48-4465-832a-1eb811bc941a/image_67.png)

##### Velocity

Orients the clones based on their velocity direction. As they rotate around the sphere, they maintain orientation in the direction of their rotation.

![Velocity Mesh Facing Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20082dc-9dda-494c-a4e0-0cd2afb18ae5/image_68.png)

##### Camera Position

Orients all clones to face the camera. For example, the arrows in the GIF below only show the front and none of the tail because they fully face the camera at all times.

![Clones oriented towards camera position](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/739050db-91b8-4e49-9a91-4aeed8233978/image_69.gif)

##### Camera Plane

Orients all clones to point toward the plane where the camera is, rather than directly at the camera itself.

![Clones oriented towards camera plane](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/066d3b96-58ed-46e9-b17c-d37689c00c36/image_70.gif)

#### Meshes Cast Shadows

You can make meshes cast shadows by enabling the **Meshes Cast Shadows** property.

#### Default Meshes

If there is no mesh attached below the cloner actor in the Details panel, you can set the default meshes that appear instead. You can do this by using the **Default Meshes** option. In this example, we set it to SM\_Ball\_01.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9cf1503-3890-4b13-832d-217961f49e0c/image_71.png)

#### Visualize Effectors

The **Visualize Effectors** property toggles using a default material for all clones, so that you can evaluate the results of using effectors more clearly by temporarily removing any confounding colors and patterns added by your material.

#### Use Override Material

You can define a custom material for all clones by enabling the **User Override Material** property.

![Use Override Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2a886e4-4c73-4090-ad88-e470e78e732b/image_143.gif)

##### Override Material

Use this property to select your override material. You can select any material from your Content Browser.

##### Edit with Material Designer

When you have selected an override material, you can edit it by clicking **Edit with Material Designer**. This opens your material in the **Motion Design Material Designer** in a separate panel.

##### Set Translucent Priority

You can enable this property to use the **Set Translucent Priority** feature.

| **Rendering Properties** | **Description** |
| --- | --- |
| **Mesh Render Mode** | 
Determines the render mode for the cloners. Options are:

-   Iterate
-   Random
-   Blend



 |
| **Mesh Facing Mode** | 

When enabled, the clones always face the camera. Options are:

-   Default
-   Velocity
-   Camera Position
-   Camera Plane



 |
| **Mesh Cast Shadows** | When enabled, the clone meshes cast shadows. |
| **Default Meshes** | Use this array to set the default meshes used for the clones when there is no mesh attached below the cloner. |
| **Visualize Effectors** | When enabled, a default material is used for all clones to simplify viewing effectors. |
| **Use Override Material** | 

When enabled, you can define a custom material used for all clones. Has several sub-properties and options you can use to define your material:

-   **Override Material**
-   **Edit with Material Designer**
-   **Set Translucent Priority**



 |

### Utilities

There will be occasions where you don’t want a cloner to remain in a "live" state, and only need it to exist with the settings that you’ve established. Several of the utilities described below are useful in that use-case.

![Cloner actor Utilities category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77202a73-9aee-4ce5-a925-23f9246aba28/image_72.png)

For example, if you create something with the cloner and you want actual actors in the scene instead of particles, you can export your cloner creation by converting them into static meshes or dynamic meshes. You can then use those meshes (including instances) like any other mesh, with all the advantages of those asset types. It's like taking a snapshot of the particles, and transforming the results into actors in your level.

#### Create Default Actor Attached

If you deleted the default actor that spawns when you create a cloner, clicking this utility respawns that actor using the actor currently set as the default. If you didn’t change the current default actor, this utility spawns a standard cube static mesh.

If you do not have a mesh attached below the cloner, you can set the default meshes that appear instead, using the **Default Meshes** option under the **Rendering** tab. In the example in the image below, we set it to SM\_Ball\_01.

![Example Default Mesh settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e3153f9-d9e5-45e1-ae1a-8db719d7cd8a/image_73.png) ![Example Default Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cadcc20b-6619-40a6-861e-36384f9749de/image_74.png) 

#### Convert to Static Meshes

Clicking this utility requires you to specify a save location for the static mesh output.

![Specify save location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a7e6c2d-b851-43c8-91c4-5042f289edba/image_75.png)

Instances of each clone are saved as a static mesh and placed where they originated.

![Saved static meshes in the outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96d0e84a-eb56-4beb-80e8-92bb461aaf28/image_76.png)

#### Convert to Static Mesh

This utility condenses all clones into a single static mesh.

The image below shows an example of a cloner and clones before converting to a static mesh:

![Before converting to a static mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d839e8c6-767b-4dfa-baaf-f702316505e7/image_77.png)

After using the Convert to Static Mesh utility, this static mesh output appears in your Content Drawer:

![Static mesh output in the Content Drawer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d8cf1a2-e81c-41f6-a40a-8659a281cd02/image_78.png)

The newly-created static mesh is given an auto-generated name, using the format `SM_{ClonerName}_{MeshUniqueId}`. You can rename the static mesh in the Content Drawer.

#### Convert to Instanced Static Mesh

Converts all children of the cloner into an **Instanced Static Mesh**. This might result in performance improvements.

#### Convert to Dynamic Mesh / Convert to Dynamic Meshes

These utilities are similar to the utilities for converting to static meshes described previously, but convert the clones to dynamic meshes instead. **Dynamic Meshes** are described in the documentation for **Modifiers**.

#### Create Cloner Sequencer Tracks

You can use this to link a cloner to Sequencer, which helps you to scrub your colliding, cloned animations linearly. To accomplish this, the animation is cached.

The Effector Collision Velocity Physics property is a good way to experiment with this feature. Enable the property first, then set up your clones before creating the track for Sequencer, as shown in the following images:

![Effector Collision Velocity Physics property settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f8d1b41-47cd-42af-82b8-3fbf0ba160a4/image_79.png) ![Create Cloner Sequencer Tracks button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e34452b6-6dc2-4788-8123-b995a7f90958/image_80.png)

When you create the Sequencer track, the result should be similar to the following example:

![Example Sequencer track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffb24d47-b8de-46cb-a036-28e13363117f/image_81.gif)

## Effector Actors

You can use **effectors** to modify the various transform values of your clones. You can set this to be done from multiple points of engagement by using multiple effectors all linked to your cloner system. Examples of results you can achieve using effectors include:

-   Moving clones in different directions.
-   Randomizing clone positions with noise patterns.
-   Manipulating clone transforms by offsetting, rotating, and scaling them.

The main requirement is that the clones must be within the effector’s area of influence.

### Creating an Effector

There are two ways to create an effector:

-   Select an existing cloner, then click the **Spawn Linked Effector** button in the Details panel.
    
    ![Spawn Linked Effector on an existing cloner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52ddf8e4-74a3-4910-9e52-6f7ac39186d3/image_82.png)
-   Place an effector directly by double-clicking **Effector Actor** on your **Motion Design** toolbar, or by using the **Place Actors** tab and searching for the Motion Design Effector Actor.
    
    ![Place an Effector Actor directly](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dfaa954-43fd-4b5c-abf3-641d230ba56a/image_83.png)

If you only have a single cloner, we recommend the first method.

If you want to use multiple effectors, then you need to create an **Effector** actor, name it, and add it to the **Effectors** array on your cloner.

![Creating multiple effectors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81a18a80-ed7e-43e8-bdee-71cd0c1da4fd/image_84.png) ![Adding effectors to your cloner array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63c845dc-5921-4eff-88cc-f2afec4b36a9/image_85.png)

After adding and assigning the new effector, you can set up your project to resemble the following example. The red area shows the original effector, and the new effector is blue.

![Using multiple effectors together](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94002353-32fd-4788-b3a8-7b226c0cfecf/image_86.gif)

### General

![Effector actor General category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54e6ff41-5bb9-40f4-9771-dd9a76e63c4c/image_87.png)

The General category shows standard settings for transforms applied to the Effector actor.

| **General Properties** | **Description** |
| --- | --- |
| Location | Standard location transform, using X, Y, and Z coordinates. |
| Rotation | Standard rotation transform, using X, Y, and Z coordinates. |
| Scale | Standard scale transform, using X, Y, and Z coordinates. |
| Mobility | 
Determines the [actor mobility](/documentation/en-us/unreal-engine/actor-mobility-in-unreal-engine), similar to other UE actors. Options are:

-   Static
-   Stationary
-   Movable



 |

### Effector

In the **Effector** category, the **Enabled** checkbox determines whether you want to use the tool. To use effectors, make sure the checkbox has a check.

![Effector actor Effector category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2406993d-9a1c-4339-ac74-70055e5bf91a/image_88.png)

The **Magnitude** property determines the strength of the effector's impact on the clones within its range.

You can use the **Color** property to colorize the clones your effector is affecting. If you don’t want to colorize them, you can set this property to white. You can use the Unreal Engine color picker to select the color, or just enter RGBA values directly.

Under the **Advanced** section, you can:

-   Control the visibility of your effector's inner and outer boundaries in the viewport using the **Visualizer Sprite Visible** property
-   Control the visibility of the visualizer component under the Effector actor in the Details panel using the **Visualizer Component Visible** property.

Visualizer Sprite Visible enabled:

![Visualizer sprite enabled, boundaries showing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee83aa56-ccfa-4f79-acfe-9c78955c731d/image_89.png)

Visualizer Sprite Visible disabled:

![Visualizer sprite disabled, boundaries hidden](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/266bd604-9bfc-4b87-8662-a03b61446941/image_90.png)

The **Channel Data Identifier** property is an advanced feature that provides a way for you to use effectors with custom projects outside Motion Design. For example, advanced users could build their own custom systems using Niagara modules that can be affected by Motion Design effectors using the effector's data channel. The values are transient, and can be different every time the world is reloaded.

| **Effector Category Properties** | **Description** |
| --- | --- |
| **Enabled** | Enables using effectors. |
| **Magnitude** | Determines the strength of the effector's impact on the clones within its range. |
| **Color** | Standard RGBA color selection using the color picker. |
| **Advanced** |   |
| **Visualizer Component Visible** | When enabled, the visualizer component is visible in the Details panel. |
| **Visualizer Sprite Visible** | When enabled, the visualizer sprite is visible in the viewport. |
| **Channel Data Identifier** | Identifies effectors for use with custom systems. |

### Forces

You can use **Forces** to animate your clones without the need for keyframes, instead relying on Niagara physics. There are several methods to animate within the Effector system, which you can combine as desired. The settings for the various Forces options are only accessible when the associated Force is enabled.

![Effector actor Forces category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6667e42-c63b-4525-a14b-20ee2cabfea8/image_91.png)

| **Forces Properties** | **Description** |
| --- | --- |
| **Forces Enabled** | Enables the Forces effector options. |
| **Orientation Force Enabled** | Enables the Orientation Force and related settings. |
| **Vortex Force Enabled** | Enables the Vortex Force and related settings. |
| **Curl Noise Force Enabled** | Enables the Curl Noise Force and related settings. |
| **Attraction Force Enabled** | Enables the Attraction Force and related settings. |
| **Gravity Force Enabled** | Enables the Gravity Force and related settings. |
| **Drag Force Enabled** | Enables the Drag Force and related settings. |
| **Vector Noise Force Enabled** | Enables the Vector Noise Force and related settings. |

#### Orientation Force

![Orientation Force properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a69c76ff-3ab7-4029-a5a8-3bed96e843cc/image_92.png)

This Forces option influences the orientation of the clones at a constant rate, and spins them faster depending on how close they are to the center of the **Inner Radius**.

In this example, the darker green area that the effector is reaching is twirling the shapes at a faster rate than the greyer shapes based on their intersection with the inner radius of the effector. If the clones are outside of the inner and outer boundaries, they will not spin at all.

![Orientation Force ring of toruses example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df1f6af8-2300-450e-bb12-80614b25400d/image_93.png)

You can combine the **Orientation Force Rate**, **Orientation Force Min**, and **Orientation Force Max** properties to manipulate where the affected clones are facing and how often they cycle. The Orientation Rate changes the speed of rotation, while the Orientation Force Min and Max regulate the cycle speed.

![Orientation Force spinning example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4e66754-75e7-4539-b3f0-c0d557116869/image_94.gif)

| **Orientation Force Properties** | **Description** |
| --- | --- |
| **Orientation Force Rate** | Determines the rotation speed of the clones. |
| **Orientation Force Min X / Y / Z** | The minimum force applied to clones along the specified axis. |
| **Orientation Force Max X / Y / Z** | The maximum force applied to clones along the specified axis. |

#### Vortex Force

![Vortex Force properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41fbca40-7fe6-442a-aa42-61f50679d69f/image_95.png)

Early in the process, the clones will begin to drift after increasing the force along the X axis.

![Vortex Force example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6ac2422-20e2-4302-b037-93e51d93b14b/image_96.gif)

This rotates the clones according to Vortex Force Amount and around a Vortex Force Axis. The values in the GIF above combined with the size of the effector result in a relatively slow reaction that sends the clones offscreen.

| **Vortex Force Properties** | **Description** |
| --- | --- |
| **Vortex Force Amount** | Determines the force of rotation applied to the clones. |
| **Vortex Force Axis X / Y / Z** | Determines the axis of rotation. The magnitude of the different axis determines the relative position of the final axis in relation to the cardinal axes, with the result normalized to 1. |

#### Curl Noise Force

The two properties here are **Curl Noise Force Strength** and **Curl Noise Force Frequency**.

-   Increasing **Curl Noise Force Strength** increases the acceleration affecting the clones.
-   **Curl Noise Force Frequency** sends the clones in different directions. The higher the value, the more time it will take the clones to disperse, because there is more randomness in the direction of the force applied to the clones.

The results are deterministic, not random, and depend on the cloner's seed. When the same seed value repeats for the same arrangement of layout and cloners, it always has the same effect.

The image below shows the effect of a Curl Noise Force Frequency value of 1 after 2 seconds:

![Curl Noise Frequency value of 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/599de89d-1a58-400e-8512-97e233d5ecb1/image_97.png)

Here is the same setup except with a **Curl Noise Force Frequency** value of 50 after 2 seconds:

![Curl Noise Frequency value of 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2122d626-cd34-4a8f-a54e-2fc4eb6b82bb/image_98.png)

| **Curl Noise Force Properties** | **Description** |
| --- | --- |
| **Curl Noise Force Strength** | Determines the magnitude of the force applied to clones. |
| **Curl Noise Force Frequency** | Determines the randomness of the force's direction. |

#### Attraction Force

Thia Force option causes your clones to flow toward the effector’s location. They will flow faster the closer they are to the inner radius of the effector. In the example below, the green area is the inner radius.

![Attraction Force example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/319d69d8-e80c-4765-aca6-c47962ecc1e9/image_99.png)

The **Attraction Force Falloff** property decreases the speed of the particles as it gets closer to the outer boundary. In the example below, the outer boundary is represented by the red outer area.

![Attraction Force Falloff example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2464d0b1-5d12-4d35-8674-8ee6f1507103/image_144.gif)

| **Attraction Force Properties** | **Description** |
| --- | --- |
| **Attraction Force Strength** | Determines how quickly clones flow towards the center. |
| **Attraction Force Falloff** | Decreases particle speed closer to the outer boundary. |

#### Gravity Force

Using this forces clones to fall gradually depending on the inner/outer radius set in the **Shape** property.

The image below shows an example setup of clones before enabling **Gravity Force**.

![Clones before enabling Gravity Force](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4086693d-65c9-49cc-84fd-db1a5e6ab6e0/image_100.png)

This image shows the same setup shortly after enabling Gravity Force:

![Clones just after enabling Gravity Force](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e495b7b-38ce-4208-9a6d-f78507b6f0f0/image_101.png)

Combining Gravity Force and Orientation Force produces an effect like in the image below:

![Gravity Force abd Orientation Force combined example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c28a8db4-0c6a-43f7-a5b6-4624386f47d3/image_102.png)

| **Gravity Force Properties** | **Description** |
| --- | --- |
| **Gravity Force Acceleration X / Y / Z** | 
Determines the magnitude of the acceleration along each axis.

A value of -981 on the Z axis approximates real world gravity (9.81 m/s/s downwards, or -981 in Unreal Units).



 |

#### Drag Force

You can use this to add drag and decrease the speed of your forces. If you use it in conjunction with another force like Vortex Force, increasing the Drag Force Linear property makes everything move slower.

The GIF below shows an example of what occurs when an effector with drag force moves off to the left, allowing the Vortex Force to take over.

![Drag Force and Vortex Force combined example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47f9a2af-c523-43f1-9ca0-f22bda4d8c7e/image_103.gif)

| **Drag Force Properties** | **Description** |
| --- | --- |
| **Drag Force Linear** | Determines the magnitude of the linear drag force, which acts to slow down any linear movement of particles. |
| **Drag Force Rotational** | Determines the magnitude of the rotational drag force, which slows down any rotation of the particles. |

#### Vector Noise Force

This Forces option shifts particles in all directions with speed depending on the **Vector Noise Force Amount** property.

The results are deterministic, not random, and depend on the cloner's seed, so the same seed value repeated for the same arrangement of layout and cloners will always have the same effect.

![Vector Noise Force example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/586d29b3-9bcc-44d1-9ad7-b1b3a8d81f09/image_104.png)

| **Vector Noise Force Properties** | **Description** |
| --- | --- |
| **Vector Noise Force Amount** | Determines the magnitude of the Vector Noise Force. |

### Mode

There are four modes that you can use to influence an individual clone’s transforms. The effects of the Mode you choose depend on the [shape](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#shape) of the effector and the proximity of the clone.

| **Mode Properties** | **Description** |
| --- | --- |
| **Mode** | 
Choose which mode to use to affect clone transforms. Options are:

-   Offset
-   Target
-   Noise Field
-   Push



 |

#### Offset

**Offset** applies standard transformation properties like Location, Rotation, and Scale to the clones within range of the effector. The image below shows an offset of the X axis value and a rotation of 80. This affects some effector Shape options more than others depending on their proximity to the Offset effector.

![Offset Mode example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a9b5ae8-015b-4b19-bda7-3afbb7595857/image_105.png)

| **Offset Mode Properties** | **Description** |
| --- | --- |
| **Offset X / Y / Z** | Offsets the influence of the effector by the specified distance on the indicated axes. |
| **Rotation X / Y / Z** | Standard rotation transform, using X, Y, and Z coordinates, within the influence of the effector. |
| **Scale X / Y / Z** | Standard scale transform, using X, Y, and Z coordinates, within the influence of the effector. |

#### Target

By default, this mode automatically sets the **TargetActor** to the effector. All clones rotate to face the effector as long as they are within the inner or outer boundary of the effector type used.

![Target mode example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6853175d-d7d4-4852-9dad-2c5225e83200/image_106.png)

You can also target a specific actor. In the example below, there is a cube mesh present in the level. As long as the clones are within the inner and outer boundaries of the effector, they will face the static mesh. It does not matter if the target static mesh itself is within the effector range. It only matters that the meshes that you want to face the target are within that range.

![Clones tracking a target actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b106e87a-ce65-4f03-962d-85470900790f/image_107.gif) ![Select a target actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fe434e0-5dd4-4ef3-87a2-f7415aedba97/image_108.png)

| **Target Mode Properties** | **Description** |
| --- | --- |
| **TargetActor** | Defines the target actor all clones face when within the influence of the effector. |

#### Noise Field

The **Noise Field** organizes and animates clones based on a variety of parameters. The example below uses a combination of the various **Strength**, **Pan**, and **Frequency** properties:

![Noise Field example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcb7d986-0cce-456d-8fc7-8faf40b8c772/image_109.png)

##### Scale Strength

**Scale Strength** adjusts the scaling of each clone in the affected area along the selected axes according to the easing curve. In the examples below, the Scale Strength is set to affect the Z axis. The clones rise and fall with the noise field passing through the effector area due to the **Pan** setting value.

This example shows the Scale Strength on the Z axis set to 1.0:

![Noise Field Scale Strength low Z axis scaling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2da12ae5-74ac-4750-9abf-208e639fd635/image_115.png)

The example below shows the same effector set-up, except with the Scale Strength on the z axis set to 25.0:

![Noise Field Scale Strength high Z axis scaling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d4fa2de-d103-45b9-9347-2561f2d3ba85/image_116.png)

##### Location Strength

**Location Strength** determines how flat the noise field is. The example below uses a relatively low value:

![Noise Field Location Strength low value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b85f0e47-fbba-4a24-bacb-b703941547de/image_110.gif)

In the example below, the Location Strength is set to a relatively high value.

![Noise Field Location Strength high value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c6d2a5f-4ac5-426a-8ce6-6f3037ecb4d3/image_111.gif)

##### Rotation Strength

The **Rotation Strength** property rotates clones according to how close they are to the center of the effector. In the example shown below, the clones most affected are whiter and more acutely rotated.

![Noise Field Rotation Strength example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc31c9fc-c066-49d9-b718-3879989b5748/image_112.gif)

##### Pan

The **Pan** value determines how quickly the noise curve passes through the effector. When you use a low value, the result should look similar to the example below.

![Noise Field Pan value low example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69496846-070d-4513-8d71-c2658845c4f3/image_113.gif)

The example below shows Pan set to a high value.

![Noise Field Pan value high example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b244e425-a738-4f73-8dbc-aa8fbe6c038b/image_114.gif)

##### Frequency

Setting the **Frequency** value determines the overall intensity of the noise, which affects the number of peaks.

The example below shows a relatively low Frequency value.

![Noise Field Frequency value low example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4542f808-8380-4811-a0c3-b3c80e79f8ee/image_117.gif)

Here is the same example, except with a higher Frequency value.

![Noise Field Frequency value high example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a509d795-0ea4-4f6a-bfc6-e2212589fb51/image_118.gif)

| **Noise Field Mode Properties** | **Description** |
| --- | --- |
| **Location Strength X / Y / Z** | Determines how flat the noise field is. Higher values result in a less flat field. |
| **Rotation Strength X / Y / Z** | Determines how much the affected clones rotate around the indicated axes. |
| **Scale Strength X / Y / Z** | Determines how much the cloners affected will move along the indicated axes. |
| **Pan X / Y / Z** | Determines the rate and axes along which the noise field passes through the effector area. |
| **Frequency** | Determines the intensity of the noise, affecting the number of peaks. |

#### Push

You can use the **Push** mode to push the clones in a variety of directions and with varying levels of **Push Strength**.

![Push Mode properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbc3743c-7d36-466b-a84a-8eafc9d2e023/image_119.png)

##### Push Forward

This push option creates a push effect on your clones parallel to the axes defined for the Push Strength.

![Push Forward example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3710acb-c832-463a-9146-f92882f1906f/image_120.png)

##### Push Right

This push option creates a push effect on your clones horizontally perpendicular to the axes defined for the Push Strength.

![Push Right example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0f87241-2f9c-4a07-9a6a-6edec855ec0e/image_121.png)

##### Push Up

This push option creates a push effect on your clones vertically perpendicular to the axes defined for the Push Strength.

![Push Up example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90b1a361-3ea8-4e02-bb26-04603f515bfd/image_122.png)

When using the Push Forward, Push Right, and Push Up mode options, you can push in the opposite direction (back, left, or down) by using negative numbers for the values.

##### Push Effector

This push option creates a unit vector based on the relative locations of the effector and particle, and pushes based on the Push Strength along that vector.

##### Push Random

This push option creates a random unit vector based on the cloner seed, and pushes based on the Push Strength along that vector. This effect is deterministic, the same options with the same cloner seed always produce the same result.

| **Push Mode Properties** | **Description** |
| --- | --- |
| **Push Strength X / Y / Z** | Determines the magnitude of the push on the indicated axes. |
| **Push Direction** | 
Determines the direction of the push. Options are:

-   Forward
-   Right
-   Up
-   Effector
-   Random



 |

### Step (Effector)

![Effector actor Step Mode example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aefb4633-6740-465d-bb77-7760cb8803af/image_123.gif)

The Step effector provides a method for you to position, scale, and rotate your clones along a strict before-and-after plane, represented by the floating plane as it moves through the system.

| **Step Mode Properties** | **Description** |
| --- | --- |
| **Position X / Y / Z** | Determines the position of the Step effector plane on the indicated axes. |
| **Rotation X / Y / Z** | Determines the rotation of the Step effector plane on the indicated axes. |
| **Scaling X / Y / Z** | Determines the scaling of the Step effector plane on the indicated axes. |

### Shape

Using the **Effector** panel, there are several shaped formations you can set up to control the scope of an effector's influence on your clones, for a variety of effects. Their primary function is to restrain the effector's influence within specific bounds. You can begin by using the **Unbound** mode to understand the full extent of the effectors on your design when they aren't limited,, but below you will find descriptions for each Shape option in the order that they appear on the menu.

For all Shape options except Unbound, you can set the **Easing** property, which provides a list of curves you can choose from (linear, sine, cubic, circular, elastic, and so on). These apply an additional intensity effect on the clones in range, based on the shape you selected. See below under [Effector Boundaries](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#effectorboundaries) for more information.

Except when specified otherwise, all examples for demonstrating shapes shown below use the following settings for the **Mode**.

| **Property** | **Value** |
| --- | --- |
| **Mode** | Noise Field |
| **Scale Strength X** | 1.0 |
| **Scale Strength Y** | 1.0 |
| **Scale Strength Z** | 25.0 |
| **Frequency** | 1.0 |

Values not listed are 0.

![Shape example settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d358c14-61f2-4fe5-a917-b2fdae772e96/image_124.png)

| **Shape Properties** | **Description** |
| --- | --- |
| **Shape** | 
Determines the shape applied to the effector. Options are:

-   Sphere
-   Plane
-   Box
-   Unbound
-   Radial
-   Torus



 |
| **Easing** | Determines the easing curve applied to the effector's influence as it passes through the boundaries of the shape. Options are listed below. |

#### Effector Boundaries

Most effector shapes have two wireframe boundaries:

-   An **inner boundary**, inside which clones are fully affected by whatever effect is generated by the effector. By default, the inner boundary area is shown in **red**.
    
-   An **outer boundary**, inside which clones are partially affected by whatever effect is generated by the effector. By default, the outer boundary area is shown in **blue**.
    

The exception is any effector with the [Unbound](/documentation/en-us/unreal-engine/motion-design-cloners-and-effectors-in-unreal-engine#unbound) shape. See below for more information.

The outer boundary interpolates the effect on the clones between the full effect within the inner boundary area, and the default clone behavior outside the effector's area. How much the effector affects the clones within the outer boundary area depends on:

-   The position of the clones within the outer boundary, with respect to the edge of the inner boundary and the external region.
    
-   The Easing property curve associated with the effector, which determines how the interpolation is calculated.
    
    -   There are many different curves available, mostly based on various mathematical functions. See the list of curves below along with images which demonstrate each curve.

| **Curve Name** | **Image** | **Curve Name** | **Image** |
| --- | --- | --- | --- |
| **In Expo** | ![In Expo curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b4f047e-7a8a-4e28-a6e9-4186e60a9911/in-expo-curve.png) | **In Out Quint** | ![In Out Quint curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1909ba4f-82de-4650-b42b-6a9c4960afaf/in-out-quint-curve.png) |
| **In Circ** | ![In Circ curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f1b6374-4034-4186-815b-5473fe69dc0a/in-circ-curve.png) | **In Out Quart** | ![In Out Quart curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6d0c040-d578-4b85-b65c-b40d861b0cb4/in-out-quart-curve.png) |
| **In Quint** | ![In Quint curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4d7a557-860c-460d-9e60-2f181bad8b82/in-quint-curve.png) | **In Out Quad** | ![In Out Quad curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6909dba1-59f5-46b7-8547-d88452deb693/in-out-quad-curve.png) |
| **In Quart** | ![In Quart curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/553ee768-b453-4532-a58a-9f19424d69fb/in-quart-curve.png) | **In Out Cubic** | ![In Out Cubic curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba7769f9-4a6a-4c48-87b2-5dec60c0c928/in-out-cubic-curve.png) |
| **In Quad** | ![In Quad curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6ec6de3-0f1e-4669-9c20-449efc2cce83/in-quad-curve.png) | **In Out Sine** | ![In Out Sine curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb07f4e5-3f82-4ba1-b8ba-dbccf6e14e76/in-out-sine-curve.png) |
| **In Cubic** | ![In Cubic curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52e4d7e4-a6be-412b-9700-12bb734ec7ae/in-cubic-curve.png) | **Linear** | ![Linear curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6859a982-2ac0-4bbb-a783-e3507f4019ed/linear-curve.png) |
| **In Sine** | ![In Sine curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e5a551c-4c11-403f-9145-78a8a0d6d79d/in-sine-curve.png) | **In Bounce** | ![In Bounce curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a3e14df-871a-427b-a8a4-8a8de5f52375/in-bounce-curve.png) |
| **Out Expo** | ![Out Expo curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bec9756e-28ec-4873-be8f-80ac5b93b642/out-expo-curve.png) | **In Back** | ![In Back curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77d78226-e4dc-4cd7-a406-31c974fb4622/in-back-curve.png) |
| **Out Circ** | ![Out Circ curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07ebc878-83ff-4f94-afa1-ac680a20853a/out-circ-curve.png) | **In Elastic** | ![In Elastic curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41b19477-8749-4baf-aaca-fb0d85f706bc/in-elastic-curve.png) |
| **Out Quint** | ![Out Quint curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1309a157-f56d-4f1e-8af8-29c544b27b62/out-quint-curve.png) | **Out Bounce** | ![Out Bounce curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/889e5b4b-4392-43a4-889c-5eccbf9a755c/out-bounce-curve.png) |
| **Out Quart** | ![Out Quart curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b01afd6e-c3e5-4982-8529-fbad56041320/out-quart-curve.png) | **Out Back** | ![Out Back curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3976080-fa80-4e1f-ae31-6369bf8bf1fc/out-back-curve.png) |
| **Out Quad** | ![Out Quad curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41f70a75-5cdb-42cf-ba05-ae963c389a8e/out-quad-curve.png) | **Out Elastic** | ![Out Elastic curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20437922-3ee2-4751-b992-3ad52b66e8d3/out-elastic-curve.png) |
| **Out Cubic** | ![Out Cubic curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7af23e4-21ce-4c8d-8e03-2764e3083192/out-cubic-curve.png) | **In Out Bounce** | ![In Out Bounce curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb4cee8b-1d31-48f1-aacb-6e58e77b6c50/in-out-bounce-curve.png) |
| **Out Sine** | ![Out Sine curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eba3958b-9713-4c6f-8e5b-4e54df5c63b3/out-sine-curve.png) | **In Out Back** | ![In Out Back curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49405bc1-e43b-4555-945d-c13d41d72589/in-out-back-curve.png) |
| **In Out Expo** | ![In Out Expo curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cb51ce5-19f0-4642-9ccf-2a9b6581096d/in-out-expo-curve.png) | **In Out Elastic** | ![In Out Elastic curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/414127cd-2a31-4a3b-8650-6c5eb15d08da/in-out-elastic-curve.png) |
| **In Out Circ** | ![In Out Circ curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0426235d-c509-4413-97d7-c654c41e03fd/in-out-circ-curve.png) | **Random** | ![Random curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27ec901f-3952-44f6-b425-56f815208e40/random-curve.png) |

Depending on the shape of the effector, the boundary description will differ, either as inner / outer radius, or inner / outer extent. See specific shape options below for details.

You can control the color and transparency of the boundaries in your **Project Settings**, under **Motion Design - Cloner & Effector**. You can set the color with the Color Picker, or manually set the RGBA values. The alpha channel (A) controls the transparency of the wireframes, from 0.1 (most transparent) to 1 (least transparent).

![Motion Design effector color settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6a0e2ce-6fc5-47d9-9a48-ff40aa5831e5/image_125.png)

#### Invert Type

An important setting shared across all of the Shape properties is the **Invert Type** option at the bottom of the list. Enabling this property inverts the affected area.

![Invert Type setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b90aa19e-a7c5-4069-aea6-0cc52053d866/image_126.png)

The example below shows an effector using a sphere shape before inverting. The effect is contained within the boundaries of the effector, attenuating to nothing at the edge of the outer boundary.

![Sphere shape example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/680d587a-9cc2-4688-9e3a-493dd7d61f86/image_127.gif)

After inverting, the example now shows the effects are reversed. The effector's influence is at full strength outside the boundaries, attenuating across the outer boundary volume and having no effect on the inner boundary volume.

![Sphere shape inverted example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2949113c-3f5b-4055-837e-ca79a3f7baf5/image_128.gif)

#### Sphere

This shapes the effector into a sphere that has customizable properties for the **Inner / Outer** boundaries. Any clone that falls outside of the **Outer** boundary is not influenced by the effector. You can set the **Easing** property as described previously.

![Effector Sphere shape example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edffc2c8-6f5c-481e-ab42-fa50ebd33ca0/image_129.png)

Below is a clearer example of the Sphere shape boundary when the mode is changed from **Noise Field** to **Offset**.

![Effector Sphere shape Offset mode example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2aa0021b-025a-43a6-95c2-93f84d81bc9e/image_130.png)

The image below shows the Mode settings we used for this change in the example above.

| **Property** | **Value** |
| --- | --- |
| **Mode** | Offset |
| **Offset Z** | \-262.70 |
| **Rotation Y** | 90.0 |
| **Scale X** | 1.0 |
| **Scale Y** | 1.0 |
| **Scale Z** | 1.0 |

![Effector Sphere shape Offset mode settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15f3113a-aeef-44b4-8b0f-fd86f1a0a0b8/image_131.png)

| **Sphere Shape Properties** | **Description** |
| --- | --- |
| **Inner Radius** | Defines the boundaries of the inner area of influence for the effector using a sphere shape. |
| **Outer Radius** | Defines the boundaries of the outer area of influence for the effector using a sphere shape. |
| **Invert Type** | Inverts how the shape modifies the effector's influence. |

#### Plane

Passing this effector shape through the cloner will interpolate between minimum and maximum values of the mode selected along the curve selected under the **Easing** setting. The effector has two handles that represent what happens before and after the effector passes through the space.

![Plane shape Noise field example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a47de321-e45a-4838-bc2d-27fbf7cca8ba/image_132.png)

Lowering the value of **Plane Spacing** reduces the space between the two handles, and the effect will have a less gradual curve.

When using the Plane shape, you must select one of the Easing property curve options. The default setting is the Linear curve option.

![ Effector Plane shape default linear curve example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e2a3edd-85e8-44f3-ad8f-1ee5783f097c/image_133.gif)

| **Plane Shape Properties** | **Description** |
| --- | --- |
| **Plane Spacing** | Determines the space between the two plane handles. |
| **Invert Type** | Inverts how the shape modifies the effector's influence. |

#### Box

This shape restrains the effector's influence using the **Inner Extent** and **Outer Extent** properties, which use the X, Y, and Z axes to define rectangular cuboid volumes. The Box shape draws a bounding box to indicate where the effect is present. Much like the other Effector Shape options, you can set the Easing property.

![Effector Box shape example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/831ed77a-13f3-45d5-8a1e-fdd937d552aa/image_134.png)

Inverting the previous example results in the image below.

![Effector Box shape inverted example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90585bc4-a33a-4af0-b27d-23b9bebea900/image_135.png)

| **Box Shape Properties** | **Description** |
| --- | --- |
| **Inner Extent** **X / Y / Z** | Defines the boundaries of the inner area of influence for the effector using a box shape, on the respective axes. |
| **Outer Extent** **X / Y / Z** | Defines the boundaries of the outer area of influence for the effector using a box shape, on the respective axes. |
| **Invert Type** | Inverts how the shape modifies the effector's influence. |

#### Unbound

This option places no shape restraints on the effector. This shape does not have boundaries, nor does it use the Easing property, unlike the other options.

![Effector Unbound shape example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0606dda5-1654-41d9-9c0f-aeab3ebea594/image_136.png)

#### Radial

When using the Radial shape, you can set the **Radial Angle**, which you can increase up to a full circle with a hollow center. The center is defined by the **Radial Min Radius** and **Radial Max Radius** properties. You can use the standard Easing property options to define how the Radial shape changes.

The example below shows the Radial Angle property using the In Out Back curve Easing option. This option makes the Radial shape start low and curve upward.

![In Out Back curve setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c919453d-85b1-4dfe-8b5d-d8a5df7287dc/image_137.png) ![Effector Radial shape example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5a68c74-a081-4c57-80f3-8aa1cbcfb974/image_138.gif)

The following GIF shows an example of manipulating the Radial Min Radius and Radial Max Radius to customize the inner and outer thickness of the ring.

![Effector Radial shape modify inner and outer thickness example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c3c9fad-306d-4e0c-acba-f461de4892e0/image_139.gif)

For this example, the **Invert Type** property instead pushes the shape area down into the floor.

![Effector Radial shape inverted example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ebcfcce-f001-44cb-9831-cd2c4a6e36d1/image_140.gif)

| **Radial Shape Properties** | **Description** |
| --- | --- |
| **Radial Angle** | Determines the arc of the radial shape. Can extend to a full circle at 360 degrees. |
| **Radial Min Radius** | Determines the radius of the minimum (inner) boundary of the Radial shape. |
| **Radial Max Radius** | Determines the radius of the maximum (outer) boundary of the Radial shape. |
| **Invert Type** | Inverts how the shape modifies the effector's influence. |

#### Torus

When using the Torus shape option, you can control the radius of the main torus, as well as the radius of both the inner and outer boundaries.

![Effector Torus shape example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5a9fcde-c8cf-41da-a258-fea50818f197/image_141.gif)

You can use the Torus Radius property to expand the size of the torus while still remaining an equal thickness. Below is an example.

![Effector Torus shape changing radius example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11f9d21b-ccb2-400a-979d-26e63191efdd/image_142.gif)

| **Radial Shape Properties** | **Description** |
| --- | --- |
| Torus Radius | Determines the radius of the entire Torus shape. |
| Torus Inner Radius | Determines the radius of the Torus inner boundary. |
| Torus Outer Radius | Determines the radius of the Torus outer boundary. |
| Invert Type | Inverts how the shape modifies the effector's influence. |