# Capsule Shadows Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/capsule-shadows-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/capsule-shadows-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:09

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6577142f-9244-40c5-bc44-4daffd6be9a7/qs_capsuleshadow.png)  
At the end of this guide, you'll have a scene similar to the one above.

### Goals

The Capsule Shadows Quick Start intends to quickly get you up and running with the basics of creating a capsule representation of your character with a Physics Asset and enabling Capsule Shadows for character in your games differently lit environments.

### Objectives

After going through this tutorial, developers will know the following:

-   How to create a Physics Asset for shadows.
-   How to assign the Shadow Physics Asset to your Skeletal Mesh.
-   How to enable Capsule Shadows in your level for your characters.

## 1 - Required Setup

Before we get started, the first thing we'll need to do is to create a new project that we can work from for the rest of this guide. In the steps below, we'll use Unreal Engine 4's Project Browser to create the project. After completing this step, you will have a template that you can build onto for your future projects.

### Steps

1.  Start by opening **Unreal Engine** from the **Epic Games Launcher**. The [Project Browser](/documentation/en-us/unreal-engine/working-with-projects-and-templates-in-unreal-engine) will appear.
2.  Create a new project in the **Games** > **Third Person** template, with the following settings:
    
    -   **Blueprint** enabled
    -   **No Starter Content** enabled
3.  Click **Create Project**.

### End Result

After creating our project, and once the Unreal Editor has finished loading, you will be presented with the Main Editor Interface shown below. In the Content Browser, you will see various folders for the Blueprint Third Person Template that we will use in the next steps.

Click image for full size.

In the next step, we will start by setting up a new Physics Asset for our Third Person Character that will be used for our Capsule Shadows.

## 2 - Your Character - Creating a Shadow Physics Asset

With your project ready to go, in this step, we'll create a new Physics Asset for the Third Person Character's Skeletal mesh that will be used for shadow representation with Capsule Shadows.

### Steps

1.  Inside of the **Content Browser**, use the folder hierarchy to navigate to **Mannequin** > **Character** > **Mesh** folder. Here you will find the asset named **SK\_Mannequin**, which you'll use. Select it, and then right-click, to bring up the context menu. From there, select **Create** > **Physics Asset** > **Create**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7905786d-7ec7-41ca-81f1-2f4f46727145/contextmenucreatepa.png)
2.  After you click Create, the **New Asset** window will open to create the new Physics Asset. Set the **Minimum Bone Size** to 15 and then click **OK**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/483fcef6-3efe-4a39-8b28-c918f896d69a/newphysicsasset.png)
    
    Only use Sphyl bodies for the best result. Sphere bodies will also work, but they are not as flexible in their use with character Skeletal Meshes.
    
3.  Next, the [Physics Asset Tool](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) will open with your new Physics Asset for the Skeletal Mesh `SK_Mannequin`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a725477-2d79-4bec-9609-04da4cce0b75/pa_character.png)
4.  This is an optional step. Before moving forward, it is recommended that you take a moment and give your newly created Physics Asset a name. Do this by minimizing the PhAT window, and in the **Content Browser**, locate the Physics Asset that was created for SK\_Mannequin in your **Mesh** folder. Give it a name so that you can locate it later ("SPA\_Mannequin" would be a good name). Once you've done this, you can maximize the PhAT window again.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f37d976-23c8-4d7d-a736-6980fb391cb7/cb_spa_mannequin.png)
5.  In the PhAT window, you'll now want to adjust the various Physics Bodies, so that the capsule represents the character more accurately. This will require deleting some existing bodies, along with scaling and rotating the remaining ones to better fit. Below, you'll find a list of things you should keep in mind when adjusting and removing your capsules:
    
    -   Limit the number of bodies by removing unnecessary capsules; like hands, arms, multiple capsules for the torso and neck, etc.
    -   Foot capsule placement is very important to make your character look grounded, and may need to be tweaked later to look more accurate.
    -   Use a little bit of overlap between the capsules's joints to avoid gaps in the shadow.
    -   Capsules for the arms are not necessary for this Quick Start and can be removed.
6.  When you are finished with your adjustments, you should have something that looks similar to this. The placement does not have to be perfect and can easily be tweaked later to refine any shadowing issues that you may run into.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/449455cc-940e-45dd-9357-8fd4882ea14d/pa_characteradjusted.png)

### End Result

Now that the Physics Asset for the character's capsule representation is complete, you should be familiar with the process of creating a new Physics Asset and setting it up to represent your character with as few bodies as possible.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a86a6677-d99a-4bce-b727-65b193180521/before.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56e57f2e-b2cb-4c6a-8ea5-77964f74c42c/after.png) |
| Before: 21 Capsule Bodies | After: 10 Capsule Bodies |

In the next step, we'll assign our new Physics Asset to our Skeletal Mesh.

## 3 - Your Character - Assigning the Physics Asset

We created a new Physics Asset for our Skeletal Mesh character that we'll use in this step to assign in the [Skeleton Editor](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine).

### Steps

1.  Inside of the **Content Browser**, use the folder hierarchy and navigate to the **Mannequin** > **Mesh** folder. Select **SK\_Mannequin** asset and double-click to open it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aac0986-73ad-4fe6-b637-197569aa8986/cb_mannequin2.png)
2.  When the Skeleton Editor opens, navigate to the **Asset Details** panel and scroll down to locate the tab for **Lighting**. Click the selection box next to **Shadow Physics Asset** and select the Physics Asset we created in the previous step.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6040fd5a-7fb1-43fd-8a2c-74914e7d632a/assetdetailslighting2.png)
    
    Be vigilant in naming your Physics Assets clearly because when you use the Shadow Physics Asset selection box, all Physics Assets for the project will be listed here.
    
3.  You can now **Save** & **Close** the Skeleton Editor.
    

### End Result

You have now assigned the Physics Asset that you created in the previous step to your character's Shadow Physics Asset slot. This will enable your character to use this Physics Asset for shadowing purposes.

In the next step, we will add our character to the level, and then enable Capsule Shadowing.

## 4 - Your Level - Enabling Capsule Shadows For Your Character

In the previous step, you assigned the Physics Asset to your character in the Skeleton Editor as its Shadow Physics Asset, which, in this step, will enable you to use Capsule Shadowing for your character in directly and indirectly lit areas when enabled.

### Steps

1.  Inside the **Content Browser**, use the folder hierarchy to navigate to the **ThirdPersonBP** > **Blueprints** folder. Select the **ThirdPersonCharacter** Blueprint, and double-click to open it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60565f5c-7b59-4010-b82f-1d9a24f63e9d/cb_tpbp.png)
2.  When the Blueprint Editor opens, use the **Components** window, and select **Mesh (Inherited)**. Then, in the **Details** panel, scroll down and locate the **Lighting** tab. Under the advanced rollout, locate and enable the following:
    
    -   **Capsule Direct Shadows**
    -   **Capsule Indirect Shadows**
        
        Click image for full size.
        
3.  With Capsule Shadows enabled for Direct and Indirect lighting, you can **Save** & **Close** the ThirdPersonCharacter Blueprint.
    
4.  Before we can fully test Capsule Shadows, you'll need to create some indirectly lit areas in your level to use Capsule Indirect Shadows. From your Level Viewport, select the **Floor** Actor, and then hold down the **ALT** key while left-clicking to drag a copy up along the Z-axis (Blue). Move the floor Actor to the top of the outer walls, and then use the X-axis (Red) on the translation tool to move it back, so that only part of the floor is covered. This will give you an area that uses indirect lighting when you rebuild the lighting for the scene.
    
5.  Now, select the **Direcitonal Light**, named "Light Source", from the **World Outliner**. In its **Details** panel, set the **Intensity** for the light to **10**. This will make sure there is enough light to illuminate the area being covered.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43d90ba1-9481-4b43-b1c2-f3c57de924b4/lightsourcesettings.png)
6.  From the Main Toolbar, click the **Build** button so that lighting will be rebuilt for the scene. This ensures that you will be able to use Capsule Indirect Shadows for your character.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd3dab30-42d9-46df-acab-683f2b7330af/buildbutton.png)

### End Result

You now have a character that supports Capsule Shadowing when in direct and indirect lighting. You can **Play in Editor** (PIE) to move your character around the scene to see how the soft shadows look.

You can enable both Capsule Shadow settings individually, such that, if you don't need the soft shadowing while your character is lit in open areas, you can disable this option and leave only Capsule Indirect Shadow enabled for these areas that are indirectly lit.

In the final step, there are some challenges you can attempt on your own, along with reminders for creating a Shadow Physics Asset.

## 5 - On Your Own!

Now that you have created a sample Shadow Physics Asset for Capsule Shadowing, you can try some of the following on your own:

-   Try using different lighting angles, or time-of-day scenarios, for mid-day, dusk, or evening.
-   Adjust the **Light Source Angle** of your Directional Light to soften your Capsule Shadow in areas that are directly lit so that your character blends in with surrounding shadows.
-   Add some closed off areas with doorways and windows (or something similar) to a cave opening, to get contrasting light that gives directionality for the light source when **Capsule Indirect Shadow** is enabled.
-   Use the setting for **Capsule Indirect Shadow Min Visibility** in your Character's Details panel to blend the soft shadow's intensity with your environment.
-   Add some additional capsule bodies for the arms of your character for shadowing when it's near wall surfaces, like with a cover system, or if your character goes prone.

To explore some additional features of Unreal Engine, see the following:

-   For information covering Capsule Shadows, see [Capsule Shadows](/documentation/en-us/unreal-engine/capsule-shadows-in-unreal-engine).
-   For information covering the Physics Asset Tool, see [Physics Asset Tool](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine).
-   For information covering Lighting, see \[building-virtual-worlds\\lighting-and-shadows).