# City Sample

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/city-sample-project-unreal-engine-demonstration](https://dev.epicgames.com/documentation/en-us/unreal-engine/city-sample-project-unreal-engine-demonstration)  
**Processed:** 2025-06-14 16:13:30

---

The City Sample project is a playground where designers and developers alike can explore how various new and improved systems are brought together to create expansive and engaging environments. This sample is built using the same assets and design techniques used in [The Matrix Awakens: An Unreal Engine 5 Experience](https://www.unrealengine.com/wakeup) technical demo released on PlayStation 5 and Xbox Series S|X hardware.

The new and improved features of Unreal Engine 5 enable you to build large, highly-detailed worlds that are brought to life with Mass AI and fully dynamic lighting. The city is designed and built using procedural generation using the Rules Processor.

The following features are used in this sample project:

-   World Partition works in conjunction with One File Per Actor to improve level streaming and editor workflow efficiency.
-   Nanite enables the use of high-fidelity virtualized micropolygon geometry.
-   Lumen generates dynamic global illumination and reflections using Hardware Ray Tracing.
-   The Virtual Shadow Maps system provides consistent, high resolution shadowing for the city.
-   Mass AI manages the behavior and visualization of traffic and crowds based on the MetaHuman library.
-   Chaos physics drives the vehicle and the destruction systems.
-   The MetaSounds system fills the city with urban sounds.
-   Niagara is used for particle systems.
-   And more!

## Accessing the City Sample Project

To create a project with the City Sample project, follow these steps:

1.  Access [City Sample](https://fab.com/s/5e8f5eda64d8) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    1.  Alternatively, you can search for the sample project from the Fab plugin for UE.
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.

To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).

### Recommended System Specifications

The City Sample is a graphically intensive project that requires a powerful video card and system to run at a stable framerate. It is recommended to install the project on a solid state drive (SSD), Nanite and Virtual Shadow Maps depend on fast speeds for the best possible performance.

-   Windows 10 with support for DirectX 12
-   12-core CPU at 3.4 GHz
-   64 GB of System RAM
-   GeForce RTX-2080 / AMD Radeon 6000 or higher
-   At least 8 GB of VRAM

This sample project requires that your machine have up-to-date graphics drivers and DirectX 12. Nanite and Virtual Shadow Maps require DirectX 12.

On lower spec systems, you can adjust the viewport screen percentage setting to get better performance by reducing the resolution of the Level Editor viewport. You can set this in the **Viewport Options** located in the upper-left corner of the editor viewport using the **Screen Percentage** slider.

![setting screen percentage in the level viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b63723e3-c62e-4ac4-81da-e0fecd579dfc/setting-screen-percentage.png)

## Navigating the City Sample Project

When you open City Sample, you are greeted by the **Startup** map that provides some on-screen information for using this sample project and its recommended system requirements. The project includes two maps: a big city and a small city. Select one of these maps to open from the Content Browser in the **Content > Map** folder.

-   The **Big City** (Big\_City\_LLV) map is the same one generated for [The Matrix Awakens](https://www.unrealengine.com/wakeup) technical demo. This particular map is resource intensive and may not perform well on machines with lower than recommended specifications. It's roughly 4 kilometers by 4 kilometers in size.
-   The **Small City** (Small\_City\_LVL) is a smaller city generated using the same assets and configurations as the larger one. It is designed to showcase all of the rendering, physics, artificial intelligence, sounds, and gameplay features as the larger city.

The City Sample is a showcase for developing and designing worlds using World Partition and Data Layers. Unlike Unreal Engine 4, there are no sub-Levels that would traditionally be used to load in objects. Instead, World Partition loads them on-demand, and breaks up the scene into separate, editable parts.

When you load either city level, you'll find the **World Partition** window is docked on the right side of the editor viewport, and displays a simplified map of the world.

![World Partition Window with world map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/995115eb-b87e-4881-a4fe-524bc2c3d6f1/world-partition-window.png)

Part of the World Partition tools is the **Data Layers Outliner** that provides a listing of data layers that contain objects that make up the scene. The Data Layers Outliner can be opened from the main menu under **Window > World Partition > Data Layers Outliner**.

The Data Layers can be disabled as-needed from this window. Use the **Visibility** (eye) icon next to a listed layer to stop it from being rendered, or, to disable that layer completely, use the checkbox.

![World Partition Data Layers Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51a4b304-f520-4799-98c7-a6c7d86f1198/wp-data-layers-outliner.png)

When a Data Layer is selected, the properties are displayed in the bottom portion of the window.

![World Partition Data Layers Outliner with properties shown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8530704d-a031-4cd1-bbcf-0aa63e9f34a8/wp-data-layers-outliner-2.png)

When opening the Small City for the first time, you'll notice that it's ready to go and all assets are loaded. However, when opening Big City, none of the cells are loaded. You'll want to use the World Partition window in the editor to do that. Right-click on any single cell, or use the mouse to left-click and drag to select multiple cells before right-clicking. Then, choose **Load Selected Cells**.

You can quickly navigate the map by double-clicking on any cell in the World Partition window to move the camera to that location on the map.

### City Sample In-Game Controls

The City Sample is a playable experience where players walk, drive, and fly around the city. You can use a keyboard and mouse or gamepad. Below are the controls for each.

#### Walking Controls

| Item Name | Controller | Keyboard and Mouse |
| --- | --- | --- |
| **Move Forward** | Left Joystick | W |
| **Move Backward** | Left Joystick | S |
| **Move Left** | Left Joystick | A |
| **Move Right** | Left Joystick | D |
| **Look** | Right Joystick | Mouse Move |
| **Menu** | Start or Options Button | O |
| **Enable Flying Mode** | Y | X |
| **Sprint** | Right Bumper | Left-SHIFT or L-SHIFT |
| **Dismiss Controls** | X | Z |

#### Driving Controls

| Item Name | Controller | Keyboard and Mouse |
| --- | --- | --- |
| **Throttle** | Right Trigger | W |
| **Brake/Reverse** | Left Trigger | S |
| **Steer Left** | Left Joystick | A |
| **Steer Right** | Left Joystick | D |
| **Look** | Right Joystick | Mouse Move |
| **Handbrake** | B | Spacebar |
| **Enter/Exist Vehicle** | A | C |
| **Menu** | Start or Options Menu | O |
| **Dismiss Controls** | X | Z |

#### Flying Controls

| Item Name | Controller | Keyboard and Mouse |
| --- | --- | --- |
| **Move Forward** | Left Joystick | W |
| **Move Backward** | Left Joystick | S |
| **Move Left** | Left Joystick | A |
| **Move Right** | Left Joystick | D |
| **Look** | Right Joystick | Mouse Move |
| **Altitude Up (Ascend)** | Right Trigger | E |
| **Altitude Down (Descend)** | Left Trigger | Q |
| **Speed Up** | Right Bumper | F |
| **Speed Down** | Left Bumper | R |
| **Menu** | Start or Options Button | O |
| **Enable Walking Mode** | Y | X |
| **Dismiss Controls** | X | Z |

#### Menu Navigation Controls

| Item Name | Controller | Keyboard and Mouse |
| --- | --- | --- |
| **Menu Navigation** | Left and Right Bumper | \[ and \] |
| **Menu Item Navigation Up** | D-pad Up | Up Arrow |
| **Menu Item Navigation Down** | D-pad Down | Down Arrow |
| **Adjust Settings** | D-pad Left and D-pad Right | Left Arrow and Right Arrow |

#### Photo Mode Controls

| Item Name | Controller | Keyboard and Mouse |
| --- | --- | --- |
| **Move Forward** | Left Joystick | W |
| **Move Backward** | Left Joystick | S |
| **Move Left** | Left Joystick | A |
| **Move Right** | Left Joystick | D |
| **Look** | Right Joystick | Mouse Move |
| **Altitude Up (Ascend)** | Right Trigger | E |
| **Altitude Down (Descend)** | Left Trigger | Q |
| **Reset Camera** | Y | \- |
| **Auto Focus (Hold)** | A | X |
| **Close Menu** | Start or Options Button | O |
| **Hide User Interface** | X | Z |

### City Sample In-Game Menu Options

After opening the in-game **Menu**, a user interface will appear in the bottom right corner of the screen. It includes options to change the lighting, the crowd and traffic densities, and enable visualization options for features like Nanite. It also includes a dedicated photography mode with common camera features like exposure, aperture, and depth of field settings.

You can navigate the menus using the keyboards **Left / Right Bracket** keys or if you're using a controller, use the **Left / Right Bumpers**. The following in-game menus are available.

#### Photo Mode Menu

The **Photo Mode** menu contains Camera and Focus settings to configure exposure, aperture, and focus.

![In-Game Photo Mode Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/067c6ba9-686b-4765-b81c-bd46e3af4745/menu-photo-mode.png)

| Menu Setting | Description |
| --- | --- |
| Camera |   |
| **Exposure Compensation** | Adjusts the exposure of the rendered frame to be brighter or darker. |
| **Aperture** | Changes the size of the opening for the camera lens. Lower f-stop values increase the amount of light coming into the opening of the lens, which can increase focus to create depth of field. |
| **Focal Length** | Sets the angle of view used by the camera. Larger focal lengths capture less of the scene but enlarge objects further away and increase depth of field. Smaller focal lengths capture more of the scene but decrease the amount of depth of field that occurs. |
| Camera |   |
| **Focus Distance** | Sets the shortest distance in which the lens can focus the image. |

#### World Settings Menu

The **World Settings** menu contains various settings that affect lighting, density of crowd, traffic, and parked vehicles, and various visualization options.

![In-Game World Settings Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e644b02b-2773-4e30-a86b-fef34c605075/menu-world-settings.png)

| Menu Setting | Description |
| --- | --- |
| Simulation |   |
| **Night Mode** | Toggles between daytime and nighttime lighting. |
| **Sun Rotation** | Sets the degree angle the sun is rotated. |
| Density |   |
| **Crowd** | Sets the density of the crowds that populate the city streets. |
| **Traffic** | Sets the density of the traffic that populates the city streets. |
| **Parked Cars** | Sets the density of the cards parked alongside the city streets. |
| Visualizations |   |
| **Crowd & Traffic** | Toggles a visualization mode that replaces parked cars (blue), driving cars (green), and individuals in a crowd (white). |
| **Post-processing Filter** | Toggles a post processing filter similar to the one used in the Matrix: Awakens technical demo. |
| **Nanite View** | 
Toggles between the different visualization modes of Nanite.

-   **Default** is the game view.
-   **Primitives** are the number of which have Nanite enabled for them.
-   **Instances** applies a different color for each individual instance of a Static Mesh in the scene.
-   **Clusters** displays colored representations of all groupings of triangles being rendered in the current scene view.
-   **Triangles** displays all triangles of the Nanite meshes that make up the scene.
-   **Material ID** applies a separate color for each material of a Nanite primitive.



 |

#### Controller Settings Menu

The **Controller Settings** menu displays the controller button mappings for walking, driving, drone, and photo modes. The menu also contains settings for camera control with look sensitivity and inverting the vertical axis.

![In-Game Controller Settings Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3108ceba-57be-4669-9f27-47d45f047fcd/menu-controller-settings.png)

| Menu Setting | Description |
| --- | --- |
| Camera Control |   |
| **Haptic Feedback** | Toggles haptic feedback vibration while playing. |
| **Invert Vertical Axis** | Inverts the vertical axis of movement. |
| **Look Sensitivity** | Adjust the sensitivity scale applied to the camera movement when looking around. |

Changes to these settings also affect Keyboard and Mouse.

## High-End Visuals

The City Sample demonstrates Unreal Engine 5's high-end visuals for building large open worlds.

The City Sample requires DirectX 12 for its high-end visuals. Some features work in a limited capacity or not at all with systems that don't meet the [Recommended System Specifications](/documentation/en-us/unreal-engine/city-sample-project-unreal-engine-demonstration#recommendedsystemspecifications) of this project.

### Lumen Global Illumination and Reflections

Lumen is used to provide dynamic global illumination and reflections across the city. Lumen provides dynamic, photorealistic lighting for scenes with many areas being indirectly lit. It adapts to changes in direct lighting and geometry, combining new and old techniques to achieve high-quality results within real-time budgets.

Lumen is built with the next-generation consoles and high-end PCs in mind.

![Lumen Global Illumination and Reflections: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ae87fe1-a08d-42cf-91cd-f5655f89bb34/lumen-enabled.jpg)

![Lumen Global Illumination and Reflections: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/296454b0-919f-4a5d-b39c-a4bee53d5de9/lumen-disabled.jpg)

The City Sample uses [Hardware Ray Tracing](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#hardwareraytracing), which supports a larger range of geometry types such as skinned meshes. Hardware Ray Tracing also scales up better to higher qualities since it intersects against the actual triangles of geometry and has the option to evaluate lighting at the ray hit instead of the lower quality surface cache.

For Static Meshes using Nanite, Hardware Ray Tracing can only operate on the Fallback Mesh generated from Nanite's **Fallback Triangle Percent** in the Static Mesh Editor. Screen Traces are used to cover the mismatch between the full triangle mesh rendered by Nanite and the fallback mesh being ray traced by Lumen.

Lumen works with all movable light sources, including emissive materials as light sources. Skylighting uses Lumen's Final Gather for sky shadowing, which allows for indoor areas to be much darker than outdoor areas, and that helps bring out lightly colored surfaces that reflect more light. The City Sample is being lit by only Directional Light, Sky Light, and Emissive Materials from surfaces.

![Lumen Global Illumination and Reflections | Daytime Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f8d0430-c66a-466b-817d-b4eae4ca1890/lumen-day.png)

![Lumen Global Illumination and Reflections | Nighttime Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc2069f2-2042-40c9-b7e4-330753b2218a/lumen-night.png)

While you explore the city in-game, use the menu to access the **World Settings** where you can adjust the **Sun Rotation**. Or, while working in the editor, you can use the keyboard shortcut **Right Ctrl + L** and drag your mouse to move the Directional Light around.

For more information and details about how it works, see [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) and [Lumen Technical Details](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine).

### Nanite Virtualized Geometry

Nanite virtualized geometry is used on all of the Static Meshes in the City Sample, and none make use of traditional [levels of detail](/documentation/en-us/unreal-engine/creating-levels-of-detail-in-blueprints-and-python-in-unreal-engine). Nanite renders pixel scale detail and handles high object counts by intelligently doing work on only the detail that can be perceived, and no more. It does for geometry what [Virtual Texturing](/documentation/en-us/unreal-engine/virtual-texturing-in-unreal-engine) does for texture detail.

Nanite's internal mesh format and rendering technology means that its representation changes dynamically as you move through the world, updating the level of detail on the fly and culling parts that aren't rendered on screen. Objects closer to the player camera receive more detail, while further objects receive less, all the while keeping on screen detail uniform.

![Examples of Nanite's quality](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f05ad0e-e516-4577-95a1-a9d8a4629e47/nanite-examples.png)

The City Sample is made up of billions of polygons from tens of thousands of objects placed throughout the world. Nanite makes it possible to use film-quality assets in real-time with little to no additional setup other than enabling Nanite on the Static Mesh. It's even possible to drop a high-polygon ZBrush sculpt directly in game.

Use any one of the visualization modes that Nanite offers to see how it renders the scene. You can select from the list of visualization using the **View Modes** menu under **Nanite Visualization** rollout menu.

![Nanite Visualization Modes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac2a993a-29b0-44c9-bd03-b0970215e866/nanite-vis-modes.png)

Nanite's Overview visualization mode.

For more information about how to use and configure Nanite for your own projects, see the [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) documentation.

### Temporal Super Resolution

The geometric detail and fidelity required for large, open worlds with thousands to millions of instances totaling billions of polygons have increased the demands of games developed for next-generation consoles and high-end PCs. That level of fidelity can mean that games can consume a significant amount of their performance budgets before including rendering a frame at native 4K resolution.

**Temporal Super Resolution** (TSR) is an anti-aliasing method built to meet the fidelity demands of large, densely populated worlds. It uses a platform-agnostic temporal upscaling algorithm by taking a lower input resolution and outputting rendered frames at quality near 4K resolution. This means that you can increase performance without rendering native 4K but still achieve quality that rivals 4K from rendered lowerer resolutions.

In the comparison below, you can see the quality and performance differences between captured frames rendered at native 4K and one rendered at 1080p that has been upscaled to 4K. Temporal Super Resolution makes it possible to achieve image quality near native 4K resolutions while reducing GPU frame time by nearly half in this shot from City Sample.

![4K frames rendered at Native 4K resolution | Frame Time: 57.50 ms  ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abbd6327-201e-4288-93c9-93ec14a38118/tsr-native-4k.png)

![4K frames rendered at 1080p resolution (r.ScreenPercentage=50) | Frames Time: 33.37 ms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1480f88e-a49b-4cbe-a898-2addd7f4f93d/tsr-4k-upscale.png)

You can right-click and save each of the images in the comparison slider at their full-resolution to inspect the quality similarities.

### Virtual Shadow Maps

**Virtual Shadow Maps** (VSM) is Unreal Engine 5's new shadow mapping method used to deliver consistent, high-resolution shadowing that works with film-quality assets and large, dynamically lit open worlds that use Nanite, Lumen, and World Partition features.

Traditional dynamic shadowing techniques have often been limited to small and medium-sized worlds, forcing designers and artists to sacrifice quality for performance. By contrast, Virtual Shadow Maps offer a single unified shadowing method that automatically applies quality where it is needed most. Shadows can now have consistent quality for small and large objects over greater distances — with realistic soft penumbra and contact hardening.

In the comparison below looking down on the cityscape, you can see the quality and consistency differences that Virtual Shadows have over Cascaded Shadow Maps. With Virtual Shadow Maps, the entirety of the city is shadowed in a consistent way from large to small detail. Small parts of the building, like the spires and equipment on the rooftops are captured in fine detail, even the cars and larger objects on the ground in the distances have shadows.

Compare that with Cascaded Shadow Maps where you must decide where in the scene you want to have that detail. Shadows maps are not well-suited for high quality detail over large areas without incurring significant performance cost. Note how shadows in the distance are not sharp and shadowing on the ground appears to just shade everything rather than individual objects.

![Virtual Shadow Maps ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5a3df6d-127e-48ed-95cf-da2e678587e4/shadow-vsm.png)

![Cascaded Shadow Maps](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5c68948-0790-4b33-8dec-de714883d6a9/shadow-csm.png)

See the [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) documentation to learn more about how to use and configure it for your own projects.

### Post Processing Local Exposure

**Local Exposure** is a new technique developed for Unreal Engine 5 that automatically applies local adjustments to exposure — within artist-controlled parameters — to preserve both highlight and shadow detail, on top of the existing global exposure system. It's not uncommon to have scenes with challenging high dynamic ranges using dynamic lighting in which applying a single global exposure adjustment is simply not enough to avoid having blown out highlights and completely dark shadows.

In games with a dynamic time-of-day system or like City Sample where you can change the lighting dynamically, scenes can easily be under or over-exposed in parts of the rendered image. Take for example the scene below, the sun lit area is very bright and the area under the bridge, without using Local Exposure adjustments, is very shadowed. Local Exposure helps achieve more consistent results when carefully crafted lighting per-scene is not feasible, like in City Sample where players can explore the environment at will.

![Post Processing with Local Exposure](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87df8ada-595c-4a4c-9af7-fd9e85799198/ppv-local-exposure.png)

![Post Processing with only Exposure ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7dd94d0b-6ffb-4a31-a121-4cd7d3c82ef4/ppv-exposure-only.png)

## Procedurally Generated and Populated City

The City in the City Sample project has been designed and created with procedural generation using SideFX's Houdini software extensively to build all aspects of the city, from the shape of the city island to all the parts in between for the roads and highway, buildings, sidewalks, street furniture, and more. The "generation" of the city happens only inside Houdini using custom tools and inputs provided by the user.

The result — a huge point cloud — is exported from Houdini and imported into Unreal Engine 5 where the **Rule Processor** — an Unreal Engine tool developed for this project — converts the point clouds into thousands of instances.

When Epic games developed The Matrix Awakens, it was known that the project would be an open world city that would need to be fully detailed and very large. This project is using many new features of Unreal Engine 5 and at the time of its development, it was known that many other departments would be creating content and they would need to be able to simultaneously work together. The relatively small size of the environment team and the amount of detail being targeted for the project meant two things: Nanite would remove typical polygon budget limits, and modular assets would be needed that could be instanced thousands of times across the world.

Houdini is used to handle all the upfront work of generating the city shape, the road networks, connecting freeway system, building placement and provides a ton of metadata that can be used in Unreal Engine 5 to procedurally generate the final city. Using these tools in Houdini enabled an infinite number of different cities to be generated in a short period of time by the designers.

The generated city data contains all sorts of metadata that can be used by other tools in the Unreal Engine 5, including the Artificial Intelligence system that drives the traffic and crowd simulations. Buildings are constructed from a volume. The building generator uses a shape grammar language to style the building volume. Each different building style has a different set of rules. A given volume can also be split into two different styles: one for the bottom of the building and one for the remaining top section.

The City Sample project includes the source files needed to procedurally generate your own city using Houdini and Houdini Engine. You will need a license from SideFX in order to use the City Building Generator asset in the engine with Houdini. The Houdini source files are located in the CitySample root folder and are named `CitySample_HoudiniFiles.zip`.

The City Sample was developed using the following versions:

-   Houdini: 18.5.532
-   Houdini Engine: 3.5.2

Guided walk throughs for using these files to generate your own city with roads and freeway network will follow in the near future.

Houdini uses a node graph that flows from top to bottom. Each node is a program that executes a task on its input and outputs the result to be passed to other nodes, just like a material graph in Unreal Engine. The main city is built in stages that follow this structure:

1.  City Layout
2.  Roads
3.  Freeway
4.  Lots and Sidewalks
5.  Traffic, Buildings and Ground
6.  Street Furniture, Decals and Audio

Parts are built in a dependency order such that the Freeway is dependent on the Road network, and building placement requires the Freeway to be built to avoid placing buildings on top of it.

In order to build the city and support all the procedurally generated instances that make up the world, Nanite needed to be used as much as possible. It meant that a mega mesh could be built and needed to use instances to do so. Each building in the city is made up of hundreds of instances, and all props on the street, such as furniture, decals, and even trash are using Nanite. Very little custom geometry is used in the city, which ensures that the project's memory usage stays within the set budget.

However, it was inevitable that some amount of custom geometry would be required. Custom meshes are used for collisions, the freeway deck, road decals, and custom roofs for non-rectangular buildings.

## Collaboratively Constructing Large Worlds

Unreal Engine 5 makes it easier to work collaboratively within your projects to manage and edit your assets and scene.

### One File Per Actor

The Entire world in City Sample uses the **One File Per Actor** (OFPA) system. It writes a separate file for each unique instance of an Actor placed within the Level rather than writing its data into a single map file.

For developers working in the Level Editor, nothing about your workflow has changed. You can still edit a Level by opening a single map file and making your changes. However, for those who work collaboratively using a version control system, the underlying system now tracks each Actor as a separate file, meaning that designers and artists can edit different objects and layers of the same Level without encountering conflicts when committing changes.

To learn more about setting up and using this feature in your own projects, see [One File Per Actor](/documentation/en-us/unreal-engine/one-file-per-actor-in-unreal-engine).

### World Partition

Developing games with large, open worlds in mind requires dividing the map into many smaller sections that can be loaded and unloaded as the map is traversed. Loading a multi-kilometer area all at once and having it populated with objects isn't always possible. Development tools in the past have required developers to manually divide their Levels into sublevels and carefully manage when they are streamed in and out. Viewing sections of the world in context with each other could often be difficult.

The **World Partition** system solves this problem and simplifies the process as it automatically divides objects in the level into cells based on their grid position. The cells manage the content within them and adjust accordingly as objects are added and removed so that you never need to manually manage assets. During gameplay, World Partition automatically loads and unloads cells as you move through the world.

![World Partition with some cells loaded in the Big City level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d136f623-c68b-428f-9c92-a9da0c24ac45/wp-big-city-loaded-cells.png)

The Level Editor with part of the Big City loaded using World Partition.

To learn more about setting up and using this system in your own open world projects, see [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine).

### Data Layers

Where the World Partition system divides the level into cells that can be loaded and unloaded at will, **Data Layers** are a system within World Partition used for organizing objects into layers that can be loaded and unloaded as needed. Data Layers replace the older Layers system found in Unreal Engine 4 that required a lot of manual curation of content to manage.

The City Sample makes use of Data Layers by organizing them into different sets of objects found in the world, such as procedural ones, rooftop props, freeway, and so on. The Data Layers Outliner contains a list of all layers that contain objects found in the scene. From there, you can add, remove, or set visibility of objects using these layers.

![World Partition Day Layers Outliner Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ea01887-f58e-42c2-8254-ac47a87037d2/wp-data-layers-outliner-3.png)

For more information about setting up and using layers to organize objects in your scenes, see [World Partition - Data Layers](/documentation/en-us/unreal-engine/world-partition---data-layers-in-unreal-engine).

## Simulating Real-World Systems

### MetaHumans

The City Sample is populated with thousands of unique digital human characters adapted from a subset of MetaHumans and accessories. The **MetaHuman** characters are generated using [MetaHuman Creator](https://www.unrealengine.com/metahuman-creator). MetaHuman Creator enables you to generate many diverse and unique photorealistic characters with consistent quality.

![MetaHuman Non-Playable Characters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/504dcf2d-a949-4d49-bf74-8fc1950cba4c/city-sample-crowd.png)

A crowd of generated MetaHuman characters used in City Sample and The Matrix Awakens.

The MetaHuman Creator makes it possible to design and develop film-quality characters that can be used for playable and non-playable characters (NPCs). For example, you can see in the images below that the background NPCs are consistent in quality to the playable hero character IO.

![MetaHuman Hero and Non-Playable Characters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9baf1e5c-2a68-4652-b0b9-bb84f3b0a268/mh-characters.png)

(Left to Right) City Samples playable hero character IO, Male Character, and Female Character.

MetaHuman characters come fully rigged and ready to animate. They also include their own levels of detail to balance quality with performance, making it possible to fill the city with animated film-quality characters.

![MetaHuman Crowd Simulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89cdf6dd-9867-49db-9ccb-179bb48edb3c/mh-crowd-simulation.png)

City street crossing with many unique high quality characters.

Using Drone mode while in-game, you can see hundreds of crowd characters. The closest ones are fully rigged and animated MetaHuman characters, and the more distant ones are custom generated, vertex-animated Static Meshes generated from the MetaHumans.

![MetaHuman City Streets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec3fbe05-1d01-47d5-9518-454a4efb7e5c/mh-city-street.png)

City Sample sidewalks populated with MetaHuman characters using the Mass AI Crowd System.

To start creating your own film-quality digital humans, start using the [MetaHuman Creator](https://www.unrealengine.com/metahuman-creator) today. To learn more about the MetaHuman creator and how you can use MetaHumans in your own Unreal Engine 5 projects, see visit [MetaHuman documentation](https://docs.metahuman.unrealengine.com/).

### Artificial Intelligence System

The **Artificial Intelligence** features of Unreal Engine 5 bring the city and world around it to life. Many of these features are new to the engine and are considered experimental at this time. You can dive into the City Sample and explore how they work for this project.

For more information about these features developed for Unreal Engine 5 and used in the City Sample, see the [Artificial Intelligence](/documentation/en-us/unreal-engine/artificial-intelligence-in-unreal-engine) documentation.

#### MassEntity

**MassEntity** provides a framework for data-oriented calculations that can be used in places where performance is key — including the simulation of thousands of AI agents in the scene, but not exclusive to the AI domain. It also ensures entities inside the world are persistent. This system is used for both the Traffic and Crowd systems in City Sample.

The **Mass Spawner** is an entry point to bring Mass Entities into the world. The Mass Spawner dictates two things: what type of entity is spawned and where it is spawned. The City Sample uses multiple spawners, one each for crowds, intersections, traffic, and parked vehicles.

When you select one of the Mass Spawner Actors placed in the level, the **Details** panel contains information about how the entities are used. The **Entity Type** (1) specifies what type of entity is being spawned and the **Spawn Data Generators** (2) specifies where it will be spawned in the world.

![Mass Crowd Spawner Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84f5a50e-1317-48bd-a171-22816b6039bc/bp-mass-crowd-spawner.png)

When specifying what should be spawned by the Mass Spawner, you should make a new asset type called the **Mass Entity Definition**. It dictates Traits for that entity being spawned, such as visuals, level of detail, behaviors and more.

A new **Mass Entity Definition** Data Asset type is used by the Mass Spawner to specify what should be spawned. This data asset dictates **Traits** about entities being spawned, such as their behavior, visuals, level of detail, and more.

![Mass Entity Definition Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77e28fae-bce5-44d3-9ba7-5963681f5b4c/mass-entity-definition-asset.png)

When deciding where to spawn entities, distribution along a ZoneGraph (see next section) provided through the procedural data from Houdini is used to generate spawn points along the ZoneGraph for the Crowd and Traffic Systems to use.

![Generated data used for spawning Crowd and Traffic Entities](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3541a0e6-46bf-4ca3-a90e-05df9fa43349/crowd-traffic-entities.png)

Generated data used for choosing where to spawn Crowd and Traffic entities in the city.

For parked vehicles using the spawner, a point cloud of locations is generated along city streets from the procedural data.

![Point Cloud locations used for spawned parked vehicles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1755813f-51b7-4b16-bdcb-f0877abcae92/point-cloud-parked-vehicles.png)

Point cloud locations along city streets used for spawned parked vehicles.

The Mass Spawner supports many distribution possibilities for entities in the world. The example below is a visualization of the Traffic and Crowd Systems spawned throughout the world. Green represents driving vehicles, Blue are parked vehicles, and White are crowds.

![Mass Spawner for Crowds and Traffic Systems](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8ae31ba-9191-413c-8aff-e0deea1dfb14/mass-spawner.gif)

Learn more about this feature by visiting [Mass Entity](/documentation/en-us/unreal-engine/mass-entity-in-unreal-engine) in the Unreal Engine 5 documentation.

#### ZoneGraph

The **ZoneGraph** is a lightweight design-driven flow for AI that follows a point-by-point corridor structure. It can store meaningful tags (static and dynamic) that can be leveraged for AI behaviors.

![Zone Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfb9909d-43fa-49fe-8901-c2d9f3e1bfb3/zone-graph.png)

The **Zone Shape** component can be added to the world from the **Place Actors** panel. See the Big City level's World Outliner and look for the **Zone Shapes** folder to see how these are being used.

#### StateTree

**StateTree** is a new generic state machine with an intuitive user interface shown in a decision tree structure. The StatTree dictates the behavior of Crowds. These StateTree assets are linked directly in the Mass Entity Definition data asset of the Crowd.

![State Tree Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12f8d746-9e18-4403-9963-5104acd537c0/state-tree.png)

You can find these StateTree assets specified in the Mass Entity Definition data asset of Crowds. The Traffic System does not run on StateTree behavior. For example, see the data asset named **CrowdStateTree** in the `Content/AI` folder.

Learn more about this feature by visiting [StateTree](/documentation/en-us/unreal-engine/state-tree-in-unreal-engine) in the Unreal Engine 5 documentation.

#### Smart Objects

**Smart Objects** are a collection of Actors placed in a level that the AI agents and players can interact with.The system is configurable and adds an unprecedented level of interactivity to your scene.

These did not ship as part of the developed city, but you can explore them on your own in the **MassCrowd** test map included with the sample project.

Learn more about this feature by visiting [Smart Objects](/documentation/en-us/unreal-engine/smart-objects-in-unreal-engine) in the Unreal Engine 5 documentation.

## Chaos Vehicles

Vehicles in the City Sample are driven by the **Chaos Vehicles System**. This physics-based system enables you to set up and configure vehicles for different styles of gameplay like an arcade racer or something that provides more realistic handling.

![Chaos Vehicle Physics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8182a352-84b3-4684-9cf0-f63f51551367/chaos-vehicles.gif)

The City Sample also allows you to drive a variety of four-wheeled vehicles, each with their own physics configuration for handling.

![Vehicle Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ad7fbb7-c994-4dc5-82c8-1fbba8799995/csv-featured.png)

The Chaos Vehicle system also supports a robust deformation system using Control Rig to create unique deformations for each vehicle.

![Chaos Vehicle Physics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e214a101-cf22-4b29-94c1-c4ae5834317d/chaos-vehicle-physics.gif)

For more information about setting up and using vehicles in Unreal Engine 5, see [Chaos Vehicles](/documentation/en-us/unreal-engine/vehicles-in-unreal-engine).

### Tuning Vehicle Handling

Each vehicle Blueprint contains a **Vehicle Movement Component** that defines the physical and mechanical properties of the vehicle, including its engine torque, transmissions, gearing, mass, and center of mass. The Vehicle Movement Component also has an array of data-only **Wheel Blueprints** for the front and rear wheels. Wheel Blueprints control many of the vehicle's handling and braking properties with settings for tire friction, suspension, braking torque and more.

Vehicle data Blueprints for each vehicle are located in the `Content/Vehicles/[Vehicle_Name]` folder. For example, `Content/Vehicle/vehCar_vehicle02`.

The drivable vehicle Blueprints end with "\_Sandbox" in their name, like `BP_vehCar_vehicle02_Sandbox.` These cars can be dropped in a level and are drivable.

### Dynamic Vehicle Deformation

The vehicles in City Sample make use of [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) with the Chaos Vehicle system to apply unique deformations to each vehicle. This means that each crash is achieved dynamically by utilizing the vehicle's driving dynamics. Collisions are detected using several physics bodies placed around the vehicle's body, and constraint plasticity provides the ability for physics constraints to permanently deform after passing a specified threshold.

The vehicle Control Rig contains movable constraints that are locked along a single axis. As they are moved along that axis, they will deform part of the car's body. In the City Sample, a single Control Rig is used for all drivable vehicles to apply dynamic deformation. It is named **CR\_Frame\_Destructible** and located in the `Content/Vehicle/Animation` folder of the Content Browser.

Since a single Control Rig is used for all vehicles, you will want to use the **Preview Mesh** assignment slot to swap out different drivable vehicles to preview their deformation.

![Different Vehicles with Deformation Control Rigs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eac2dce6-3d1d-4d14-b892-26a9686512a9/vehicle-cr-preview-mesh.png)

Deformation Control Rig for different drivable vehicles.

## Procedural Audio and MetaSounds

In addition to all the tools that give you freedom in visuals, game mechanics, and building open worlds, Unreal Engine 5 also allows greater control over your game's audio with **MetaSounds**.

MetaSounds provide audio designers access to a fully featured **Digital Signal Processing** (DSP) graph and sample-accurate control of sound modulation and events whether you're playing pre-designed sounds or synthesizing in real-time — all of which is powered by a robust interface for reacting to game data from both code and Blueprint.

MetaSounds empower designers with production efficiency tools, like the **Preset** and **Composition** Systems that enable designers to define and reuse their MetaSound graphs. It also enables them to build a library of powerful, customized MetaSound nodes that can streamline workflows while making MetaSounds accessible across teams.

In addition to the developed MetaSounds system, the City Sample also includes experimental designs, tools, and systems for bringing procedurally generated worlds to life with sound.

Learn more about this system by visiting [MetaSounds](/documentation/en-us/unreal-engine/metasounds-in-unreal-engine) in the Unreal Engine 5 documentation.

### Vehicle Audio

#### Drivable Vehicles

The drivable vehicles in the City Sample take advantage of an experimental tool called **MotoSynth**. It is a granular-based engine simulation tool that utilizes recordings of car accelerations and decelerations to granularly resynthesize acceleration and deceleration movement in real-time. Additionally, the drivable vehicles use MetaSounds for various decorative engine sounds, including idle loops, drifting noises, and RPM max-out sounds.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0c48545-5237-4746-ab7f-34c6d11c0293/stereo-mixer-graph.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc352a57-a35e-4890-a71b-1abf806573db/moto-synth.png) |
| Stereo Mixer for Vehicle Sounds | MotoSynth Controls |

#### NPC Vehicles

The non-playable character (or NPC) vehicles are entirely powered by MetaSounds. They take advantage of procedural audio generation features around seeded randomization. A procedurally randomized mixture of traditional pitch-blended engine loops, synthesized filtered noise, and synthesized sub-tones are dynamically modulated based on the NPC vehicle's speed.

![Non-playable Character Vehicle MetaSounds Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6eb274d5-a3bc-4d49-8713-f055170c4203/npc-vehicle-metasounds-graph.png)

### Music Redesign

MetaSounds are a powerful design environment, allowing designers to kit-bash and reuse existing sounds and music material.The City Sample features two remix variations reusing original music stems created for the demonstration, creating brand new variations of the music including a night-mode variant that is reminiscent of club music.

![MetaSounds Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98168079-375a-4db6-831c-e11e9763f1ac/metasounds-graph.png)

### City Soundscape and Procedural Audio Generation

#### World Audio Data System and Working With Houdini

The **World Audio Data** System is an experimental suite of tools and features centered around working with procedural data propagation and design. It includes a custom **Processor Rule** to convert Houdini point cloud metadata and bake it down into a **Soundscape ColorPoint Spatial Hashmap**, and then distributing the cached hashmap data to individual Actors designed to stream in and out with World Partition spread across the 16 square-kilometer Big City.

These World Audio Data Actors contain **Colorpoint** caches and take advantage of World Partition Streaming to maintain a low memory footprint.

![World Audito data System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be6e05f3-1bd7-4c50-8bd2-430eed4c31a9/world-audio-data-system.png)

#### Soundscape Design

Most of the ambient sound around the city is controlled by **Soundscape**, an experimental state-based procedural ambient sound system. Soundscape enables designers to define spawning behavior for sounds around the **Listener**, including conditional spawning behavior based on ColorPoint metadata. Most of the sound that spawn in the City Sample depends on ColorPoint data cached and loaded dynamically through the World Audio Data System. This allows designers to designate which types of sounds are allowed to spawn based on spatial metadata, such as ambient highway sounds around the freeway, ambient traffic noises on large streets, and so on.

In addition to ColorPoint data, Soundscape also listens for dynamic ColorPoint data being fed to Soundscape through a Mass AI processor to keep track of the location of idling MetaHuman and NPC vehicles. The locations are used for ambient honking and MetaHuman shouts and other vocalizations. Soundscape plays a key role in making the city sound alive.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1949d6ad-531f-4d9a-b290-14f3ca3e11d2/soundscape-ambient-sounds.png)![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6548123-93ce-4aa9-9f72-d8a91b58fd6b/soundscape-ambient-sounds-1.png)

## Creating Your Own Procedural City Guides

The City Sample project provides all the source files necessary to generate your own procedural city using Houdini and Unreal Engine 5.

In the first guide you will use Houdini to setup and generate procedural data used to create your own city with its own road network, freeway system, building zones, and more. The data exported from Houdini is then used in the second guide to populate and build your city using Unreal Engine tools and features.