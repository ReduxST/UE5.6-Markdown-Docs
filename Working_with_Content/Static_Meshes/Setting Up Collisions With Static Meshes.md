# Setting Up Collisions With Static Meshes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:28

---

In **Unreal Engine**, you can have **Static Meshes** do many things, such as change its **Texture** or **Material** during gameplay, or move throughout your **Level** using **Sequencer**. It is likely, whatever you have your Static Mesh do in your Level, you do not want to have the player be able to walk or shoot through the mesh. That is where setting up collision on your Static Mesh is useful.

## Set Up

To start, create a new project using the **First Person Game** template and enable **Starter Content.** For more information on creating new projects in Unreal Engine, refer to [Creating a New Project.](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine)

You may already have a level and Static Meshes of your own to work with. If you do, you can skip this step. However, with the template, you can fire projectiles to demonstrate a point later discussed, so using this template may help you follow along.

Click image for full size.

Once the project is open, in the **Content Browser** you can use the search bar or navigate to **Content > Starter Content > Props** to open the **Static Mesh** named **SM\_Door**.

Click image for full size.

Click image for full size.

**SM** in **SM\_Door** stands for Static Mesh and follows the standard naming convention recommended by Unreal Engine. Following a consistent naming convention helps maintain an organized project. To learn more about naming files in Unreal Engine, refer to [Recommended Asset Naming Conventions](/documentation/en-us/unreal-engine/recommended-asset-naming-conventions-in-unreal-engine-projects).

  

Once you have found **SM\_Door**, go ahead and open up the **Static Mesh Editor** by either:

-   **Double-clicking** on the asset.
-   **Right-clicking** on the asset and selecting **Edit** from the context menu.

When the editor opens, you will see something similar to what is shown below:

Click image for full size.

## Collision On a Simple Shaped Mesh

By default, there is no collision mesh set on the door. Without collision, the player can walk through the door.

You can test this by placing the door into your Level before setting up collision, then play the Level.

![No Collision on Static Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a842013-d97c-4db8-a9be-f24a95e60201/no-collision-on-static-mesh.gif "No Collision with Door Mesh")

Also, if you want the door to blow away when you shoot it or fall to the ground when placed in the sky, you will need to set **Simulate Physics** to *true* from the **Details** panel. However, this option is not available by default if the Static Mesh does not have a collision.

Click image for full size.

These effects are undesirable in most cases, so go ahead and set up collision for this Static Mesh.

In the menu bar at the top of the Static Mesh Editor, there is a **Collision** dropdown menu. Click it to see the options for adding collision to your mesh. You can also access these options by clicking the **Collision** dropdown menu in the toolbar (![Collision Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7afee584-df86-4839-b28a-cec5ff7f4440/13-collision-button.png "Collision Button")) . To learn more about the layout of the Static Mesh Editor, refer to [Static Mesh Editor UI](/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine).

Click image for full size.

The door mesh is a rather simple shape. This makes things easy when trying to set up collision for your Static Mesh.

The top three options in the **Collision** menu surround your Static Mesh with a simple collision shape used as the bounds of what can and cannot be blocked or overlapped with your mesh. Below are examples of the door mesh with these collision meshes.

|   |   |   |
| --- | --- | --- |
| ![Sphere 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd9deb8a-52c0-46c9-ae69-a352091685bd/07-sphere-1.png "Sphere") | ![Capsule 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7879d14f-570d-4fd4-9516-7806d9221881/08-capsule-1.png "Capsule") | ![Box 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d633735-c13f-45d8-aa32-d856ba42cf3f/09-box-1.png "Box") |
| ![Sphere 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21fa16f3-e6dc-40d5-bbcc-e8336d3e8c22/10-sphere-2.png "Sphere") | ![Capsule 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a703f71-beeb-4047-b9b3-e4dd41c1c62c/11-capsule-2.png "Capsule") | ![Box 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c131c91-7c9d-4f27-98c8-01372f79359a/12-box-2.png "Box") |
| Sphere Simplified Collision | Capsule Simplified Collision | Box Simplified Collision |

If you already have a Simplified Collision on a mesh and you add another, the new collision does not replace the other collision, but adds to it.

Adding all three of the Simplified Collisions from above gives you something that looks like the image below.

Click image for full size.

To solve this, you can do one of the following:

-   Select one of the collisions and press the **delete** key.
-   Select **Delete Selected Collision** from the **Collision** dropdown menu to remove them one by one.
-   In the **Collision** menu, select **Remove Collision** to remove all collisions on the Static Mesh.

Click image for full size.

After applying the collision, click the collision mesh to notice a translation widget. You can translate, rotate, and scale the collision mesh like you would with any other object within the engine.

## Collision On a More Complex Mesh

Using the simple collision mesh you set up in the last section will work fine for:

-   A Static Mesh that can easily fit into a capsule or box.
-   A Static Mesh where having precise collision does not matter.

However, you may have a Static Mesh with a more complex shape requiring a precise collision. This section will go over how to set that up.

Back in the **Props** folder, within the **Starter Content**, browse to the Static Mesh **SM\_Chair**. **Double-click** on the thumbnail to open it up in the Static Mesh Editor.

As you can see, this mesh already has collision on it, and looks similar to what is shown below:

Click image for full size.

Let's assume you want the player to be able to sit on the cushion of the chair. The default collision mesh of the chair has an invisible barrier that would prevent the player from sitting.

When the player is playing the game, they only see the Static Mesh itself, not the collision mesh. The player would try to sit on the chair and not know why something is blocking their way.

Remove the collision mesh by selecting **Remove Collision** from the **Collision** dropdown menu. You can try to use the primitive shapes you used in the previous section, but as you can see in the images below, none look quite right.

|   |   |   |
| --- | --- | --- |
| ![Chair Sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0af1472-5155-4d2b-bf48-af3fab447190/17-chair-sphere.png "Chair Sphere") | ![Chair Capsule](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc27717d-a9be-40d0-8721-ef29902775dc/18-chair-capsule.png "Chair Capsule") | ![Chair Box](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/193a2612-76a7-4188-942f-14e3b5abf13b/19-chair-box.png "Chair Box") |
| Sphere Simplified Collision | Capsule Simplified Collision | Box Simplified Collision |

It seems none of the primitive shapes quite achieve the precise collision needed. However, you can get closer with the other options within the **Collision** dropdown menu. These options are called the **K-DOP** Simplified Collision generators.

K-DOP is a type of bounding volume, which stands for K discrete oriented polytope (where K is the number of axis-aligned planes). Basically, it takes K axis-aligned planes and pushes them as close to the Static Mesh as possible. You use the resulting shape as a collision hull.

In the Static Mesh Editor K can be:

-   **10** - Box with 4 edges beveled - you can choose X- Y- or Z-aligned edges.
-   **18** - Box with all edges beveled.
-   **26** - Box with all edges and corners beveled.

Click image for full size.

Here is what your chair mesh looks like with 10-DOP, 18-DOP, and 26-DOP respectively.

|   |   |   |
| --- | --- | --- |
| ![10-DOP](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aedfe277-50d0-43de-9ea8-5a4eef972d86/21-10-dop.png "10-DOP") | ![18-DOP](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc424f95-160c-496a-b643-019a5ebd17aa/22-18-dop.png "18-DOP") | ![26-DOP](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f16c9ac-c854-410b-8e59-835aa3a56c6c/23-26-dop.png "26-DOP") |
| 10DOP | 18DOP | 26DOP |

These collision options are closer to the precision needed, but there is still a gap between the cushions that might prevent the player from sitting down in the chair.

Select **Remove Collision** one more time. Next, select **Auto Convex Collision** from the **Collision** dropdown menu.

Click image for full size.

The **Convex Decomposition** panel, pictured below, will then appear in the **Details** panel.

Click image for full size.

The table below describes each option in the **Convex Decomposition** panel.

| Option | Description |
| --- | --- |
| **Hull Count** | Determines the number of primitives to represent the collision mesh. |
| **Max Hull Verts** | Increases or decreases the number of vertices your collision mesh has. |
| **Hull Precision** | Number of voxels to use when generating the collision mesh. |

The higher these values, the more precise your collision mesh will be, but also the more complex. Clicking **Apply** applies these settings to your Static Mesh and makes the collision mesh visible.

|   |   |
| --- | --- |
| ![Auto Convex Collision](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f858e5b-f56d-4670-826b-5183757db731/26-auto-convex-collision-1.png "Auto Convex Collision") | ![Auto Convex Collision](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1773cde4-cb76-4fbc-91e7-12ce31157106/27-auto-convex-collision-2.png "Auto Convex Collision") |
| Default Settings | Max Accuracy and Max Hull Verts |

Another way to set up a precise collision is by using multiple Simplified Collision meshes. If you remember from earlier, creating another Simplified Collision mesh does not replace the original one but adds to it. Also, each collision mesh has its own transform widget allowing you to translate, rotate, and scale individually. You can use this to create a custom collision mesh for your Static Mesh.

To get started select **Add Box Simplified Collision** from the **Collision** dropdown menu. **Click** the collision mesh to bring up its transform widget.

Next, translate, rotate, and scale the collision mesh so that it fits along the arm of the chair down to the ground.

![Custom Box Collision Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a206304-a397-4960-8373-300e6262af0f/box-collision-mesh-around-arm.gif "Collision Mesh Around Arm")

With the collision mesh still selected, duplicate the collision mesh by either selecting **Duplicate Selected Collision** from the Collision dropdown menu or by pressing **Ctrl + D**.

Next, move this collision mesh so that it fits along the other arm of the chair.

Click image for full size.

Duplicate the collision mesh again. With this new mesh selected, move, scale, and rotate the mesh to fit along the bottom of the chair.

Click image for full size.

Duplicate that collision mesh and move it up, so it fits along the chair's seat.

Click image for full size.

Duplicate the collision mesh one more time and rotate it, so it fits along the back of the chair.

When you are done, you will have something that looks similar to this:

Click image for full size.

You could go back and follow the shape of the chair more closely, but for now the current collision mesh will allow a player to sit on the cushion.

## Simulating Physics and Collision Presets

With collision applied to your Static Mesh, it can now simulate physics. Save your chair mesh by clicking the **Save** button on the left of the Toolbar within the Static Mesh Editor.

Next find **SM\_Chair** inside your **Content Browser** and drag it into the level. With it still selected, look at the **Details** panel.

In the **Physics** section of the **Details** panel, the **Simulate Physics** option is now available and will be *false* by default. If you play the Level now with Simulate Physics set to *false*, walking into the chair or shooting projectiles at it has no effect. However, your character can not walk through the chair as it now has a collision.

To shoot projectiles at the chair using the First Person Shooter template, you need to walk your character into the weapon to collect it, then **Click** to shoot.

Click image for full size.

Stop playing the Level and set **Simulate Physics** to *true*. Now when you play, notice the chair moves when the player walks into it. The Static Mesh also gets shot across the level and into the air when you shoot at it.

![Simulate Physics Active for Static Mesh Collision](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba097032-a1cf-4d44-896b-6a1bf456d72f/simulate-physics-active.gif "Simulate Physics Active")

This is not only because the Static Mesh is simulating physics, but also because the mesh is set to **Physics Actor** by default under **Collision Preset**.

Go back to the **Details** panel for the chair and in the **Collision** section, there is a dropdown menu labeled **Collision Presets**. The way this instance of the Static Mesh reacts to other objects in the world depends on what its **Collision Presets** are. Take a look at the options you have, which are shown below.

Click image for full size.

If you switch it to **Overlap All**, as soon as play begins, you see the Static Mesh fall right through the level. There is also a custom preset, which allows you to manually set how the mesh responds to different objects in your level.

You may want it to block Pawns, but overlap Projectiles, and ignore everything else. In the custom preset, you can tell the Static Mesh to do that.

When selecting a **Static Mesh Actor** in the level editor, or any **Static Mesh Component** such as those in the Blueprint Editor, the **Details Panel > Collision Category > Collision Presets** will show **Default**. This indicates there has been no change to the Collision Preset from what it was initially set to. If something else is listed here, such as **BlockAll**, that indicates the selected Static Mesh Actor / Component has had its Collision Preset overridden.

Click image for full size.

Now that you have collision set up on your mesh, you are ready to place it in your Level and use its collision to set up how it affects and can be affected by other objects.

To continue learning about collisions in Unreal Engine, refer to the [Collision](/documentation/en-us/unreal-engine/collision-in-unreal-engine) documentation.