# Third Person Template

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:28

---

When you create a new project, **Unreal Engine** gives you a list of templates you can choose from. These templates contain some ready-to-use Assets, such as level geometry, a character you can control, and simple character animations. Many tutorials use one of these templates as a starting point.

In a **third-person** game, the player sees the game world from a Camera that's located at a fixed distance behind and slightly above their character. In Unreal Engine, you can control camera distance and position, and adjust it as needed.

The **Third Person** template in Unreal Engine 5 contains the following elements:

-   A playable third-person character that can move and jump.
-   Additional meshes for the character.
-   A Level with basic geometry (ramps, platforms).
-   Physics-enabled cubes that react when the player collides with them.

The template also comes with redesigned Mannequins.

## Creating a Third Person Project

Launching Unreal Engine 5 opens the **Project Browser** window, where you can choose to open an existing Unreal project or create something new. To create a third-person project, select the **Games** category on the left, and then select the **Third Person** template.

![Creating a new third-person project in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d33ae0d2-7bcc-4a62-b872-adcbee3cdec5/create-new-project.png)

Creating a new third-person project in Unreal Engine 5.

There are several additional settings you can configure for your Third Person project. For an overview of these, refer to the [Creating a New Project](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) page.

If you want to have some ready-to-use objects to populate your Level with, choose the **With Starter Content** option. These are great to use while you get used to the controls and workflows in Unreal Engine.

After following these steps, you now have a basic Level with a third-person character you can control.

Why don't you try out your new Level? In the Main Toolbar, click **Play**. Use the WASD keys to move your character, press the Space bar to jump, and look around by moving the mouse.

## Template Contents

The Third Person template contains all of the basic elements of a simple third-person experience. You can use it as a starting point for a traditional role-playing game (RPG), third-person shooter, or any other kind of application. The following section details the main template elements and where to find them in the **Content Browser**.

### Third-Person Character

Assets for the player character are located in the `Content/Characters` folder. By default, the Third Person template starts with the feminine Unreal Engine 5 Mannequin. This folder contains additional Skeletal Meshes for the player character, both in the style of Unreal Engine 5 and the legacy Unreal Engine Mannequin.

![Unreal Engine 5 Mannequins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf511198-2255-4e5d-90e4-9327a3be00f2/ue5-mannequins.png)

Unreal Engine 5 Mannequins.

The new Mannequins in Unreal Engine 5 are named Manny and Quinn.

Unreal Engine 5 Mannequins also come with configurable **Level of Detail (LOD)** settings. LODs help optimize your application for different platforms. For example, applications targeting mobile platforms (Android, iOS) should use less detailed character models. This helps improve your application's performance on these platforms. The Data Asset that controls Mannequin LODs is located in the `Content/Characters/Mannequins/Meshes` folder.

### Animations

Animations for UE5 Mannequins are located in the `Content/Characters/Mannequins/Animations` folder. There are two sets of animations specific to the two Mannequins.

The Animation Blueprints make full use of the new [IK Rig](/documentation/en-us/unreal-engine/unreal-engine-ik-rig) system in Unreal Engine 5. Unlike legacy animations, IK Rig can be used to dynamically modify pose-based solver parameters. An example of this can be seen in the screenshots below: the position of Quinn's feet adjusts dynamically to match the kind of terrain she is standing on.

![IK Rig dynamic pose solvers in action](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fb9d929-56b4-4069-8e53-ca982029cbbb/ue5-mannequin-ik-rig.png)

To see how this was implemented, have a look at the **CR\_Mannequin\_BasicFootIK** rig in the `Content/Mannequins/Rigs` folder.

Also in the `Rigs` folder, the **CR\_Mannequin\_Body** Control Rig Asset can be used to easily pose and animate the Mannequin directly in the editor. To learn more about how to pose and animate with Control Rig, refer to the [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) section of the Unreal Engine 5 documentation.

### Level

The Assets that make up Level geometry (Static Meshes, Materials, and Textures) are located in the `Content/LevelPrototyping` folder.

## Improving Your Project

Now that you have a playable Level, you can start to import content and tweak things to make your game more interesting.

### Character

You can change your character's appearance by changing its **Static Mesh**. As an example, let's change the default Mannequin mesh. To do this, follow these steps:

1.  In the **Content Browser**, go to `Content/ThirdPerson/Blueprints`, then double-click the **BP\_ThirdPersonCharacter** Blueprint to open it in the Blueprint Editor.
    
    ![Opening the Third Person Character Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65cce0d7-e027-42ed-bbaa-e42186a1eb3a/open-third-person-character-bp.png)
2.  In the Blueprint Editor, in the **Components** panel, click the **Mesh(CharacterMesh)** Component to select it.
    
    Click the image for full size.
    
3.  With the **Mesh(CharacterMesh)** Component selected, find the **Details** panel on the right side of the Blueprint Editor. Then, in the **Mesh** section, click the drop-down next to the **Skeletal Mesh** parameter and select `SKM_Manny` from the list.
    
    Click the image for full size.
    
4.  Still in the **Details** panel, in the **Animation** section, set the following options:
    
    -   **Animation Mode**: Use Animation Blueprint
    -   **Anim Class**: ABP\_Manny
        
        Click the image for full size.
        
    -   **Compile** and **Save** the Blueprint.
        
        ![Compiling and saving the Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2d307f3-fc1f-43a2-af82-10adc1c6d7d7/compile-save-blueprint.png)
    -   Click the **Viewport** tab to confirm that the mesh has updated.
        
        Click the image for full size.
        

Your character can already run and jump, but you can also add other types of **character movement**, like walking or crouching. For a detailed tutorial, see [Setting Up Character Movement](/documentation/en-us/unreal-engine/setting-up-character-movement).

### Level

Your Level already has some simple geometry, like stairs and platforms. The easiest way to add more content inside is to drag-and-drop it from the **Content Browser**.

If you chose to include **starter content** when you created your project, you should already have some things you can drag-and-drop into your Level.

For more in-depth instructions on how to populate your Level, see [Level Designer Quick Start](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine).

## What's Next?

Now that you've gone through the basics of creating a third-person experience, here are some other things you can try:

-   [Import and configure](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine) a different model for your player character. You can download premade characters from [Fab](https://www.fab.com), or [use a MetaHuman](https://docs.metahuman.unrealengine.com/en-US/retargeting-animations-to-a-metahuman-at-runtime/) instead.
    
-   Populate your Level with free content and props from [Quixel Bridge](/documentation/en-us/unreal-engine/quixel-bridge-plugin-for-unreal-engine). You can build a variety of indoor and outdoor environments, and new content is added regularly.
    
-   Add some fancy visual effects to your game, like motion blur or vignette, by using [post-processing](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine).
    
-   Create an in-game heads-up display (HUD) with [Unreal Motion Graphics (UMG)](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine) to display information such as player health and ammo count.
    
-   Add AI characters using [Behavior Trees](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine). You can set them up to chase, flee, help, or harm the player.