# Saving and Loading a Session

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-loading-a-session-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-loading-a-session-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:44

---

The host and other participants in a collaborative view can save annotations, measurements, **Xray** transparency state, **3D Cut** sections, and the position of items moved by **Transform**.

## Saving a Session

To save your session, select the **Save** button, type a name for the session, then press Enter.

Click for full image.

Each participant saves their session in their own local copy of the collaborative view package. Sessions are saved in the `YourProjectName/Saved/SaveGames` sub-folder.

The current positions and rotations of you and other participants are not saved.

You cannot modify a saved session or use the name of an existing saved session.

You cannot save and restore sessions while in VR mode.

## Loading a Session

To load a saved session, select the menu next to the **Save** button, then select a session.

Click for full image.

The list of sessions includes those you have saved, as well as those saved by any other participants who are currently connected.

## Load States in the Unreal Editor

You can now reload saved states directly in the editor:

1.  Copy the **.sav files** representing the states you want to reload as well as the **MainSaveGame.sav** file from your Saved / SaveGames folder from your application into the same folder in your project.
    
2.  In the editor, open the **CollaborativeViewer > Blueprints > Tools** folder, select the **Editor\_CollabViewerUtility\_BP**. Right-click and select **Run Editor Utility Widget**.
    
3.  A widget containing the Default state selector will appear, you can now select one of the copied states from the drop down list.
    
4.  You might need to move the camera in the viewport to refresh the parameters.
    

Click for full image.