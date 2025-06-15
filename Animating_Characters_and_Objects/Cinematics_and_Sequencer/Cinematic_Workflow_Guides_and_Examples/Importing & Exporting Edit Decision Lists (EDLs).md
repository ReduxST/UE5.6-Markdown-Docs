# Importing & Exporting Edit Decision Lists (EDLs)

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/import-and-export-edl-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/import-and-export-edl-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:02

---

Sequencer in Unreal Engine not only allows you to render and export your entire cinematic, but you can also export your cinematic split up into each of your shots along with an **Edit Decision List** (**EDL**), which is a file that can be used with most video editing applications like Premiere, Avid or Final Cut.

The EDL contains an ordered list of reel and timecode data representing where each video clip can be obtained in order to produce the final cut. In this how-to, we export a cinematic and EDL file, take it into an external program (like Premiere), make edits to it, and re-import the edited cinematic back into UE4 along with those changes.

## Steps

For this how-to, we are using the **Blueprint Third Person Template** project, having created a sample cinematic; however, you can use your own project and cinematic sequence. We are also using Adobe Premiere Pro CS6 as our external editing software; however, you can use any software that supports EDL importing.

1.  Make sure the cinematic you want to export includes a **Shot Track** containing your shots, then click the **Render Movie** button.
    
2.  Set the **Output Format** to **Video Sequence**, choose an **Output Directory** and **Filename Format** using the **{shot}** token, then enable **Write Edit Decision List**.
    
    Here, we show the sample cinematic that we want to export (along with an EDL), and click the **Render Movie** button to bring up the settings dialog window. Inside the settings window, we create a new folder to export the cinematic to, and prefix our **{shot}** token with the name of our cinematic. By using the **{shot}** token, each of our shots will be exported as individual video files along with the full cinematic.
    
    You must set the **Output Format** to **Video Sequence** in order for this to work, it does not work with individual frames.
    
3.  **Import** the **EDL** file exported from the previous step into your external video editing software.
    
    In Premiere Pro, you can right-click in the lower left of the window, choose **Import**, then point to the EDL file.
    
4.  Link the data from the EDL to the exported media files in your external video editing software.
    
    In Premiere Pro, you can right-click the media folder, select **Link Media**, then point each file to its corresponding media file.
    
5.  Modify the shots in your external video editing software as desired, then **Export** as an **EDL**.
    
    For our sample scene, we adjust the length of the shots as well as re-arrange their position in the sequence.
    
6.  Returning to your Sequence in Unreal Engine, right-click your **Shot Track** and **Import EDL**.
    
    The changes we made externally are now reflected inside our Sequence in UE4.
    

## End Result

The import/export EDL option within Sequencer gives you the flexibility to determine where you want to do your editing. You can do most of your setup inside of Sequencer, then pass your sequence off to an editor that works inside an external application (like Premiere) to perform the final touches, who can then pass it back to you to tweak in Sequencer. By exporting your sequence as an EDL and working externally, you have the ability to add post production effects (or after effects) to your scene before rendering out the final cinematic.

Optionally, when rendering out your sequence and exporting an EDL, you can add **Frame Handles** automatically to each shot, and define the number of frames to include.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0aa5c09b-86dd-4abc-9316-449679c73386/handleframes.png)

These extra frames pad each shot and are cut into and out of by the EDL, which can be used in your external video editing package to adjust the cuts between shots.