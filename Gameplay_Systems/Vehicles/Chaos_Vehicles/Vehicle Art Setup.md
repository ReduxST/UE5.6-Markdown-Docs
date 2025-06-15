# Vehicle Art Setup

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vehicle-art-setup-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/vehicle-art-setup-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:43

---

The basic, bare minimum, art setup for a vehicle is just a **Skeletal Mesh**. The type of vehicle will decide how complicated an art setup you will need, and special consideration may need to be given to the suspension. A tank does not need to have a crazy suspension setup, because it will almost always go unseen, but a dune buggy, such as the one in **Vehicle Game**, will require more joints to make all the exposed components move in a believable way.

## Basics

The vehicle mesh should point down Positive X.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a75f84c-5032-43b6-8bf8-5cc2a054180b/basics01.png)

You will need to measure the radius of your wheels, in centimeters, for use within Unreal Engine.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25bbf086-d430-4fea-a990-e736c5b5e50e/wheelradius.png)

In the image above, the Distance Measurement tool in Maya is being used to get the diameter of the wheels based on the distance between 2 vertices opposite each other on the wheel. The radius of the wheel is half of this value.

A similar tool exists in the Helpers section of 3D Studio Max.

## Joints

The absolute minimum number of joints required for a 4 wheeled vehicle, is 5:1 root, and 4 wheels. The wheel and root joints should be aligned with X forward, Z up:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8bcf5d-1717-47de-a750-e2bf2e03dcc0/wheeljnt.png)

This will ensure they roll on the Y axis and steer on the Z axis.

All other joints can be arranged as you see fit, but it should be noted that things like **Look At** nodes for the **Animation Blueprint** assume X forward.

To prevent visual oddities, the joints for the wheels should be accurately centered. The visual mesh will not be used for collision detection, however, if the wheel mesh is off center, then it will look like the wheel is broken, and will be really noticeable due to motion blur.

## Binding

Standard smooth bind for Maya or Skin Modifier for 3DS Max. Wheels should only have weighting to one joint, so they can spin free with no odd deformation. For shocks and struts, you can get away with some fancy skinning, but it will require more thought on the Unreal Editor side.

## Export

Vehicles are exported as **Skeletal Meshes**, with no special considerations.

## Import

Vehicles are imported using the standard FBX import for a Skeletal Mesh. You will want to enable the importer's **Create Physics Asset** option.

## Physics Asset

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4069d4f-3c16-4421-bb88-e2ad696f9151/paicon.png)

The Physics Asset is incredibly important for vehicles, and cannot be overlooked or skipped. When you first have Unreal Engine create a Physics Asset for you, it will probably end up looking much like this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03672d26-0ee8-4487-a099-9eda2955227f/badpa.png)

That is because the **Physics Asset Tool** (**PhAT**) attempts to wrap the vertices skinned to a joint the best it can. However, you are going to delete and recreate them all. Why? The PhAT does not currently have a way to gracefully handle the re-creation of the constraints that hold all the Physics Bodies together. So if you delete an intermediate Physics Body, it does not create a new constraint up the hierarchy. However, if you delete all the Physics Bodies and start building them from the Vehicle root joint out, all your constraints will get created correctly.

In the **Skeleton Tree** panel with the default display options (Physics Bodies only), select and delete everything. This will remove all Physics Bodies from the asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeba7ad7-ceda-4f7a-9ecb-f1990cd9068b/selectalldelete.png)

### Physics Body Creation Set-up

1.  Open the **Skeleton Tree** panel **Options** dropdown menu, and select **Show All Bones**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/592de346-265c-46f6-9386-f65124f1c7c4/showbones.png)
2.  At each creation step, check that the **Body Creation** settings in the **Tools** panel are what you need; there are two settings in particular to pay attention to
    
    -   **Min Bone Size** defines how large a bone must be for a Physics Body to be created for it, make sure it is set for an appropriate size for your Skeletal Mesh. In this example, we set it to 5.
    -   **Primitive Type** controls the basic shape of the Physics Body created, you will need to change the type depending on the Physics Body being created.
    -   For the purposes of this example, the other options can be left as is.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/735d5aee-a4af-456e-9f76-4704af28068d/bodycreation.png)

### Create the Body Collision

Now, starting with your root joint, start creating physics bodies. Keeping in mind, you only need a physics body on a joint that either needs to be physically simulated or affects the bounds of the vehicle.

In the case of our buggy here, a box for the body and spheres for the wheels will be just fine to start, but it will require a number of other Physics Bodies to get the desired behavior.

1.  Change the **Body Creation Primitive Type** to **Box**.
2.  Right-click the **rootJNT** bone in the **Skeleton Tree** panel to open the **context menu**.
3.  Select **Add/Replace Bodies**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ad06287-0a27-46eb-9f99-b42aea37a0f9/bodytoroot.png)
4.  You can then **move**, **rotate**, and **scale** the new Physics Body to better approximate the shape of your vehicle
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9544a078-1596-4e6d-a659-4ddab5606f40/newbodyboxresultscaled.png)

The Physics Body created will be the root of the hierarchy of Constraints and Physics Bodies created for the rest of the mesh. You can see the relations directly in the **Graphs** panel, and alongside the bones in the Skeleton Tree panel.

### Create the Wheel Collision

To create the spheres for the wheels:

1.  Change the **Body Creation Primitive Type** to **Sphere**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ab0c910-483b-4aa2-9997-87e27ab8beb4/bodycreationsphere.png)
2.  Select the wheel joint bones in the **Skeleton Tree** panel, then right-click to open the **context menu**.
3.  Select **Add Replace/Bodies**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab838c7b-a6a3-4175-8da3-3c0c7dacca9d/bodytowheel.png)
4.  Select the newly created Physics Bodies for the wheels, then right-click to open the **context menu**.
5.  Under **Physics Type**, select **Kinematic**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34810c01-0dd2-440c-ab7c-65b36a882b9e/makethewheelskin.png)
    
    You can also change the **Physics Type** from the **Details** panel in the **Physics** section.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/042f5960-86ca-4e79-aafa-7d8160a80d35/makethewheelskin_2.png)
    
    This is necessary for the wheels to affect the bounds of the vehicle so shadows and culling occur correctly, and also, to prevent them from just rolling off the vehicle once your game begins.
    
    The wheel Physics Bodies are never actually used for collision. Currently, the wheels use a ray casting for interacting with the world.
    

### Taking it Further

This is just a simple setup for a basic imported vehicle mesh. If you examine the Physics Asset for the Vehicle in Vehicle Game, it looks like this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d858b023-b4e7-4906-a167-db017825df72/goodpa.png)

Outside of the wheels, all of those collision bodies exist on the root joint of the vehicle. They prevent the wheels from getting jammed on certain game elements, and also prevents the meshes of the wheels from clipping through walls and railings.