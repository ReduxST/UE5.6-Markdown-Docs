# Blueprint Editor Toolbar

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/toolbar-in-the-blueprints-visual-scripting-editor-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/toolbar-in-the-blueprints-visual-scripting-editor-for-unreal-engine)  
**Processed:** 2025-06-14 16:54:40

---

The **Toolbar** is displayed at the top-left of the Blueprint Editor by default. The Blueprint Editor Toolbar buttons provide easy access to common commands needed when editing Blueprints. The Toolbar provides different buttons depending on which mode is active and which Blueprint type you are currently editing.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eb2fd31-cd4e-490e-a505-f2841a144e32/toolbarbp.png)

The Toolbar contains two sections:

-   **Toolbar options** - Tools for working with your Blueprint.
    
-   **Mode buttons** - Buttons that you can use to switch which mode your Blueprint is in.
    

## Toolbar Buttons

  

| Button | Description |
| --- | --- |
| ![Compile Successful Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97bc0d03-433f-4488-847c-0c514ba0a8b3/bp_compile_successful.png) | Compilation was successful. Clicking the button compiles the Blueprint being edited. Output from the compiling process is displayed in the Blueprint Log of the Message Log. This button will be inactive during debugging. |
| ![Compile Needed Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d378cab6-61f2-45e4-8760-35b686b76930/bp_needs_compile.png) | The *Blueprint* needs to be recompiled. Clicking the button compiles the Blueprint being edited. Output from the compiling process is displayed in the Blueprint Log of the Message Log. This button will be inactive during debugging. |
| ![Compile Warning Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65ea91ec-3810-4d0c-b51c-bff75e57794e/compile_warning.png) | There was a warning during compilation. Clicking the button compiles the Blueprint being edited. Output from the compiling process is displayed in the Blueprint Log of the Message Log. This button will be inactive during debugging. |
| ![Compile Failed Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb0b0d19-ae5f-47d1-8d34-39290f68250a/compile_failed.png) | Compilation failed. Clicking the button compiles the Blueprint being edited. Output from the compiling process is displayed in the Blueprint Log of the Message Log. This button will be inactive during debugging. |
| ![Save Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77b3b297-f423-4787-b50e-5a0a993008ba/bp_save.png) | Saves the current Blueprint. |
| ![Find in Content Browser Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11a25491-e210-4325-ba94-560cbd7c37e6/bp_find_in_cb.png) | Summons the **Content Browser** and navigates to this asset. |
| ![Search Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efaba039-2093-4ecd-b704-2cc75054225e/bp_search.png) | Finds references to functions, events, variables, and pins in the current Blueprint. |
| ![Blueprint Properties Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/049aec68-29a2-4dc4-b731-d37f2ebe8775/bp_properties.png) | Opens the Blueprint Properties in the **Details** pane. |
| ![Blueprint Properties Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18ddc032-b809-432e-8ec0-5d68d004b5bb/defaults.png) | Shows the Class Defaults Panel in the Details Tab |
| ![Simulate Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98b43edb-575e-4b2b-a84e-796594c411ba/bp_simulate.png) | Starts the game in simulation mode. See the [Simulate In Editor](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine#simulateineditor) section for more information. |
| ![Play In Editor Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf2d13d7-ca33-4cad-9372-5aa238143dd3/bp_play_in.png) | Starts the game in normal play mode. Clicking the arrow displays the **Play Options** menu. See the [Play In Editor](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine#playineditor) section for more information. |
| ![Pause Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4123673-29fb-474a-807b-4c79c9173a81/bp_pause.png) | Pauses simulation. When the simulation is paused, the **Resume** and **Frame Skip** buttons will appear on the toolbar. |
| ![Resume Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff56bcac-2243-42a7-8f19-06cab6d2fbb6/bp_resume.png) | Resumes execution after a breakpoint is hit or the Pause button is pressed. |
| ![Frame Skip Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2021113-e19a-4d31-a993-c52007780d4e/bp_frameskip.png) | Advances a single frame, or tick. This button appears when simulation is paused, or when a breakpoint is hit. |
| ![Stop Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af4ee491-4371-42af-8748-fcd6fa7d0a0f/bp_stop.png) | Halts execution of the game and exits Simulate In Editor mode. |
| ![Possess Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc7e856c-c9d9-4c26-8a20-804a8b87973d/bp_possess.png) | Switches from Simulate In Editor mode to Play In Editor mode. Attaches to the player controller, allowing normal gameplay controls. Toggles with **Eject**. |
| ![Eject Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/713c1748-0986-4e98-b0be-547b15e88346/bp_eject.png) | Switches from Play In Editor mode to Simulate In Editor mode. Detaches from the player controller, allowing regular editor controls. Toggles with **Possess**. |
| ![Step Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63fdf265-8f04-4901-a481-c3b334af9695/bp_step.png) | Steps through execution of the graph one node at a time. This button appears during simulation after a breakpoint is hit. |
| ![Debug Dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18158eb1-ff22-4840-8a82-7a3d4e75d9a8/bp_debug_dropdown.png) | If you have one or more instances of a *Blueprint* in a level, this dropdown allows you to select which instance to debug. |