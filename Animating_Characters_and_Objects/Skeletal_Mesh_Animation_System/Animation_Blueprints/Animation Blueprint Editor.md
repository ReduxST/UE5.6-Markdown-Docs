# Animation Blueprint Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:23

---

The **Animation Blueprint Editor** shares similar functionality to the [Blueprint Editor](/documentation/en-us/unreal-engine/user-interface-reference-for-the-blueprints-visual-scripting-editor-in-unreal-engine), but contains different features, tools, and windows to aid in character animation scripting.

This document provides an overview of the Animation Blueprint Editor interface.

#### Prerequisites

-   You have created an [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) and opened it.
-   You have a basic understanding of [Blueprint Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine), from which the Animation Blueprint Editor derives much of its interface and behavior.

Upon opening an Animation Blueprint, the following interface will be displayed:

![animation blueprint editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5128e43e-c448-48a4-b981-6cd36ab00fca/editoroverview.png)

1.  [**Toolbar**](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine#toolbar), which contains buttons for Animation Blueprint management and editor type switching.
2.  **Viewport**, where you can preview the behavior of your Animation Blueprint logic on your character. For more information, refer to the [Viewport](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#viewport) section of the [Animation Editors](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) page.
3.  **My Blueprint**, [similarly found](/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine) in the Blueprint Editor, contains a list of your graphs, functions, variables and other related properties within the Animation Blueprint. Also contained here is the **Pose Watch Manager** panel, refer to the [Animation Shortcuts and Tips](/documentation/en-us/unreal-engine/animation-shortcuts-and-tips-unreal-engine#posewatch) page for more information.
4.  [**Graph**](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine#graph), which displays the different graphs for visual scripting in your Animation Blueprint.
5.  **Details**, which displays properties for the selected item.
6.  [**Anim Preview Editor**](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine#animprevieweditor), where you can make changes to your variables and class defaults. Docked on a separate tab is the **Asset Browser** where you can view and open the animation assets that are associated with this Skeleton. Visit the [Asset Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine#asseteditor) section of the [Animation Sequence Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine) page for more information.

## Toolbar

The Toolbar is where you compile your Blueprints, **Save**, locate the Animation Blueprint asset in the **Content Browser**, and define **Class Settings** and **Class Defaults** settings. Several buttons and tools here are common for most Animation Editors, such as **Preview Mesh**. You can learn more about these common menus from the [Animation Editors Toolbar Section](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#toolbar).

![animation blueprint toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ead97a76-8e1d-460b-b362-38870fda85b7/toolbar.png)

The Animation Blueprint Editor Toolbar provides the following buttons and menus:

| Name | Icon | Description |
| --- | --- | --- |
| **Compile** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2017743-62ba-49dd-ab54-4381fd6d4526/toolbarcompile.png) | 
Compiles this Animation Blueprint. This icon will change depending on the compilation state of the Blueprint. In most cases, making changes to any Graph will require you to recompile.

Clicking the **Options** menu will reveal additional behaviors when compiling. **Save On Compile** can be used to automatically save the Animation Blueprint upon compiling. **Jump to Error Node** can also be enabled to automatically frame the graph node preventing a successful compile.

![animation blueprint compile settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f731a825-29b9-4fb4-8ebc-655b1f381c74/compileoptions.png)

 |
| **Diff** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e29ad64-9385-4f26-9e12-9dbd85095f6c/toolbardiff.png) | If you are using a [Source Control Package](/documentation/en-us/unreal-engine/using-source-control-in-the-unreal-editor) in Unreal Engine, then this dropdown menu can be used to compare your current Animation Blueprint against previous revisions. |
| **Find** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa28b284-839c-4ec5-8937-833427893f8b/toolbarfind.png) | Opens a search panel where you can search for references to functions, events, variables, nodes, and pins within all graphs. You can also press **Ctrl + F**. Additionally, pressing **Ctrl + Shift + F** will open a search window where you can search through all Blueprints in your project, Animation or otherwise. |
| **Hide Unrelated** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aade9f5-a91c-4db8-8fc2-0be5b8fa0ea3/toolbarhide.png) | 

Enabling this will fade out any nodes not currently selected or directly linked to your selected node in the Graph. You can also enable **Lock Node State** from the options menu, which will maintain the current hidden state of all nodes, regardless of your selection afterwards.

![animation blueprint hide unrelated](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd9cdaff-02e9-40eb-93ee-5b7ab08e2743/hideunrelated.png)

 |
| **Class Settings** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cd21e3b-a9be-4ec2-8f6d-1b56066bc9b5/toolbarsettings.png) | 

Clicking this exposes several Blueprint class settings in the Details panel. Most of these properties are general [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) class settings. However the following settings are specific to Animation Blueprints.

-   **Target Skeleton**: Specifies the Skeleton Asset to use for this Animation Blueprint.
-   **Use Multi Threaded Animation Update**: Enables the Animation Blueprint to update its native update, blend tree, montages, and asset players on a worker thread. The compiler will attempt to pick up any issues that may occur with the threaded update.
-   **Warn About Blueprint Usage**: Enabling this causes warnings to occur whenever a call into the Blueprint is made from the AnimGraph. This can help locate optimizations that need to be made.



 |
| **Class Defaults** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2835384a-de18-45ac-a336-29185640b731/toolbardefault.png) | 

Clicking this exposes your Blueprint's variables in the Details panel, including default variables from the Blueprint class.

-   **Root Motion Mode**: Controls how [root motion](/documentation/en-us/unreal-engine/root-motion-in-unreal-engine) is applied within this Animation Blueprint. You can select the following options:
    
    -   **No Root Motion Extraction**, which causes no root motion to be extracted or applied.
    -   **Ignore Root Motion**, which extracts root motion, but does not apply it.
    -   **Root Motion from Everything**, which enables root motion from all animation sources. Typically you should not enable this in multiplayer or network setups.
    -   **Root Motion from Montages Only**, which causes root motion to only apply from [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine). This is a more suitable option for multiplayer or network setups.
-   **Receive Notifies from Linked Instances**: Whether to process notifies from any linked anim instances.
-   **Propagate Notifies to Linked Instances**: Whether to propagate notifies to any linked anim instances.
-   **Use Main Instance Montage Evaluation Data**: Enabling this causes linked instances to use the main instances' montage data, synchronizing all instances when the main instance plays a montage.



 |
| **Play / Simulate** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f1fdd62-c2fc-4c17-ba4f-188b70085762/toolbarplay.png) | These buttons can be used as a way to start playing or simulating the Animation Blueprint, using the [In-Editor Testing](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine) framework. |
| **Debug Object** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d93835b9-3ace-456c-aa7b-8d9a4762885e/toolbardebug.png) | This drop-down menu links the Animation Blueprint viewport to an active animation instance in a simulating or playing session. This previews the current animation from that session in the Control Rig viewport. Additionally, your graph nodes will also respond to any inputs and changes that occur in session, so that you can debug your graph and character state. |
| **Animation Editors / Blueprint** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dda3f29d-2168-4a05-a51c-a11394d9dd76/toolbareditor.png) | When creating an Animation Blueprint for a Skeleton, this button will appear as a selectable editor type within the [Animation Editor Modes](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#editormodes) region. Clicking here opens the Animation Blueprint. You can also click the **Options** dropdown menu next to this button to select a specific Blueprint if more than one Animation Blueprint uses this Skeleton. |

## Graph

The Graph panel is where you create the logic that controls your character during gameplay. There are three main types of graphs, each with different interfaces:

-   The **Event Graph**, where you construct Blueprint-based logic to define node properties and variables which inform your other graph areas.
    
    ![animation blueprint event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbaa19d0-5091-4e90-b981-c5c8e71a7e03/graphevent.png)
    
-   The **Anim Graph**, where you construct pose-based logic which evaluates the final pose of the Skeletal Mesh for the current frame.
    
    ![animation blueprint anim graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e875afc6-e44b-44c1-9d07-170d2bb87644/graphanim.png)
    
-   **State Machines**, where you construct state-based logic, typically used for locomotion.
    
    ![animation blueprint state machine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e6b95fa-fe02-46d7-bdfa-bbb871548265/graphstate.png)
    

Visit the [Graphing in Animation Blueprints](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine) and [State Machines](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine) pages for more information about the different graph types and graphing within Animation Blueprints.

## Anim Preview Editor

The Anim Preview Editor is where you can make changes to your variables (including Class Defaults), which will update the Skeletal Mesh in the viewport.

![anim preview editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b74dd6d-c752-4c9e-af68-7d958a9150ce/animpreview1.png)

Clicking **Edit Preview** changes the behavior of this panel so that you are only making temporary edits to your variables. This can be useful if you only want to preview different variable states, without making destructive edits. When you make changes, a prompt will appear where you can choose to apply these changes to the default.

![edit preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d4a1f98-8ccf-4a8b-b0a9-9ee66ca28cb9/animpreview2.png)