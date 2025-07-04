# How to Build a Double Wishbone Suspension Vehicle

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-build-a-double-wishbone-suspension-vehicle-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-build-a-double-wishbone-suspension-vehicle-in-unreal-engine)  
**Processed:** 2025-06-14 16:28:41

---

This tutorial will walk you through the details of the **Advanced Vehicle** template. When we are done, you should have a pretty good idea of how it works in theory, and how to build and configure something similar yourself. The main focus is going to be on the suspension.

All the FBX assets used in the vehicle template are available **[here for download](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/1c79390b-3757-40ec-ac67-1ffa4a1c40fe/doublewishbonevehicle_files.zip)**. You should be able to analyze the originals and experiment with your own designs in any modeling package that is capable of reading and writing FBX files. These FBX files should be used with the **Advanced Vehicle** project template available in Unreal Engine.

Before we get started, you should be aware that a double wishbone suspension is quite a bit more complex to set up than the standard Unreal Engine vehicle, so if you have not successfully set one of those up before, you are strongly encouraged to do that first. Refer to the [How to Setup Vehicles](/documentation/en-us/unreal-engine/how-to-set-up-vehicles-in-unreal-engine) documentation for more information.

Once you have read that documentation and have successfully set up a base vehicle, you will be ready to look at the double wishbone design discussed here. We will start with some fundamental theory.

## Simulated Wheels Versus Real Suspension Linkages

When we set up the vehicle movement component and assign wheels to it, the vertical movement of the wheels is typically updated by a WheelHandler node inside the vehicle's animation Blueprint. On each frame, the handler will move the wheels up and down along the local Z axis to simulate suspension, making sure that the wheels touch the ground whenever that is possible.

Furthermore, the **WheelHandler** also applies rotation to make the wheels spin around their Y axis, driven by the rotation speed of the simulated motor and gearbox. In addition to this, it will turn the wheels around their Z axis, driven by the current steering angle.

The default vertical suspension movement is clamped by the **Suspension Max Raise** and **Drop** settings in your **VehicleWheel-derived** classes. This movement is entirely linear, as illustrated below:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8a9e5ba-b0d0-4d26-920f-d60d780c5465/simwheeldefaultmovement.gif)

The standard vertical movement produced by the WheelHandler.

While not entirely realistic, this type of suspension simulation is in fact perfectly fine for most vehicles, because you cannot usually see the suspension arms or the other components such as the springs and shocks. Any car model with a full body can get typically away with this.

However, in a more open vehicle like a Buggy or a Formula 1 car, where the moving parts are in plain view, this movement can be problematic, because there is no sensible real-world suspension design that would be able produce this kind of movement.

To achieve a more realistic result, we really need a type of motion that can be expressed as a rotation around some fixed pivot point on the vehicle's body:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc2dde95-1b5e-48b8-b555-143ecc2ebf82/realwheelmovement.gif)

Ideal vertical and lateral movement.

To solve this little conundrum, we can start by assuming that wheel management falls into two different categories: one being the simulated wheel nodes controlled by the WheelHandler, the other being the wheels that we can actually see being rendered when we drive the car. Then we could feed data supplied to us by the WheelHandler to the rest of our suspension setup to get the desired results.

In short, the visible wheel and the simulated wheel could in fact be two entirely different objects, and the simulated wheel would not even have to be visible at all.

The wheel parameters we define in the VehicleWheel class can specify the **collision mesh**, **radius** and **width** explicitly. Those specifications do not necessarily have to correspond to any real geometry in the vehicle's skeletal mesh, so there is really no need for the simulated wheel nodes in the mesh to have any real geometry attached to them at all. Furthermore, we can specify additional wheel offsets in the wheel setup section of the vehicle Blueprint, so the pivot of our wheels do not have to be aligned with the geometrical center of the visible wheel mesh.

These are the basic insights we need to build a suspension that looks like it could realistically work from a mechanical point of view.

## What Skeletal Nodes Can Do

Before we move on, we need to take a look at two animation Blueprint nodes that will be particularly useful for our setup. The WheelHandler node has already been covered, and we will definitely want to use that, but there are other powerful tools that are crucial for this type of rigging: the **CopyBone** and **LookAt** nodes. They can both be found in the Skeletal Control category in the animation Blueprint editor, and they perform much the same tasks as standard position, rotation and aim constraints typically do in an application like Maya.

### Copy Bone

As its name suggests, the CopyBone node can copy transformation data from one bone (the source) to another bone (the target):

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22c2303b-3aeb-4358-a259-b72d3088c098/node_copybone.png)

The CopyBone animation Blueprint node and its default settings.

This means that once the WheelHandler has updated the transformation of the simulated wheels, we could, for example, grab only the rotation values it has produced and apply them to our visible wheels. This basic step would take care of spinning and steering the wheels, which we do want, while we avoid getting the translation (position) data, which we do not want.

### Look At

The LookAt node can rotate any given bone in such a way that one of its cardinal axes ends up aiming at another bone:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b04feb55-6397-4e1f-bb50-d62b3d5d68c0/node_lookat.png)

The LookAt animation Blueprint node and its default settings.

This is useful for our setup, because it gives us a way to make sure that all the components of the suspension mechanism are constantly updated to point in the right direction, all driven directly or indirectly by the current position of the simulated wheels. All we have to do is to make sure that there are bones available for the LookAt nodes to aim at. This will be used for several bones in our animation Blueprint.

## Implementation Overview

To recap: for each of the four wheels we will use one invisible wheel for the WheelHandler to manage, and one visible wheel that is actually rendered in game. The former is just a single bone/joint, without any part of the mesh weighted to it, while the latter is any wheel-like mesh we build in a modeling package and add to the vehicle model, which is then imported into UE for final setup.

For everything to work as intended, key parts of the suspension will then copy the transformation data they need from other bones, or adjust their orientation by looking at targets that we have set up in the model.

## Constructing the Model

With the theory out of the way, it is time to look at how this demo vehicle is constructed. If you open `Assets/FBX/vehicle_proto_S2.9.fbx` in your main modeling application, you can follow along and see how everything fits together.

The vehicle prototype created for this tutorial has a suspension rig designed like this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a2c322e-ef41-4d25-8e81-db4ed7fbd143/keycomponents.png)

Close-up on the front right suspension of the prototype vehicle. The colors have been added to this illustration for clarity - they are not assigned to materials in the FBX file.

The key components here are the upper and lower arms (yellow), the kingpin (red) and the hub (blue). Both arms pivot around their respective hexagonal bolts seen in the far right of the image.

The most central point where everything comes together is close to the green bolt on the lower arm. That is where the simulated wheel joint, `PhysWheel_[loc]`, is initially located. The kingpin, hub, and visible wheel also have their pivots at that exact same location.

Each one of these components has a very strict responsibility and transformation range. The arms rotate only around their forward axis. The kingpin follows the position of the tip of the lower arm, but stays vertical at all times and never rotates relative to the vehicle. The hub rotates around its vertical axis only, in response to steering. The visible wheel copies its rotation from the simulated wheel, but takes its position from the tip of the lower arm. This keeps everything tightly locked together.

In any reasonably complex rig, it is very important to keep the hierarchy and update order in mind. In this particular case: when the lower arm rotates, it must bring with it a child mesh (lower green bolt) that the kingpin subsequently needs in order to position itself correctly using a CopyBone node. The upper arm in turn needs access to the updated position of a child mesh (near the upper green bolt) of the kingpin in order to have something to aim at using a LookAt node, and so on. As you can see, it is essential to make sure that the different components are updated in the correct order, otherwise parts of the suspension may appear to lag behind the movement of other parts.

All these frame-by-frame updates are handled by the animation Blueprint.

When building the model in a DCC (Digital Content Creation) application, we really only have to worry about the hierarchy and the exact position and orientation of the component pivots. A sensible orientation is particularly important for components that will have their rotation updated by LookAt nodes.

As a general note, it can be helpful to use the constraints offered by your modeling package while designing this kind of mechanism. They will not follow the FBX into UE on import, but sometimes it is easier to figure out what needs to be done if you can get some basic movement going while building the model, just to ensure that different components will be able to move the way they need to without intersecting each other. However, avoid using any constraints that you will not be able to recreate inside the animation Blueprint.

## The Setup in Unreal Engine

Now let us see how this demo has been set up inside Unreal Engine. Load up the project file in the editor to follow along, and open the vehicle's animation Blueprint. Note that most of the operations are applied four times, once for each wheel.

While driving the vehicle, the following things happen in the animation Blueprint:

First, the WheelHandler updates the position and rotation of the simulated wheels (`PhysWheel` bones). The visible wheels (`VisWheel` bones) then update their rotation by copying the rotation from the `PhysWheels`:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9a0b160-1370-48f4-8d95-2b7659d3ca1c/animbp_1.png)

The WheelHandler followed by Copy Rotation to the visible wheels.

This gives us a visually correct spin and steering, but the wheels will not change their position. That is handled separately in a later step.

Next, the lower arms (`ArmLower` bones) aim at the position of the `PhysWheel`. Arms on the right side of the vehicle use Y as the look at axis, while arms on the left side use Negative Y:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72467860-cf7c-4270-9e31-a1e0a6d94e3d/animbp_2.png)

The ArmLower bones looking at the PhysWheel position.

The result of a LookAt node can easily be previewed in the 3D window of the animation Blueprint editor: the current target of a selected LookAt node is marked with a red cross. This is easier to see if you set the preview viewport to wireframe mode.

When an `ArmLower` bone rotates to match its LookAt target, it brings with it a child component called `POS_Hub`. This is used in the next step to correctly position the Kingpin using a CopyBone node which grabs only the translation of the `POS_Hub` bone:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ef973b9-0d79-4ff4-a5bb-eebec9bcca64/animbp_3.png)

Setting the Kingpin position.

The Hub and `VisWheel` will later be set to the same position using the same method.

The next step adjusts the upper arms (`ArmUpper` bones) by looking at their respective targets (`LAT_ArmUp` bones) which have been placed in the correct position by the fact that these targets are children of the Kingpin bones, which were updated in the previous step:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e3ac0cf-c551-4bdb-af52-20b529d7ab76/animbp_4.png)

Orienting the upper arms.

After setting the position of the hubs, there is some extra work that needs to be done on the front hubs only, to account for rotation around Z caused by steering. This is handled with LookAt nodes targeting `LAT_Hub` bones that are children of the frontal PhysWheels:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a53fee3f-3255-4c41-8641-5aab269b5e76/animbp_5.png)

Setting Hub position and steering angle.

Finally, after setting the VisWheel positions to match the `POS_Hub` bones, we make sure that the upper part of the shock is aimed at the lower shockmount (`ShockMount_Low`), and that the lower shock bone follows the position of that very same shockmount, which is a child of the upper arm:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43982352-7e37-4519-a285-deeb63899c97/animbp_6.png)

Positioning visible wheels, and adjusting shock components.

## PhAT

The prototype's physics asset setup is largely the same as the standard vehicle template, with a few exceptions. The most obvious difference is a lot of small spherical bodies along the antenna, but more importantly, there is a custom collision shape surrounding the main vehicle frame.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b0b8222-8818-4ca2-8a3d-b40616bb11b6/phat_1.png)

Collision bodies in PhAT.

Since the root component of this model is actually a joint, there is no geometry available from which to create a detailed collision volume. The main body volume was created by importing a separate Static Mesh equipped with a UCX mesh (Assets/FBX/vehicle\_collision\_S2.9.fbx).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abae8f08-34fa-46e3-9bce-dc4ab1b14fe6/phat_2.png)

Separately imported Static Mesh asset with collision.

We cannot handle this entirely inside PhAT. The first step is to build the collision asset in your 3D modeling package of choice, preferably by starting from the main body mesh itself. This collision model is then imported into UE as a standard Static Mesh, along with the UCX collision. Once that is done, we can simply copy this collision data over to the root node of the vehicle inside PhAT. This option is available when you **right-click** an existing body in PhATs Skeleton Tree panel. If the target bone does not already have a body assigned, you can just add a new body which will have a default capsule shape primitive attached. Then remove the capsule once the custom collision has been added.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97985ea5-daad-45ec-9f70-409d0623ad32/phat_3.png)

Copy collision option, under "Advanced" in the menu.

### Antenna Setup

While the antenna is not part of the double wishbone suspension setup, it can still affect the overall handling of the vehicle. The simplest solution is of course a completely rigid antenna, unaffected by physics, but this template shows how to set up an antenna that will move as you drive without negatively impacting your vehicle's movement.

In this template, each antenna bone starting from **Antenna1** all the way to the tip at **Antenna10** has been set up with a spherical body that has a radius roughly matching that of the antenna mesh itself. The bodies have **Enable Gravity** turned off to make sure the antenna can remain upright with a minimum of effort from the physics system. The mass of these bodies decays exponentially as we get closer to the tip, starting with a mass scale set to 16 at the bottom. The mass scale of the next body is set to 50`%` of the previous body, and so on, giving a full sequence from bottom to tip with the values 16, 8, 4, 2, 1, 0.5, 0.25, 0.12, 0.06 and 0.03. This gives us a heavy base, a featherlight tip, and a smooth gradient between the two extremes.

![Antenna physics body details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4ce80fb-67af-445f-92bf-036040b1980b/phat_antenna_1.png)

The constraints applied to these bodies are fully locked, both linearly and angularly. Since the bone chain is relatively long, small changes in orientation will still occur in response to acceleration, which combined with the mass scale settings described above gives us a stable simulation with just the right kind of mildly amusing oscillation.

To ensure that the simulation does not explode during extreme acceleration, all the antenna constraints have **Enable Projection** checked, using an **Angular Tolerance** of 1.0, and the **Position Solver Iteration Count** for the bodies has been bumped up to 16.

![Antenna constraint details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8ac358d-b980-4eac-888a-338241b43948/phat_antenna_2.png)

Finally, all internal collision between the antenna bodies as well as the rest of the vehicle's bodies has been disabled to prevent any unnecessary infighting. To do this easily, just select all the bodies in the Skeleton Tree panel, then click the **Disable Collision** button in the main PhAT toolbar.

![Physics bodies selected in the Skeleton Tree panel and disable collision button highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e35c81e-3423-43fe-850c-aeefc997ab55/phat_antenna_3.png)

## Rolling Your Own

Now that you know how this setup works, you will no doubt want to start building your own model to replace this prototype. Below are some pointers that will help you do that with a minimum of headaches.

The first thing is to keep the names and the Skeleton Tree pretty much identical to the prototype. Doing that ensures that the Animation Blueprint can be reassigned and reused on a different Skeletal Mesh without any changes. That will save you a lot of time. All the meshes can of course be remodeled and moved to different positions. Just make sure that everything is properly aligned. Adding more mesh nodes to the model is not a problem, as long as it does not interfere with the overall hierarchy of the key suspension components.

The vehicle root should be placed at 0,0,0 in global space, and must not be rotated in any way. Making the root a simple joint object ensures that FBX export and import will work with a minimum of problems, particularly when using soft-bound components such as the deforming shock meshes.

If your modeling package allows it, set it up to use Z as the up axis. At any rate, assume that X is the forward axis even if your application of choice thinks that Y is forward.

The wheel meshes should touch the floor/grid in your modeling application. Always make sure that the individual components of your model have their pivots at the intended center of rotation, and that their rotation is zeroed out. The obvious exceptions are the shocks, where it makes more sense to orient the root and tip joints towards each other. Unless you know exactly what you are doing, never use any scaling other than 1,1,1, and avoid freezing transforms or equivalent functions.

## Import Options

The following import settings, which were used for the prototype, should be a decent guideline for importing your own custom model:

![Default FBX file import options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95ebca6b-db99-4378-9cf8-14f245d970cc/import_options.png)

Import options used for the prototype vehicle.

...and with that, you should have a pretty good idea about how to build your own advanced vehicle. Good luck!

**Credit**

This project and tutorial are based on work provided by community member Xenome, and are published here with permission.

Thank you, Xenome!