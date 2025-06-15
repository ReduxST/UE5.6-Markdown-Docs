# Automotive Configurator Sample

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/automotive-configurator-sample-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/automotive-configurator-sample-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:30

---

The automotive industry is increasingly turning to real-time solutions, such as Unreal Engine (UE), to drive their visualization and commercial projects. The **Automotive Configurator** sample is built using Epic Games' best practices for the creation of a vehicle configurator, a common use case for 3D visualization artists in the automotive industry.

The Automotive Configurator sample demonstrates the use of the following features:

-   [Variant Manager](/documentation/en-us/unreal-engine/variant-manager-template-overview)
-   [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine)
-   [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine)
-   [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine)
-   [Chaos Cloth Solver](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine)
-   [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine)
-   [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)
-   [Movie Render Queue](/documentation/404)

## How To Use the Automotive Configurator

### Downloading the Sample

To create a project with the Automotive Configurator sample, follow these steps:

1.  Access the [Automotive Configurator](https://fab.com/s/f54cb8fd6f65) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    1.  Alternatively, you can search for the sample project from the Fab plugin for UE.
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.
    
4.  Download the [Automotive Materials](https://fab.com/s/da380b9a6082) and [Automotive Salt Flats](https://fab.com/s/db62e7a8704a) assets from Fab.

To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).

This project requires the following plugins (enabled by default):

-   **Movie Render Queue**
-   **Color Correct Regions**
-   **Control Rig**
-   **Variant Manager**

This may require you to restart the Editor.

### Navigating the User Interface

The Automotive Configurator is built using the [Product Configurator](/documentation/en-us/unreal-engine/product-configurator-template-in-unreal-engine) template as a base. Using the [Variant Manager](/documentation/en-us/unreal-engine/variant-manager-template-overview), you can choose from a variety of saved Static Mesh configurations called **Variants** to customize your Audi A5.

You can control the configurator using the interface buttons located at the bottom of the screen:

| **Number** | **Description** |
| --- | --- |
| **1** | Configurator Mode |
| **2** | Commercial Mode |
| **3** | Car Paint Color |
| **4** | Wheel Style |
| **5** | Trim Color |
| **6** | Leather Color |
| **7** | Seat Upholstery Style |
| **8** | Toggle Path Tracer |
| **9** | Take Screenshot |
| **10** | Mute/Unmute |
| **11** | Camera Views |

The Automotive Configurator also includes focus points, represented by white flashing circles. These have been animated using [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine), Unreal Engine's Blueprint-based animation control system:

-   **Open/Close Doors**: Open and close the car doors.
-   **Open/Close Convertible Soft Top**: Open and close the convertible top by clicking on the roof control switch located by the rearview mirror in any of the interior views.
-   **Open/Close Trunk**: Open and close the trunk lid.
-   **Horn**: Honk the horn.
-   **Start/Stop the Engine**: Click the Engine Start button to start or stop the engine. When the engine is started, the dash gauges and Audi Virtual Cockpit are powered and the front lights and tail lights are lit up.

### Rendering the Commercial View

Clicking the **Play** button in the Configurator will transport your customized vehicle to the Commercial mode.

In Commercial mode, your vehicle becomes the star of your very own TV spot. This takes your vehicle through several camera shots often seen in car commercials. You can control the commercial using the following interface options:

| **Number** | **Description** |
| --- | --- |
| **1** | Stop |
| **2** | Play |
| **3** | Pause |
| **4** | Render Video |

Powered by [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview), the camera races across the salt flats, moving to highlight the wheels and interior. The car commercial takes advantage of [Ray Tracing](/documentation/en-us/unreal-engine/ray-tracing-and-path-tracing-features-in-unreal-engine) for real-time lighting and shadows, and can be saved to your computer thanks to the [Movie Render Queue](/documentation/404) runtime feature. Optional Path Tracer use

## Variant Manager

The Automotive Configurator is built on the Product Configurator template and uses the Variant Manager to store the various asset configurations used to customize your vehicle.

  ![Walnut trim](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e266fdbb-da0e-4c8c-8ec2-adcbe0d6b540/variant-manager-walnut.png "Walnut trim") ![Gray trim](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f3c5cbe-12f4-4bf3-a718-06309f461d33/variant-manager-grey.png "Gray trim") ![Carbon fiber trim](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/651767ab-5f2d-4ead-9665-b4b4a6f16c20/variant-manager-carbon.png "Carbon fiber trim")

**Move the slider to see the different Trim variants**

Each configuration option is stored in an entry called a **Variant**. Each variant points to a property on an Actor that is changed when the variant is activated. Variants are arranged into Variant Sets and the data is used by the **BP\_Configurator** Blueprint to populate the user interface with options. In the image above, you can see that when different trim options are selected the Variant Manager applies that value to different static mesh components on the vehicle Actor.

For more information on using the Variant Manager, please see the [Variant Manager](/documentation/en-us/unreal-engine/variant-manager-template-overview) documentation.

## Lumen Global Illumination and Reflections

Unreal Engine uses the [Lumen Global Illumination and Reflection](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) system to provide dynamic global illumination and shadows.

The Automotive Configurator sample uses Lumen's ability to provide diffuse interreflection and indirect specular reflection to accurately reflect the salt flats environment off the tire rims and car, making the most of the Clear Coat properties of the Materials used from the Automotive Materials pack.

For more information on lighting your level with Lumen, see the [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) documentation.

## Path Tracer

[Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine) is Unreal Engine's progressive, hardware-accelerated rendering mode. Designed to generate physically correct global illumination and reflection and refraction of materials, enabling Path Tracer can provide you with photorealistic renders with little to no additional setup.

![Audi A5 illuminated using Lumen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a06615d-4b1f-4ecb-99ec-d7485c37130c/lumen-sample.png)

![Audi A5 illuminated using Path Tracer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95f97f17-f74f-4361-b398-cace4ceb6d31/path-tracer-sample.png)

Path Tracer features full integration with [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) and [Movie Render Queue](/documentation/404) making it ideal for Film and TV quality render outputs.

The Automotive Configurator sample gives you the option to toggle path tracing on from the interface to provide photorealistic output for screen captures or rendering during Commercial mode.

For information on using Path Tracer in your own projects, see the [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine) documentation.

## Volumetric Clouds

The [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) found in the sample use a physically-based cloud rendering system and a material-driven approach to create the sky that is seen on the salt flats.

The Epic Games team uses volumetric clouds to bring aesthetic touches to the salt flats, while also getting bounced light reflection on the car paint. The Volumetric Cloud component uses a Material Instance of the default cloud Material to accomplish these effects.

For more information on using the Volumetric Clouds system, please see our [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) documentation.

## Chaos Cloth Solver

The Automotive Configurator sample uses the [Chaos Cloth Solver](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine) to simulate the physics interactions of the cloth convertible top.

![Chaos cloth sim on the Audi A5 soft top](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e7670f2-a840-411d-b512-c4742b48fb38/cloth-sim.gif)

Using the Cloth Painting workflow directly in the Engine, the Epic Games team is able to assign a variety of properties such as friction, constraints, drag, and stiffness to closely simulate the look and feel of the Audi A5's canvas soft top.

For more information on the Chaos Cloth Solver and in-engine Clothing Tool, please see the [Clothing Tool](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine) documentation.

## Control Rig

The [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) system is a scriptable node-based rigging system that provides rigging and animation tools directly in the engine.

In the Automotive Configurator, the Epic Games team uses Control Rig in two ways. The first is to create an adaptable skeletal mesh version of the car and create the animations for the wheels, doors, and trunk. The second is to create the animation for the convertible top.

The Audi A5 uses a skeleton with pivot locations for each movable element in the car. With this method, the main vehicle geometry does not need to be bound to the vehicle, and the skeletal mesh can be imported into Unreal quickly. Once imported, the mesh is added to a Blueprint, which attaches the rest of the vehicle components to the pivots and binds the skeleton to the Control Rig at runtime. This makes it easier to update the pivot locations if needed without having to go back to our DCC application.

Due to its complexity, the cloth convertible top is a separate piece with its own skeleton and Control Rig. A state machine tracks if the top is open or closed, and runs the correct transition animation when it is selected in the configurator application.

For more information on using Control Rig to animate in-engine, please see the [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) documentation.

## Sequencer

Powering the Commercial mode, [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) is a robust keyframe animation system which you can use to create in-game cinematics.

The Commercial mode uses a series of level sequences with animated cameras to showcase various configurable features on the car. The Epic Games team then uses **Movie Render Queue** to render and save the level sequences and assemble them using a non-linear editing program. This edited sequence is brought back into Unreal as a master sequence, where audio is added and the cameras, animation, and overall timing is refined. These sequences are found in the **CarConfigurator/Commercial/Sequences** folder.

For more information on using Sequencer in your projects, please see the [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) documentation.

## Movie Render Queue

Used to output the final commercial render, [Movie Render Queue](/documentation/404) is an engine feature that can export high-quality media. When used with Real-Time Ray Tracing, the final render can take advantage of advanced anti-aliasing, radial motion blur, and reduced noise in ray tracing:

The Epic Games team uses Blueprint to enable Movie Render Queue at runtime. With this, you can render and save a video of your commercial directly from the configurator.

For more information on using the Movie Render Queue feature, please see the [Movie Render Queue](/documentation/404) documentation.

## Adding Art Assets to the Configurator

You can add new art assets to the Automotive Configurator by adding a new variant to the Level Variant Set. This process is similar for both Materials and Static Mesh assets. The example below describes how to add a new paint color to the configurator.

The Audi A5 in this sample makes use of the [Automotive Materials Pack](https://www.fab.com/listings/5dd132fe-ee32-4e8c-9cd3-7496547dfb29) for paint, leather, and trim options. To add additional colors to the interface, follow these steps:

1.  Create a custom folder to hold your new Material and any texture samples that it may need. Do this by right clicking on the **CarConfigurator** folder and selecting **New Folder**. Name the new folder **Custom**.
2.  If you are not adding a color that is already available within the sample, you will need to either create your paint sample using the tools available within the [Automotive Material Pack](/documentation/en-us/unreal-engine/automotive-materials-pack-in-unreal-engine), or import and set up your Material. For this sample, you are duplicating an existing paint sample and editing it. For more information on importing textures and creating new Materials, see our [Material How-To](/documentation/en-us/unreal-engine/unreal-engine-materials-tutorials) documentation.
3.  Next, open the **CarConfigurator/Shared** folder and double click on the **CarVariants** Level Variant Set to open it in the Variant Manager.
    
4.  To make sure that your new color is applied to all the required static meshes, you can duplicate an existing Variant. Open the **Paint, Trim**, or **Leather** Variant Sets and right click on the last variant in the list. From the menu, choose the **Duplicate** option.
    
5.  Right click on your new variant and choose **Rename**. Create a new name that is appropriate for the color.
    
6.  Click the **BP\_AudiA5** in the **Properties** panel to display the **Properties** and **Values** for the car. For each value in the Values column, click the drop down menu and select your new color, excluding the **SM\_trunkDetails** Material.
    
    Changing the Material for **SM\_trunkDetails** changes the license plate on the car.
    
7.  Set the thumbnail image for your new variant by switching on the variant and positioning the **Viewport** camera to best display your new option.
    
8.  Then right click the variant in the **Variant Manager** choose the **Set from viewport** option.
    
9.  Test the sample by clicking the **Play** button in the Editor. Your new variant should appear in the user interface.