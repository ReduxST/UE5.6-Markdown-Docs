# Animation Blueprint Override

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-override-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-override-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:37

---

## Overview

When setting up characters and animation for those characters, there may be instances where you want to have one character perform an animation for an action and have another character perform a different animation for the same action. By using the **Asset Override Editor** inside of a child [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), you can override any previously set animation asset used in a Sequence Player Node allowing you to quickly create variations of Animation Blueprints that each of your characters can use.

Be aware that the only functionality that should be changed via a Child Anim Blueprint is the animation sequences. Changing other properties such as the Skeleton or introducing Animation Layers is not supported.

#### Prerequisites

-   For this guide, we are using the **Blueprint Third Person** template and included the **Infinity Blade: Warriors** and **Animation Starter Pack** assets which are available for free via the Marketplace.
-   We also performed some [Animation Retargeting](/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine) and retargeted the Animation Blueprint and Animations that came with the Animation Starter Pack for use with the Infinity Blade characters.

## Steps

1.  **Right-click** on the **Animation Blueprint** you would like to override animations for and select **Create Child Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85047957-ff4c-46f9-b552-bc7887b2a7da/01_createchild.png)
2.  Open the child Animation Blueprint, then click **Window** from the **File Menu** and select **Asset Override Editor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ee23d7e-5844-469f-b34d-297b46a6a693/02_openeditor.png)
3.  The **Asset Override Editor** will open showing the available animations which can be overridden.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/baa0f3e1-9c1c-4bb8-a919-b3f0a8bc2195/03_assetoverrideeditor.png)
    
    You can expand/collapse the display of assets by clicking the arrow next to each asset.
    
4.  In the **Asset** column, click the drop-down window and specify the new asset to use (which will override the existing when called).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3fb4fd5-c95b-4cd1-b221-f9f02b329456/04_selectassettooverride.png)
    
    Clicking the eyeball icon will allow you to see a preview of the node context in the parent graph as read only in the main graph panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/071254e7-d07b-46d5-b869-40a232af6b74/05_jumptonode.png)
5.  You can view your changes after you click **Compile**.
    

## End Result

Below is an example where a character's default movement (assigned as Jog) in the parent Animation Blueprint is overridden so that the character performs a Walk instead.

A prime usage case for this is if you have a character that performs a certain attack when a button is pressed but you want a different character to have the same general movement but perform a different motion when the attack button is pressed.