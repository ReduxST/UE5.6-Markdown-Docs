# Rendering your Niagara Systems

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-your-niagara-systems](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-your-niagara-systems)  
**Processed:** 2025-06-14 16:47:01

---

## Configuring your Project

Before creating a Level Sequence, click **Settings > Plugins** to open the **Plugins window** and **enable** the following plugins:

-   Niagara MRQ Support
-   Niagara SIM Caching

Restart the editor if prompted. Now you are ready to create your Level Sequence.

## Creating a Level Sequence

Follow these steps to create a **Level Sequence** with a **Camera** and generate frames with the **Movie Render Queue (MRQ)**:

1.  Right-click in the **Content Browser**, navigate to **Cinematics** and create a **Level Sequence**.
2.  Rename your Level Sequence to something appropriate.
3.  Double-click the Level Sequence to open it.
4.  Click the **Camera** button at the top of the Sequencer panel to create a new **Cine Camera** and a **Camera Cuts track**.
5.  Use the 3D view controls to position your camera to a framing that you like.

## Rendering Frames with Movie Render Queue

1.  Press the **Clapper Board** button on the top of the **Sequencer panel** to open **Movie Render Queue (MRQ)**.
2.  If you have ffmpeg configured:
    -   Click on the **Settings** for your sequence, probably called '**Unsaved Config**'.
    -   Press the **+Setting** button
    -   Add a **Command Line Encoder** settings block.
    -   Press the **Accept** button to leave the Settings dialog.
3.  On the Movie Render Queue panel, press the **Render (Local)** button.

MRQ will now run. It may compile necessary shaders as a first step before showing you a preview of the frames being generated.

If you do not have the FFmpeg codec installed on your computer, read the [How to use FFmpeg with the Command Line Encoder in Movie Render Queue](https://dev.epicgames.com/community/learning/tutorials/BbYV/unreal-engine-how-to-use-ffmpeg-with-the-command-line-encoder-in-movie-render-queue) document to learn how to install it.