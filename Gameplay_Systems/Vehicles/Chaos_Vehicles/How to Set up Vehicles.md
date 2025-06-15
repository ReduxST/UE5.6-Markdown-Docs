# How to Set up Vehicles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-set-up-vehicles-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-set-up-vehicles-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:18

---

The individual assets that make up a vehicle are as follows.

-   A Skeletal Mesh
-   A Physics Asset
-   An Animation Blueprint
-   A Vehicle Blueprint
-   One or more Wheel Blueprints
-   A Float Curve asset that represents the engine's torque curve

These are the same no matter whether you are creating an automobile or a motorcycle. This document will guide you through the process of setting up a Vehicle.

1.  Enabling the Chaos Vehicles Plugin.
    
2.  Creating and Editing Chaos Wheel Blueprints.
    
3.  Creating a Curve Asset for the engine torque.
    
4.  Importing a Vehicle Mesh.
    
5.  Creating and Editing a Physics Asset.
    
6.  Creating an Animation Blueprint with the Wheel Controller node.
    
7.  Creating a Vehicle Blueprint.
    
8.  Setting up Vehicle Control Inputs.
    
9.  Setting up the Vehicle Game Mode.
    

## Enabling the Chaos Vehicles Plugin

Before using Chaos Vehicles, the Chaos Plugin needs to be enabled.

1.  Click **Settings > Plugins** to open the **Plugins Menu**.
    
    ![Open the Plugins menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b338343-6010-445f-ba36-3e3bebb7d2ab/vs-plugins-1.png)
2.  Click the **Physics** category and enable the **ChaosVehiclesPlugin.**
    
    ![Enable the Chaos Vehicles plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d34c5af-21e6-41f5-af33-d1cfd912aeff/vs-plugins-2.png)

-   Restart Unreal Editor after enabling the plugin.
-   This plugin will not work with PhysX enabled.

## Creating and Editing Chaos Wheel Blueprints

The wheel Blueprint is where the configuration for a Wheel / Suspension / Brakes combination is set up.

In most cases, you will require at least two wheel types per vehicle. A wheel (or axle) that is affected by the steering / engine / handbrake, and one that is not. Also, this may be the case for having differently sized wheels for the front or the back, in which case, you have full control over setting the differing radii, mass, width, handbrake effect, suspension, and many other properties to give your vehicle the handling you desire.

There is no limit on the number of wheels that a vehicle may have. It is possible for multiple vehicles to share the same Wheel Blueprints, but this strategy is only valid if the wheel dimensions and suspension limits are the same.

### Create a Wheel Blueprint

1.  In the **Content Browser**, right-click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    ![Create a new Blueprint actor class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/524d1bba-7576-457c-8472-8168fafced24/vs-wheelbp-1.png)
2.  In the **Pick Parent Class window**, under **All Classes**, search for "wheel" and select **ChaosVehicleWheel**. Click **Select** to create the asset.
    
    ![Select the Chaos Vehicle Wheel class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d112985-357c-4078-a874-d6a54d222168/vs-wheelbp-2.png)
3.  The new asset will be created in the **Content Browser**. Give it a recognizable name so that you can easily locate it later (for example, 'BP\_ChaosFrontWheel').
    
4.  (**Optional Step**) Repeat these steps again so that you have a **front** and **rear** wheel type. Think of each as a setup per axle.
    

### Edit the Wheel Blueprint

Double-click the assets in the **Content Browser** to open them in the Blueprint Editor, where there are options to edit the wheels.

To start, there are five properties that need to change for each wheel, as the rest of the properties depend on how the vehicle performs (and should be tweaked later on) during testing.

| Property | Notes |
| --- | --- |
| **Axel Type** | This defines whether the wheel is in the front or the rear of the vehicle. |
| **Wheel Radius** | This needs to match the size of the render model in centimeters (cm). |
| **Affected by Handbrake** | Enable this in the rear wheels. |
| **Affected by Engine** | Enable this in the rear wheels for a rear-wheel drive (RWD) vehicle. Enable this in the front wheels for front-wheel drive (FWD) vehicles. Enable this on all of the wheels for all-wheel drive (AWD) vehicles. |
| **Affected by Steering** | Enable this in the front wheels. For vehicles with more wheels in the front (for example, a truck cab might have four-wheel steering), enable it in the second layer with a different steering angle. Alternatively, all-wheel steering is possible by selecting steering on the rear wheels with a negative steering angle. |
| **Max Steer Angle** | Normally, this is a positive value (specified in degrees). However, a negative value is allowed for rear-wheel counter-steering for all-wheel drive (AWD) vehicles. |

![Set the properties described above](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4d163de-a9ac-4a45-81e5-d5e342897783/vs-wheelbp-3.png)

Example Class Defaults for the Chaos Wheel Blueprint.

For the buggy example, set the **Wheel Radius** to **58** for both front and back wheel Blueprints.

## Creating a Curve Asset for the engine torque

The torque curve represents the amount of torque output from the engine at a given RPM. The graph's X axis represents the engine RPM (revolutions per minute) with a range from 0 to the engine max RPM. The Y axis represents the engine Torque output in NM (Newton Meters). A typical torque curve is an inverted U shape with the torque peaking near the middle of the rev range, and trailing off either side.

To create your torque curve, follow these steps:

1.  In the **Content Browser**, right-click and select **Miscellaneous > Curve**. Select the **Curve Float** type and click the **Select** button to create the asset.
    
    ![Select Miscellaneous - Curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3f37ea5-a879-4228-98d2-a280ba8b2d80/vs-curve-1.png) ![Select the Curve Float type and click Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c6a1ba9-baf7-4865-afe7-fb8b56b16cbf/vs-curve-2.png)
2.  Name the asset **TorqueCurve**.
    
    ![Select Miscellaneous - Curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0132a1f-f351-4dcc-827d-5dcbe5febf94/vs-curve-3.png)
3.  In the **Content Browser**, double-click **TorqueCurve** to open it in the **Curve Editor**. Add points to create the curve shape to your liking.
    

## Importing a Vehicle Mesh

This guide uses the **Buggy vehicle mesh** from the **Vehicle Game** sample project. In the **Epic Games Launcher** click the **Learn tab** to find the project.

### Vehicle Physics Editor

After importing a vehicle mesh to your project, follow these steps to view the mesh in the **Physics Asset Editor**.

1.  In the **Content Browser**, double-click the **vehicle Skeletal Mesh** to open it.
    
    ![Open the vehicle skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/435b3179-d9b4-4bf6-b7d4-5bb26c1bb999/vs-mesh-1.png)
2.  Click the **Physics** tab to open the **Physics Asset Editor**.
    
    ![Click the Physics tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d105df2a-3e03-44e2-be9d-2310939d9bf8/vs-mesh-2.png)

## Creating and Editing a Physics Asset

### Creating the Physics Asset

If you have a skeletal mesh that does not have an associated physics asset, then you can create a physics asset by following these steps:

1.  In the **Content Browser**, right-click the skeletal mesh asset and select **Create > Physics Asset > Create and Assign**.
    
    ![Create a new physics asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d947e148-3ac5-4ed2-9b08-be16de2c3b80/vs-mesh-4.png)
2.  Click the **Primitive Type** dropdown and select **Single Convex Hull**. Click **Create Asset** to create a new physics asset.
    
    ![Select Single Convex Hull](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a14615fa-7bad-428b-a209-1ebde0ca1860/vs-mesh-5.png)
    
    This will generate a physics asset with default collision shapes for each of the bones. The initial collision setup will most likely not be ideal since it will use the same primitive type to represent all of the bones in the physics asset.
    
3.  In the **Content Browser**, right-click the **physics asset** to open it in the **Physics Asset Editor**.
    
    ![Open the new physics asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e3644a6-88ac-4415-9b3a-3d1683661aeb/vs-mesh-6.png) ![Open the new physics asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12d84e1e-72bf-4da9-8821-d3e55620fa61/vs-mesh-7.png)
4.  Inside the **Physics Asset Editor** you can adjust the collision primitives used on each bone to better suit the vehicle mesh.
    

## Editing the Physics Asset

1.  In the **Skeleton Tree** window, click the **gear icon** and select **Show Primitives**.
    
    ![Select Show Primitives](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5d34b32-3654-42e5-8481-4e11c74edcef/vs-mesh-8.png)
2.  Select all the wheel bones inside the Skeleton Tree window.
    
    ![Select all the wheel bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac814f8f-ee54-4de4-b325-bec8becaa267/vs-mesh-9.png)
3.  Go to the **Tools** window and under the **Body Creation** section, click the **Primitive Type** dropdown and select **Sphere**. Click **Re-generate Bodies**.
    
    ![Select the Sphere primitive type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fadec6f-c45b-4c99-9639-16198d8fb1fe/vs-mesh-10.png) ![Select the Sphere primitive type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/233500c8-3195-4504-adcc-326fdfa147e6/vs-mesh-11.png)
4.  You can now see the Sphere primitives on each of the wheels.
    
    ![Wheels with Convex Hulls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/689fa51d-b17c-4c0e-bb46-45381c92e5a7/vs-mesh-12a.png)
    
    ![Wheels with Spheres](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41d12bc1-d0e6-4eed-9563-66a56ead3340/vs-mesh-12b.png)
    
5.  Select the **suspension** bones inside the **Skeleton Tree** window. Right-click and select **Collision > No Collision** to remove collision from the vehicle suspension.
    
    ![Select the Sphere primitive type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1ffcb8d-c214-426c-bb59-bdccc41850dc/vs-mesh-13.png) ![Select the Sphere primitive type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f4c7496-14c8-492d-8621-58c22e08b869/vs-mesh-14.png)

## Creating an Animation Blueprint with the Wheel Controller node

Animation Blueprints are used to control Vehicle Skeletal Mesh animations specific to that vehicle, such as spinning tires, suspension, handbrakes, and steering animations. To offload a lot of the work in creating these types of animations, you can use the **Wheel Controller Node** to drive the animations.

### Wheel Controller Node

Where an Animation Blueprint is used to get and control animations for the vehicle, the **Wheel Controller** node makes controlling all of the animations for the vehicle straightforward with little to no additional setup.

![Wheel Controller node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08a03981-f7fb-4fa1-b50c-ac7e5bc6273c/vs-anim-1.png)

The node gets the necessary information from the wheels (such as "How fast is it spinning?" or "Is it affected by the Handbrake?" or "What are the suspension settings for this wheel?"), and translates the query results to an animation on the bone that the wheel is associated with.

### Create an Animation Blueprint

1.  In the **Content Browser**, right-click and select **Animation > Animation Blueprint**.
    
    ![Select Animation Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa02f5e9-7541-46fb-8b2f-0a898d3800db/vs-anim-2.png)
2.  In the **Create Animation Blueprint** window, select the **VehicleAnimationInstance** parent class and select the vehicle **Skeleton** from the list. Click **Create** to create a new Animation Blueprint asset.
    
    ![Select the vehicle animation instance parent class and your vehicle skeleton from the list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/850cb861-9a0c-4e5e-bf7f-15d6b7cf29a1/vs-anim-3.png)
3.  In the **Content Browser**, double-click the **animation Blueprint** to open it.
    
4.  Right-click in the **Anim Graph** and search for then select **Mesh Space Ref Pose**.
    
    ![Select the Mesh Space Ref Pose node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fef3a77-8f13-4a93-90ed-eebc5d804ae9/vs-anim-4.png)
5.  Right-click in the **Anim Graph** and search for then select **Wheel Controller for WheeledVehicle**. Connect the **Mesh Space Ref Pose** node to the **Wheel Controller** node.
    
    ![Select the Wheel Controller for WheeledVehicle node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06ec6bab-0120-4165-8dbf-7d63aaf98f20/vs-anim-5.png) ![Connect the Mesh Space Ref Pose node to the Wheel Controller node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25579896-c158-4480-b071-aac2b5776138/vs-anim-6.png)
6.  Right-click in the **Anim Graph** and search for then select **Component To Local**. Connect the **Wheel Controller** node to the **Component To Local** node. Connect the **Component To Local** node to the **Output Pose** node.
    
    ![Select Component To Local node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b539dd8-c7d6-4809-9ca2-6515d4462040/vs-anim-7.png) ![Connect the Wheel Controller node to the Component To Local node. Connect the Component To Local node to the Output Pose node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/227b9aee-b7be-4390-b8ba-a6641fc7b68f/vs-anim-8.png)
7.  (**Optional Step**) If you have additional struts or other suspension needs (like the sample Buggy from **Vehicle Game**), you will need additional nodes in the **Animation Graph** to handle the joints that affect those polygons. For example, in the Buggy, the extra joints are used to control the axle connections to the wheels. These are driven by **Look At** nodes, which, when given the wheel joints, will be driven by the **Wheel Controller** node. The **Look At** nodes will ensure the suspension stays attached to the wheels, as demonstrated in the following example.
    

The Buggy uses the following Look At node composition:

| Bone | Look At |
| --- | --- |
| F\_L\_Suspension | F\_L\_wheelJNT |
| F\_R\_Suspension | F\_R\_wheelJNT |
| B\_L\_Suspension | B\_L\_wheelJNT |
| B\_R\_Suspension | B\_R\_wheelJNT |
| B\_L\_wheelJNT | B\_L\_Suspension |
| B\_R\_wheelJNT | B\_R\_Suspension |

## Creating a Vehicle Blueprint

In this section, you will create the Vehicle Blueprint that uses all the assets created in the previous sections.

1.  In the **Content Browser**, right-click and select **Blueprint Class** from the **Create Basic Asset** category.
    
    ![Create a new Blueprint class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43599538-4ae5-459e-9eb5-e793bd852505/vs-bp-1.png)
2.  In the **Pick Parent Class** window, expand the **All Classes** section and search for and select **WheeledVehiclePawn**. Click **Select** to create the new Blueprint asset.
    
    ![Create a new Blueprint class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26ac090b-26eb-413b-917e-3fa26b10dc1f/vs-bp-2.png)
3.  In the **Content Browser**, double-click the **Vehicle Blueprint** to open it.
    
    ![Open the new  Vehicle Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8b043b4-6eb9-49d2-a4fa-f01e3bdb2c0b/vs-bp-3.png)
4.  In the **Components** window, click the **Mesh** Skeletal Mesh Component. Go to the **Details** panel and under the **Mesh** section click the **Skeletal Mesh** dropdown. Select your vehicle's **Skeletal Mesh** asset.
    
    ![Select the Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd9a2c94-263c-4222-ad19-237a907a55d1/vs-bp-4.png) ![Select your vehicle's skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/397f72ef-bd20-433f-9f91-7a60c0222b5f/vs-bp-5.png)
5.  In the **Details** panel, scroll to the **Animation** section and click the **Anim Class** dropdown. Select your vehicle's **Animation Blueprint**.
    
    ![Select your vehicle's Animation Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b467ccc-0faa-4ff4-84b1-f7ce0602c8fa/vs-bp-6.png)
6.  In the **Details** panel, scroll to the **Physics** section and enable the **Simulate Physics** checkbox.
    
    ![Enable the Simulate Physics checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf535c85-21f3-4d44-a0e9-26b7ba1b1412/vs-bp-7.png)
7.  From the **Components** window, click **Add Component**, and search for then select **Spring Arm**.
    
    ![Add a Spring Arm](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/487cd26c-cced-4683-9210-1bd72ea1d1e8/vs-bp-8.png)
8.  With the **Spring Arm** component selected, click **Add Component**, and search for then select **Camera**.
    
    ![Add a Camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39f3767e-cdda-40ea-9b65-f354e214249f/vs-bp-9.png)
9.  In the **Viewport** select the **Camera** and position it to your liking.
    
    ![Position the Camera to your liking](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a28f1bd9-e3b6-4c30-82f4-cf0f45ff5aa5/vs-bp-10.png)
10.  Select the **Camera** component and go to the **Details** panel. Scroll to the **Camera Settings** section and verify that **Use Pawn Control Rotation** is disabled.
    
    ![Verify that Use Pawn Control Rotation is disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd655795-c403-4abd-be5d-f9209524380e/vs-bp-11.png)
    
    This ensures that the camera is locked to its view direction rather than the Player Controller's view direction.
    
11.  Select the **Vehicle Movement Component** in the **Components** window.
    
    ![Select the Vehicle Movement Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2cb5621-d398-4b1f-b2b4-8ff34420a8ef/vs-bp-12.png)
12.  Go to the **Details** panel and scroll to the **Vehicle Setup** section. Expand the arrow next to **Wheel Setups** and set the following for each wheel:
    
    -   Set the **Wheel Class** to the Wheel Blueprint(s) you created.
    -   Set the **Bone Name** to the name of the joint that should be controlled by the wheel.
    
    ![Wheel Setups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de897484-a0fa-47f1-9686-d7a56c1bd738/vs-bp-13.png)
    
    The order you assign the wheels has no bearing on whether it is a front or a rear wheel, only the **Bone Name** and **Wheel Class** have any effect. For organizational purposes, we recommend keeping the wheels in the same order for each new vehicle (for example: FL, FR, BL, BR). Keeping a standard helps when you access wheel data by wheel index (the index in the Wheel Setup array).
    
    If the vehicle requires more than 4 wheels, click the **+** icon next to the **Wheel Setups** property to add more, or conversely remove wheels as needed.
    
13.  Select the **Vehicle Movement Component** in the **Components** window and go to the **Details** panel. Scroll down to the **Mechanical Setup** section and expand the **Engine Setup** category. Expand the **Torque Curve** category and add the **torque curve asset** to the **External Curve** dropdown.
    
    ![Wheel Setups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13a6fb78-9e83-41e1-95b4-6ccf0468ee79/vs-bp-14.png)

## Setting up Vehicle Control Inputs

1.  Click **Settings > Project Settings** to open the **Project Settings** window.
    
    ![Open the Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d8db84f-6c60-46d1-9e72-91ef81ccf547/vs-input-1.png)
2.  Go to the **Input** category and set up control inputs for steering, throttle, brake, and handbrake. The image below shows the inputs for the Buggy in the Vehicle Game.
    
    ![Input Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c462d5c-8ae1-4ba5-a03a-a390c28b1bae/vs-input-2.png)
3.  In the **Content Browser**, double-click the **Vehicle Blueprint** to open it.
    
    -   Drag the **Vehicle Movement Component** to the **Event Graph** to create a node.
        
    -   Drag from the **Vehicle Movement Component** node and search for then select **Set Throttle Input**.
        
    
    ![Input Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4945ffe3-99ae-400b-9b4f-f61412a84d47/vs-input-3.png)
4.  Right-click in the **Event Graph** and search for then select **Throttle** to add your Throttle input event.
    
    ![Add Throttle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/701d77da-35f0-4e06-b037-9fd5802aa777/vs-input-4.png)
5.  Connect the **InputAxis Throttle** node to the **Set Throttle Input** node. Connect the **Axis Value** pin from the **InputAxis Throttle** node to the **Throttle** pin of the **Set Throttle Input** node.
    
    ![Connect the InputAxis Throttle node to the Set Throttle Input node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97e8dfb0-953e-4b1b-bcd5-97f1d3adaa01/vs-input-5.png)
6.  Follow the steps above and add the nodes for **Set Brake Input** and **Set Steering Input**, and connect them with their corresponding input events.
    
    ![Add the nodes for Set Brake Input and Set Steering Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28c61f73-5b6e-40b7-9fbf-589ec3a3fb45/vs-input-6.png)
7.  Follow the steps above and add the nodes for **Set Pitch Input**, **Set Roll Input** and **Set Yaw Input**, and connect them with their corresponding input events.
    
    ![Add the nodes for Set Brake Input and Set Steering Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/489d83ef-e08b-4c2e-b0e6-824660b92cd2/vs-input-7.png)
8.  Follow the steps above and add the nodes for **Set Change Up Input** and **Set Change Down Input**, and connect them with their corresponding input events.
    
    -   Enable the **New Gear Up** checkbox on the **Set Change Up Input** node.
        
    -   Enable the **New Gear Down** checkbox on the **Set Change Down Input** node.
        
    
    ![Add the nodes for Set Brake Input and Set Steering Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16599618-62fa-49e3-86ec-15cd629559eb/vs-input-8.png)
9.  Follow the steps above and add the node for **Set Handbrake Input** twice, and connect each node to the **Pressed** and **Released** pins of the **InputAction Handbrake** node. Enable the **New Handbrake** checkbox on the **Set Handbrake Input** node connected to the **Pressed** pin.
    
    ![Add the nodes for Set Brake Input and Set Steering Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80b37b3f-af63-40f2-a522-66c1281281ae/vs-input-9.png)

## Vehicle Game Mode Setup

1.  In the **Content Browser**, right-click and select **Blueprint Class** from the **Create Basic Asset** category.
    
    ![Create a new Blueprint class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2e306b4-16b7-40a6-88e5-389aa51f369d/vs-bp-1.png)
2.  In the **Pick Parent Class** window, select **Game Mode Base** to create the Game Mode Blueprint.
    
    ![Select Game Mode Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/683c24d5-b21d-4a84-a379-73cb88b6ef20/vs-gamemode-1.png)
3.  In the **Content Browser**, double-click the new **Game Mode Blueprint** to open it.
    
    ![Double-click the new Game Mode Blueprint to open it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d60cc8be-2a34-4183-ae82-79bc510ea97c/vs-gamemode-2.png)
4.  Go to the **Details** panel and scroll to the **Classes** section. Click the **Default Pawn Class** dropdown and select your **Vehicle Blueprint**.
    
    ![Double-click the new Game Mode Blueprint to open it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15d9c77d-a27e-4c81-9f21-925859303b64/vs-gamemode-3.png)
5.  Click **Compile** and **Save**, then close the window.
    
6.  In the Main Viewport window, click **Window > World Settings** to open the **World Settings** panel.
    
    -   Go to the **World Settings** panel and scroll down to the **Game Mode** section.
        
    -   Click the **GameMode Override** dropdown and select your Game Mode Blueprint.
        
    
    ![Open the World Settings panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79e9dc64-20ab-47bc-bb1a-cc119675b933/vs-gamemode-4.png) ![Click the GameMode Override dropdown and select your Game Mode Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbe4e1da-3d26-4e6c-a407-4cbd78f33d5d/vs-gamemode-5.png)
7.  Press **Play** and test your vehicle.
    
    ![Showcase of three Fluid Systems in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39da5f5c-b2f9-45e7-9aac-7ee17acb03dc/vs-vehicle-demo.gif)

If you have an existing PhysX vehicle that you want to convert to Chaos, follow the [PhysX to Chaos Vehicle Conversion](/documentation/en-us/unreal-engine/how-to-convert-physx-vehicles-to-chaos-in-unreal-engine) guide.