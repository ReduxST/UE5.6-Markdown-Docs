# Import a MetaHuman to the Game Animation Sample Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/import-a-metahuman-to-the-game-animation-sample-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/import-a-metahuman-to-the-game-animation-sample-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:59

---

The [Game Animation Sample Project](/documentation/en-us/unreal-engine/game-animation-sample-project-in-unreal-engine) is an example project that you can download to access a suite of motion capture animations, and learn how to use Motion Matching in Unreal Engine. The project contains a sample MetaHuman, with preview meshes for all MetaHuman body types, that you can enable in the Game Utility Widget, to observe how the system functions when using a MetaHuman character. This example project exemplifies the premiere example for using a MetaHuman as the player character, with a high-fidelity animation system.

It is also recommended that you try importing and implementing your own MetaHuman character to observe how the system functions for your own character. You can use the following documentation to learn how to import and implement your own MetaHuman character to the Game Animation Sample Project.

#### Prerequisites

-   You have downloaded and created a new project using the Game Animation Sample Project template. For more information about setting up the Game Animation Sample project for the first time, see the [Game Animation Sample Project](/documentation/en-us/unreal-engine/game-animation-sample-project-in-unreal-engine) documentation.
    
-   You have a MetaHuman character you would like to implement in the Game Animation Sample Project. For more information about creating and adding a MetaHuman to an Unreal Engine project, see the following documentation.
    

%metahuman-creator:topic%

%downloading-and-exporting-metahumans:topic%

## Implementing your MetaHuman

1.  Navigate in the Content Browser to `Content/Blueprints/RetargetedCharacters`.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efa8f089-b4b2-42a5-bfe5-65461bfa5c37/image_0.png)

1.  Locate the `CBP_SandboxCharacter_Metahuman_Kellan` Character Blueprint, and duplicate the asset by right-clicking the asset and navigate to the Duplicate option in the Context Menu.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4a0ffb2-f32e-49d6-960c-1453d9b2c03a/image_1.png)

1.  Open your new duplicated Character Blueprint.
    
2.  In the Blueprint Editor’s components panel, select the **Body** Skeletal Mesh Component and all of its Child Components, and the **LODSync** component, and delete them using the delete key, or by right-clicking the selected components and selecting **Delete** from the context menu.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bda99cc-ed70-4104-a9a3-77e0345a622d/image_2.png)

1.  Open the MetaHuman Blueprint that you would like to add as a player in the Game Animation Sample Project. In this example workflow Danielle is used.
    
2.  Select the Body including the child components and the LODSync component again, right-click the selected components, and select **Copy** from the context menu.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17b75f59-edfb-4741-9e72-aa32475ec9d8/image_3.png)

1.  Back in the Character Blueprint and paste the components onto the existing Mesh component, by selecting and right-clicking the Mesh Component, and selecting the **Paste** option in the context menu.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02d4ea9a-ca73-4341-917e-ca9efc93e7ba/image_4.png)

1.  Reparent the Body Mesh Component to the Blueprint Mesh Component, by selecting and dragging the Body onto the Mesh in the **Components** panel.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07f54a5c-8476-4d2b-8e08-3f6bc67f4113/image_5.png)

1.  Select the Body component to open its **Details** panel, and then navigate to the **Anim Class** property and select the `ABP_GenericRetarget AnimBP` animation blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/220b4ed4-5e0f-49a4-8176-9619b8e8a9ae/image_6.png)

1.  Additionally, you will need to let the Retarget AnimBP know about the new body type, by adding a tag to the Body Mesh Component. In the **Details** panel, navigate to the Component tags property, and add a new element to the array using (**+**) **Add**. Then using the array’s text field, input the following tag:

`RTG_UEFN_to_Metahuman_nrw`

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bed2e00-2613-496e-af50-dce9dd6a4c20/image_7.png)

1.  Open the **Viewport** panel within the Blueprint Editor.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ebdcb41-dca0-4260-b5c5-c9765ca6caea/image_8.png)

1.  Align the MetaHumans Mesh with the capsule component, by selecting the Body component, and transforming the mesh down so their feet match with the Capsule’s button, and Rotate the MetaHuman so it faces the arrow in forward direction.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9653bd76-4e27-4d3d-89b7-869e973c148c/image_9.png)

1.  Next you will need to repair the Construction Script. Open the Construction Script by selecting it in the **My Blueprint** panel, then re-add the Feet, Legs, and Torso get reference variables, by dragging each component into the graph, so that each Enable Master Pose node has a definition.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af146311-2a5d-4b86-9ce8-a435b1aece77/image_10.png)

1.  Then open the `EnableMasterPose` function in the **My Blueprint** panel in order to rebind the Body reference variable. Drag the **Body** Mesh Component into the graph, and connect its output pin to the **Ne****w Leader Bone Component** pin of the existing **Set Leader Pose Component** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c7d94c6-7f7a-4c35-8a6b-f537859befab/image_11.png)

1.  After setting and connecting your Skeletal Mesh Component reference variables, **Save** and **Compile** your Character Blueprint.

## Add Your Character to the Game Animation Widget

1.  Open the Game Animation Widget asset, which can be found in the **Content** > **Widgets** folder path.
    
2.  In the Widget Editor’s **Designer** panel, copy one of the character tiles and paste it right next to the last one on the right.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52848c05-7844-4d93-bf9d-4a9af4c890b7/image_12.png)

1.  Select your new Tile to open its **Details** panel, and then in the Object property, select the **Character Blueprint** that you created using the asset selection menu.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/277e5d93-d198-40ec-8c69-048e8d14ac5f/image_13.png)

1.  Finally **Save** and **Compile** the Game Animation Widget.

You can now play the project using PIE and use your new button in the Game Animation Widget to swap the player to be your new MetaHuman character, using the project’s animation system.