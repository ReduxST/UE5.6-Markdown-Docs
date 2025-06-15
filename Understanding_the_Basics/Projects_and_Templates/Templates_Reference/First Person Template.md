# First Person Template

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/first-person-template-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/first-person-template-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:49

---

When you create a new project, **Unreal Engine** gives you a list of templates you can choose from. These templates contain some ready-to-use Assets, such as level geometry, a character you can control, and simple character animations. Many tutorials use one of these templates as a starting point.

In a **first-person** game, the player sees the game from the viewpoint of the character they are playing as. Some first-person games show parts of the character models, like the character's arms or a weapon. This is different from a [third-person game](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine), where you see the action from a point that's behind and slightly above the character.

The **First Person** template in Unreal Engine 5 contains the following elements:

-   A playable first-person character that can move and shoot.
-   A gun that can be picked up and fires projectiles.
-   A Level with basic geometry (ramps, platforms).
-   Cubes that react when the player or a projectile collides with them.

## Creating a First Person Project

Launching Unreal Engine 5 opens the **Project Browser** window, where you can choose to open an existing Unreal project or create something new. To create a first-person project, select the **Games** category on the left, and then select the **First Person** template.

![Creating a new first-person project in Unreal Engine 5.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b22f825-5d77-4d15-bbf0-f3f38b4ae4fd/create-new-project.png)

Creating a new first-person project in Unreal Engine 5.

There are several additional settings you can configure for your First Person project. For an overview of these, refer to the [Creating a New Project](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) page.

If you want to have some ready-to-use objects to populate your Level with, choose the **With Starter Content** option when configuring your Project Settings. These are great to use while you get used to the controls and workflows in Unreal Engine.

After following these steps, you now have a basic Level with a first-person character you can control using the keyboard and mouse.

Why don't you try out your new Level? In the Main Toolbar, click **Play**, then try to move around and shoot some cubes.

Use the WASD keys to move your character, and look around by moving the mouse. Walk over to the gun to pick it up, then left-click to fire a projectile.

## Template Contents

The First Person template contains all of the basic elements of a simple First-Person Shooter (FPS) game or any other kind of first-person experience. The following section details these elements and where to find them in the **Content Browser**.

### Blueprints

The First Person Template includes Blueprints for the:

-   Player character
    
-   Rifle
    
-   Rifle projectile
    
-   Game mode
    

These Blueprints are located in the `Content/FirstPerson/Blueprints` folder.

Each Blueprint's **Event Graph** includes comments and annotations to help you understand what different node groups do and some of the logic behind the implementation.

Here, you can see some developer comments inside the BP\_Rifle Blueprint. Click the image for full size.

### First Person Character

Assets for the player character are located in the `Content/FirstPersonArms` folder. Here, you can find the Skeletal Mesh, Materials, Textures, and animations for the character.

### Rifle and Projectile

The `Content/FPWeapon` folder contains the Assets for the rifle and projectile. The rifle uses a Skeletal Mesh (**SK\_FPGun**). Projectiles are spawned on left-click and apply a physics impulse to any physics-enabled Actor they collide with in the Level. You can see how this logic was implemented in the **BP\_FirstPersonProjectile** Blueprint located in the `Content/FirstPerson/Blueprints` folder.

### Level

The Assets that make up Level geometry (Static Meshes, Materials, and Textures) are located in the `Content/LevelPrototyping` folder.

## Improving your Project

Now that you have a playable Level, you can start to import content and tweak things to make your game more interesting.

The easiest way to add more content inside your Level is to drag-and-drop it from the **Content Browser**. If you chose to include **starter content** when you created your project, you should already have some additional things you can drag-and-drop into your Level.

For more in-depth instructions on how to populate your Level, see [Level Designer Quick Start](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine).

## What's Next?

Now that you've gone through the basics of creating a first-person experience, here are some other things you can try:

-   [Import and configure](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine) a different model for your gun, or choose a different weapon entirely. You can download premade Assets from [Fab](https://www.fab.com) or create your own.
    
-   Populate your Level with free content and props from [Quixel Bridge](/documentation/en-us/unreal-engine/quixel-bridge-plugin-for-unreal-engine). You can build a variety of indoor and outdoor environments, and new content is added regularly.
    
-   Add some fancy visual effects to your game, like motion blur or vignette, by using [post-processing](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine).
    
-   Create an in-game heads-up display (HUD) with [Unreal Motion Graphics (UMG)](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine) to display information such as player health and ammo count.
    
-   Add AI characters using [Behavior Trees](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine). You can set them up to chase, flee, help, or harm the player.