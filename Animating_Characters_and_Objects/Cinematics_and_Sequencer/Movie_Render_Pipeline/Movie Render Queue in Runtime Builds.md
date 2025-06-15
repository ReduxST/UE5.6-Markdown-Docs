# Movie Render Queue in Runtime Builds

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-queue-in-runtime-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-queue-in-runtime-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:18

---

In addition to rendering using the **Movie Render Queue** user interface, you can also execute renders using **Blueprints** on runtime distributed builds. This makes it so that renders can be created on end-user devices.

This document provides an overview of how to create renders using Blueprints, and the functions available to you to configure various settings.

#### Prerequisites

-   You have completed the prerequisite steps from the Movie Render Queue section of the [](/documentation/404)page.
-   You have an understanding of using [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) in Unreal Engine.

## Movie Pipeline Subsystem

Movie Render Queue in Blueprints is accessed using the **Movie Pipeline Runtime Subsystem** node. This subsystem features a **Queue** which contains a list of rendering **jobs**. Each job can contain one or more **shots**, and each job also has its own **configuration**, which contains the [render settings](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine) used to render its shots. To render a video, you need to build a list of jobs, allocate them to the queue, then call the Movie Render Queue subsystem's **Executor** to process the queue.

To add this, right-click in the **Event Graph** and select **Engine Subsystems > Get MoviePipelineQueueEngineSubsystem**.

![get movie pipeline queue engine subsystem](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e89ca7b-ce5b-41ee-b5f2-b8c562c943e6/basic1.png)

## Creating a Basic Render

From the **Movie Pipeline Runtime Subsystem** node, there are three main functions and steps required for successfully rendering using Blueprints.

1.  **Allocate Job**, which is a function used to assign a **Level Sequence** to the render job.
2.  **Set Configuration**, which is used to assign a [render configuration](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine).
3.  **Render Job**, which renders the job using the provided sequence and configuration.

### Allocate Job

First, drag off the **Movie Pipeline Runtime Subsystem** node and select **Movie Render Pipeline > Rendering > Allocate Job**.

![allocate job](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c257bfc3-262f-4402-b78e-fd987946d64e/basic2.png)

Connect the **Subsystem** node to the **Target** pin, and then assign the Level Sequence you want to render to the **In Sequence** pin.

![assign sequence to allocate job](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4bcc1b9-d02d-43b7-8b4a-64e33b442077/basic3.png)

### Set Configuration

Next, drag off the **Allocate Job** node's **Return Value** pin and create a **Set Configuration** node.

![set configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eab50e8-f0a6-405d-8426-6a45206e135c/basic4.png)

Assuming you already saved a custom render configuration as a [Preset](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine#preset), assign it in the **In Preset** pin.

![assign render configuration to set configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b54ee001-1eb3-4491-97fd-743881c80565/basic5.png)

### Render Job

Lastly, drag off the **Movie Pipeline Runtime Subsystem** node and create a **Render Job** Function. It should execute after Set Configuration, and **In Job** should connect to **Allocate Job**.

![full render logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73290220-237e-47e2-bf22-a4dc5e0b87c8/basic6.png)

Executing these functions performs a render on the local machine using the sequence assigned in **Allocate Job,** and the render settings assigned in **Set Configuration**.

## Additional Functions and Settings

For more advanced render controls, you can use the following functions and workflows.

### Customize Render Configurations

If you want to edit or create new render settings for a job, you can connect **Get Configuration** and **Find or Add Setting by Class** nodes after Allocate Job.

![customize settings using get configuration and find or add settings by class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7e195d4-03d9-45c2-9605-f9f7f28de19d/additional1.png)

Next, set the specific [export format](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine), [image setting](/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine), or [render pass](/documentation/en-us/unreal-engine/cinematic-render-passes-in-unreal-engine) in the **In Class** pin.

![class settings menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da052d5d-683e-4575-a152-523fba9b85fd/additional2.png)

After you choose a setting, you can now drag from the **Return Value** pin to **get** or **set** property variables related to that setting class.

![settings variables](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64d035d1-a55a-4154-a9fc-c407d90f6351/additional3.png)

If you are building custom render configurations without setting a base configuration, you are required to add a base render pass and output format. Typically this means adding **Deferred Pass** and an output such as **PNG** or **JPG**. Unlike the editor, these settings will not be added by default.

### Canceling Jobs

You can also cancel active render jobs using functions. This can be important as a protection for cases when the simulation ends while a render is ongoing. Without this protection, it could cause the editor to enter into a softlock state.

To cancel all render jobs, connect the **Movie Pipeline Runtime Subsystem** node to **Get Active Executor**, then **Cancel All Jobs**.

![get active executor and cancel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4182342f-949f-452e-8860-b3ddecdbbc8d/additional4.png)

To implement the cancellation as a protection when the simulation ends, create an **End Play Event**, connect it to an **Is Valid** check, then connect **Is Valid** it to **Cancel All Jobs**.

![cancellation protection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c7e1e48-75c9-4282-a6a8-066684fdd5f2/additional5.png)

### Render Finish Event

Render finish events can be created by binding to a custom event from the Movie Pipeline Runtime Subsystem. To do this, drag off the subsystem and select either **Assign On Render Finished** (to create both a **Bind** and **Custom Event** node), or **Bind Event to On Render Finished** (to create only a **Bind** node to connect to an already existing custom event).

![on render finished event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53bb8734-f935-4bdc-bfbc-075766a28dab/additional6.png)

Once connected to a custom event, right-click on the **Results** pin and select **Split Struct Pin**. A Render Finish event outputs the following information related to the render that occurred when this event fires:

![render finish output properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e3a8ed5-484d-415a-8bbe-f6451852108f/additional7.png)

| Name | Description |
| --- | --- |
| **Results Pipeline** | The internal UMoviePipeline object that generated this event. This is an advanced option and is only meant for tracking. |
| **Results Job** | The UMoviePipelineExecutorJob that generated the event. This is the same result as **Allocate Job** earlier, and can be used for tracking. |
| **Results Success** | Outputs **true** or **false** depending on if the render was successful. |
| **Results Shot Data** | This contains lists of the render passes and the file paths for the files that were generated on disk. This can be used in the event you want to load these images for further processing. |

### Change Render UI

The **Debug Widget** is the UI Widget that displays the preview frames of your movie while it renders. You can set the Executor to use a different Debug Widget by using **Set Configuration** from the **Movie Pipeline Runtime Subsystem**.

![render preview user interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70ddeadc-d47b-420e-991b-ba2ee7b550a7/additional8.png)

Select the In Progress Widget Class dropdown menu to select which widget to use. You can select from the following:

-   **MovieRenderDebugWidget**, which is the base class and shows a blank screen.
-   **UI\_MovieRenderPipelineScreenOverlay**, which shows the default rendering progress UI seen above.
-   **UI\_MovieRenderPipelineScreenOverlayBlank**, which shows a blank screen.

![set configuration widget class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d6290ac-671d-407e-9a56-674834dcdf89/additional9.png)

You can create your own custom debug widget by creating a **Widget Blueprint**, then setting its **Parent Class** to **MovieRenderDebugWidget**. You can then select this custom widget as your Debug Widget Class for your Executor.

![movie render debug widget class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee1a6923-dd1b-4e4c-b735-14ac77b105da/additional10.png)

## Limitations

Some settings are unavailable in runtime builds, as they depend on editor-specific functionality. These include:

-   The FinalCut Pro XML output format
-   Object ID render passes
-   Wav Output (unless your application is launched with `-deterministicaudio` and `-audiomixer`).