# Water Buoyancy Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/water-buoyancy-component-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/water-buoyancy-component-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:59

---

The Water system includes a Blueprint **Buoyancy** Component which uses spheres (pontoons) to create a simplistic volumetric approximation of the object that is meant to interact with the water surface. This approximation provides a low-cost solution that can support multiple objects using buoyancy at the same time.

![Water Buoyance with many objects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2469921-0d29-497f-a7e2-d816d88be97a/water-buoyancy-many-objects.gif)

## Example Water Buoyancy Blueprint

The **Water** plugin contains its own example content that you can use and explore. This includes a Blueprint which is set up using the Buoyancy component with a cube static mesh. In order for the cube to balance and sit upright on the water's surface, the Blueprint is set up using four pontoons.

The Buoyancy example Blueprint can be found under **Engine > Plugins > Water Content > Blueprints** and is named **BP\_BuoyancyExample**. Drag and drop it above any Water Body surface. When you **Play** or **Simulate**, it will automatically drop and float along the water's surface like the example below.

## Setting Up Water Buoyancy In A Blueprint

The following steps will show you how to set up and use your own Blueprint using a Buoyancy component.

1.  In the **Content Browser**, create a new **Blueprint Class**, pick the **Actor** class, and give it a name. For this guide, we'll use "BuoyancyExampleBP."
    
    ![Create a Blueprint Actor.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38c17155-c1af-438f-8652-ecf9b2a8cebc/1-create-actor-bp.png)
2.  Open your Blueprint. In the **Components** panel, click the **Add +** dropdown and select **Static Mesh**.
    
    ![Add a Static Mesh Component to your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fe627be-84fe-4245-8e31-5cd0acd015cd/2-bp-add-staticmesh-component.png)
3.  Select the **Static Mesh** Component. In the **Details** panel, assign a mesh to the **Static Mesh** assignment slot.
    
    ![Assign a Static Mesh to the Static Mesh Component in your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70c19751-3240-4dd1-80cc-a34cb5d43378/3-bp-assign-staticmesh.png)
    
    You can download the mesh used with this guide if you want to follow along exactly as shown. Drag and drop this mesh directly in to the **Content Browser**.
    
    [Boat Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/adb31599-3601-4cf3-a977-844470bf9239/boat-mesh.zip)
    
4.  While still in the **Details** panel, enable **Simulate Physics** and the checkbox next to **Mass (kg)** under the **Physics** category.
    
    ![Enable Physics in the Static Mesh Component of your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03e0696f-81e4-4186-b8d3-99a6ecf7afc4/4-bp-staticmesh-enable-physics.png)
    
    **Mass (kg)** must be enabled for the Buoyancy Component to work.
    
5.  In the **Components** panel, use the **Add +** drop down menu to add a **Buoyancy** Component.
    
6.  Select the **Buoyancy** Component. In the **Details** panel under **Buoyancy Data**, you'll add some **Pontoons** that allow the mesh to float on water surfaces. Start by adding one Pontoon by clicking the **Add (+)** icon.
    
    ![Add Pontoons to the Buoyancy Component of your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f75aa6c0-b5c8-4127-ac08-5664c97874d5/6-buoyancy-component-add-pontoons.png)
    
    You should see a new pontoon element added to the array that looks like this:
    
    ![Buoyancy Component Pontoon settings in your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9eb2493-175d-4e57-9f50-eee0d1c18ded/6-buoyancy-component-pontoon-settings.png)
7.  Add **three** more **Pontoons** to the array for a total of four array elements. Place these pontoons along the front and back sides of the mesh to stabilize it on the water's surface, by using **Relative Location** to place the pontoons at the following locations:
    
    ![Listing of the four Pontoons added to your Buoyancy Component of your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8808b892-394f-4069-8b6b-5724cabb882c/7-buoyancy-component-pontoon-locations.png)
    -   **Index 0 (back left):** 660, 370, 0
    -   **Index 1 (back right):** 660, -370, 0
    -   **Index 2 (front left):** -220, 370, 0
    -   **Index 3 (back right):** -220, -370, 0
        
        There is no visualization of the pontoons when entering their relative location. However, you can use [Static Mesh Sockets](/documentation/en-us/unreal-engine/using-sockets-with-static-meshes-in-unreal-engine) and the **Center Socket** tag to place pontoons without entering specific location data, or add **Scene** components to your Blueprint and copy their location to the pontoon's relative location manually.
        
8.  In the Blueprint **Components** panel, click and drag the **StaticMesh** component onto the **DefaultSceneRoot** making it the new Root component.
    
    ![Making the Static Mesh component the root of your Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cefd03df-f8dd-4eb7-94fc-d84bf6eebb4e/8-buoyancy-staticmesh-scene-root.png)
    
    The Static Mesh **must be** the Root for the Buoyancy component to work properly.
    
9.  Drag and drop your Buoyancy Blueprint into the level and place it above the surface of the water. Press **Play** or **Simulate** to see the results.
    

## Buoyancy Component Properties

The **Buoyancy** Component has the following properties. These control the physics of how the pontoons interact with the surface of the water.

Click image for full size.

The following properties are available in the Blueprint **Details** panel under the **Buoyancy** section when you select the Buoyancy Component.

| Property | Description |
| --- | --- |
| **Pontoons** | 
An array of available pontoons which can be of varying radii that are added to the component to approximate its volume.

-   **Center Socket:** The socket on the Static Mesh to center this pontoon on.
-   **Relative Location:** The location of the pontoon relative to the parent Actor's location. It is overridden by Center Socket when one is specified.
-   **Radius:** The radial size of this pontoon (in world units).
-   **FXEnabled:** Should this pontoon be considered as a candidate for visual/audio effects upon entering water for burst cues, which are implemented by the user?



 |
| **Center Pontoons on COM** | If enabled, center the pontoons around the center of mass when using relative locations. This is not used when pontoon locations are specified using sockets. |
| **Buoyancy Coefficient** | Increases the buoyant force applied to each pontoon. |
| **Buoyancy Damp** | A damping factor to scale damping based on Z velocity. |
| **Buoyancy Damp 2** | A second order damping factor to scale damping based on Z velocity. |
| **Buoyancy Ramp Min Velocity** | The minimum velocity to start applying a ramp to buoyancy. |
| **Buoyancy Ramp Max Velocity** | The maximum velocity up to which the buoyancy can ramp up. |
| **Buoyancy Ramp Max** | The maximum value that buoyancy can ramp to (at or beyond the max velocity). |
| **Max Buoyant Force** | The maximum buoyant force in the Up direction. |
| **Water Shore Push Factor** | The coefficient for nudging objects toward the shore (primarily for performance reasons). |
| **Water Velocity Strength** | The coefficient for applying force in River Water Bodies. |
| **Max Water Force** | The maximum push force that can be applied by River Water Bodies. |
| **Apply Drag Forces in Water** | Specifies whether to apply drag forces to an object moving through water. |
| **Drag Coefficient** | The coefficient for applying linear drag based on speed. |
| **Drag Coefficient 2** | The coefficient for applying linear drag based on the square of the speed. |
| **Angular Drag Coefficient** | The coefficient for applying angular drag that resists the rotation of the object. |
| **Max Drag Speed** | The maximum speed at which drag force is applied. |
| **Apply River Forces** | Specifies whether the engine should apply river forces such as downstream push and shore push. |
| **River Pontoon Index** | List of which Pontoons water forces should be calculated from. Used to calculate lateral push/pull, and to grab water velocity for main force calculations from downstream calculation when possible. |
| **Water Shore Push Factor** | The coefficient for nudging objects to the shore in Rivers (for performance reasons). Or, set negative to push towards the center of the river. |
| **River Traversal Path Width** | The path width along the inside of a river which the objects should traverse. |
| **Max Shore Push Force** | The maximum push force that can be applied by rivers towards the edge or center. |
| **Water Velocity Strength** | The coefficient for applying push force in rivers. |
| **Max Water Force** | The maximum push force that can be applied by rivers. |
| **Always Allow Lateral Push** | When enabled, allows an object to be pushed laterally regardless of the forward movement speed through the river. |
| **Allow Current when Moving Fast Upstream** | When enabled, it applies the current when moving at high speeds upstream. Disable for vehicles to have more control. |
| **Apply Downstream Angular Rotation** | When enabled, it applies torque to align the object along the downstream direction of the river. |
| **Downstream Axis of Rotation** | The axis with respect to the object with which the downstream angular rotation should be aligned. |
| **Downstream Rotation Strength** | The strength of the downstream angular rotation application. |
| **Downstream Rotation Stiffness** | The stiffness of the spring used to align the object along the downstream direction. |
| **Downstream Rotation Angular Damping** | The damping of the spring used to align the object along the downstream direction. |
| **Downstream Max Acceleration** | The maximum torque to apply per update for downstream rotation. |

## Debugging Water Buoyancy

You can debug the Buoyancy Component interactions with water surfaces using the console command `r.Water.DebugBuoyancy 1`. Each pontoon is drawn along with a grid of points that interact with the water surface.

The example below shows several different shapes and boat meshes using pontoons with different spacing and sizes.