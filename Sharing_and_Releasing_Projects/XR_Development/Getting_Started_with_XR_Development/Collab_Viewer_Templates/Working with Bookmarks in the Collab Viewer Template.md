# Working with Bookmarks in the Collab Viewer Template

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-bookmark-in-the-collab-viewer-template-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-bookmark-in-the-collab-viewer-template-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:36

---

The Collab Viewer offers a built-in type of Blueprint Asset called a **BP\_Bookmark**, which you can use to set up predetermined locations and camera views in your Level. Users can easily teleport to these predetermined locations at runtime.

This page explains how to place new Bookmarks into your Level, and how to set up hotkeys that teleport the user between different Bookmarks when they press number keys on the keyboard.

## Placing a Bookmark

You can place new Bookmarks anywhere in your Level. However, it's best to make sure that each new Bookmark is:

-   At ground level.
-   Immediately above a Static Mesh that has a Collision Mesh set up for it, as instructed in [Adding Your Own Content to the Collab Viewer](/documentation/en-us/unreal-engine/adding-your-own-content-to-the-collab-viewer-in-unreal-engine).

Otherwise, if the user is in Walk mode or in VR, they may fall to the ground or through the ground after the teleport.

### Steps

To place a Bookmark:

1.  Each Bookmark is represented in the Level by an instance of the **BP\_Bookmark** Blueprint class. You'll find this class in the *CollaborativeViewer/Blueprints/Commands/Bookmark/BPs* folder of the **Content Browser**.
    
    ![BP_Bookmark Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58923d88-2c41-40e9-9831-bd2f21a20bd5/01-select-bp-bookmark_ue5.png "BP_Bookmark Asset")
2.  To set up a new Bookmark, drag the **BP\_Bookmark** from the **Content Browser** into your Level.
    
    ![Drag a Bookmark into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2e8a9b1-3e6a-4644-9beb-26068fdd59e3/02-add-to-viewport_ue5.png "Drag a Bookmark into the Level")
3.  Select the Bookmark Actor in the Viewport or the **Outliner** and move it to the position and rotation that you want it in the Level.
    
    Make sure you're moving the Bookmark Actor, and not just its child Camera Component.
    
    **Piloting** the Actor is a fast and easy way to set its viewpoint the way you want it. See [Pilot Actors in the Viewport](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine).
    
4.  In the **Details** panel, find the **Hotkey** setting in the **~ Bookmarks** section, and set the hotkey that you want to assign to the new Bookmark.  
    You can enter the number you want to assign directly in the **Hotkey** field, or use the **Assign Unused Hotkey** button to assign the Bookmark the lowest available numeric key.
    

### End Result

Users who join the session in desktop mode can teleport to your bookmark location by pressing the hotkey you assigned, by using the Bookmarks menu in the toolbar, or by using the **Bookmark** item in the Interaction Menu.

See also [Interacting with the Collab Viewer Template](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine).

## Saving Bookmarks during a Session

During a session in the Collab Viewer, you can record your current position as a new bookmark. The new bookmark will then appear in the Bookmark menu list as an option, and it will be saved and available on reload.

To save a bookmark:

1.  Move to the location where you want to save a bookmark.
    
2.  Open the **Interaction** menu, and select **Bookmark**.
    
3.  In the **Bookmark** menu, select **Create Bookmark**.
    
    ![Create bookmark in the interaction menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5157be47-7a50-4170-af7a-7d791cc4a9ce/04-create-bookmark_ue5.png "Create bookmark in the interaction menu")
4.  Give your new Bookmark a name, and click the **+Add** button.
    
    ![Name and save a bookmark](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/afce8974-401f-4abd-bcb5-89d1cc064075/05-add-bookmark_ue5.png "Name and save a bookmark")
5.  You can delete saved Bookmarks by clicking the **bin** icon next to a saved Bookmark in the **Create Bookmark** menu.