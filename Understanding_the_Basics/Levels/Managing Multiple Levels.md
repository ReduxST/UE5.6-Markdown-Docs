# Managing Multiple Levels

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/managing-multiple-levels-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/managing-multiple-levels-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:55

---

When working on **Unreal Engine** 4 legacy projects or non-game projects such as architectural visualization, you can use the **Levels** window for level management. For game development in Unreal Engine 5.0 and beyond, the **Levels** window has been made obsolete by [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine). This page covers managing multiple levels through the **Levels** window.

The steps uses the [Architecture template](/documentation/en-us/unreal-engine/unreal-engine-templates-reference#architecture,%20engineering,%20and%20construction%20templates) as a reference.

You can access the **Levels** window from the **Windows** menu.

![Acess Level Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97f47a1f-4282-4b35-8f5a-594c2339669e/ue5-levels-window.png)

You will always have a **Persistent Level**, and you can have one or more sublevels that are always loaded or are streamed in with **Level Streaming Volumes**, **Blueprints**, or **C++ code**. The **Levels** window shows all of these levels, enabling you to change which level is current (indicated in bold blue text), save one or more levels, and access Level Blueprints. If changes are made in the Level Editor's Viewport, you will modify the current Level. You can use this window to work on multiple maps, as long as they are all writeable.

![Persistent Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1166e77-298f-4f2a-9a04-1cf2c6a0c702/ue5-persistent-level.png)

By right-clicking on the **Persistent Level**, you can perform operations like making it the current level, changing its visibility and lock status, and selecting all the Actors in that level.

![Persistent Level Context Menu ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c73dba56-6317-4805-9b3c-472bc61ed82e/ue5_right_clicl_persistent.png)

Right-clicking on any sublevel provides similar options, with additional entries for removing the sublevel and changing its streaming method.

![Sublevel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a698ab49-a9fb-42fa-8b90-951eb33ca6a0/ue5-sub-level.png)

Changing a Level's visibility is for visualization purposes only and does not effect whether or not a level will stream into the game when it is run. However, a Level that is not visible here will not be affected if you rebuild the Level, which can be a great timesaver if you have complicated levels.

## Adding New Sublevels

You can create sublevels by splitting off part of an existing Persistent Level or sublevel, by creating a new Level, or by adding an existing Level. Adding a new sublevel makes it the current Level, so if you want to continue working in the level you were using before the addition, make sure to right-click on it and select **Make Current** from the context menu.

### Adding an Existing Level

1.  Click on the **Levels** dropdown menu, then select **Add Existing** to add a new sublevel.
    
    ![Add Existing Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddf671d2-1df4-4120-b50f-806e6ace66af/ue5-add-existing.png)
2.  Select your Level to add in the **Open Level** dialog, then click on **Open**.
    
    ![Open Existing Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb6ba7ac-0fcf-4346-b1b7-997dbb92c46d/ue5-open-existing-level.png)

### Creating an Empty Sublevel

1.  Click on the **Levels** drop-down menu, then select **Create New** to create a new blank Level.
    
    ![Create a new sublevel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9e5a8ab-b1e8-4089-873c-6b4695b35c94/ue5-create-new.png)
2.  Choose to create a blank level or template
    
    ![Create a blank or template based sublevel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b309f04-5395-415b-83f8-14a86d2e4f03/ue5-choose-level-creation.png)
3.  Select a save location and a name for your Level, then click on **Save**.
    
    ![Save New Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b3fb21a-d48f-4fad-bbc9-bdb73e0fb639/ue5-save-new-level.png)
    
    The new Level is added as a sublevel of your current Persistent Level, and it will also be the current Level for working in the **Viewport**.
    

### Splitting Off Sublevels

If you've already created a Level, and later decide you want to split part of that Level off for streaming or for collaboration with a team, you can use it to create a new Level with Actor.

1.  Select the Actors you want to move to the new Level in the **Scene Outliner** or in the **Viewport**.
    
2.  In the **Levels** window, click on the **Levels** drop-down menu, then select **Create New with Selected Actors** to create a new Level.
    
    ![Create New with Selected Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f98c79e0-4d2a-428c-89ab-e34eca7975b0/ue5-new-level-from-actors.png)
3.  Select a save location and a name for your Level, then click on **Save**.
    
    ![Save Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/581c19bc-ec6b-4f41-8253-421ac67be3d6/ue5-name-new-actor-level.png)

All your selected Actors will be removed from their original Level and added to the new one, which will be added as a sublevel of your current persistent Level and made the current Level for working in the Viewport.

If you are moving an Actor that another Actor that remains in the persistent Level references, you will get a pop-up message asking if you really want to delete it from the persistent Level.

![Delete New Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c2947bc-ae67-44e5-bb0b-54a243ec66a8/deletenewlevel.png)

## Moving Actors Between Levels

While you can copy Actors from your active Level, then switch active Levels to paste Actors, there is a simpler way to move Actors between Levels.

1.  Select the Actors you want to move to the new level in the **Scene Outliner** or in the **Viewport**.
    
2.  **Right-click** on a Level in the **Levels** window, then select **Move Selected Actors to Level** from the context menu.
    
    ![New Level from Actor Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/958eb163-004c-44eb-8b91-2d7f47ba0953/ue5-move-actors.png)
3.  Press **Ctrl+S** to save all Levels.
    

## Level Details

The **Level Details** button is indicated with a magnifying glass in the **Levels Window**, and provides you access to additional information about your current Levels. To set Level Streaming Volumes, you need to open the **Level Details** for your streaming Levels; for more on this process, see [Level Streaming Volumes Reference](/documentation/en-us/unreal-engine/level-streaming-using-volumes-in-unreal-engine).

![Level Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea576879-488a-4add-9b37-e78448cde20a/ue5-level-details.png)

No additional details are visible for persistent Levels, although there is a drop-down menu you can use to change to another Level.

![Persistent Level Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/933b2829-e130-4114-abf1-ecce6af3f7ca/ue5-persistent-level-detail.png)

For sublevels, you can set the Level's offset **Position** and **Rotation**, the **Streaming Volumes** to use, and the debug **Level Color**. Advanced settings like the minimum time between unload requests to improve performance are also accessible here.

![Level Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/289e79ba-ba68-452b-84bd-ce1ed0e57c5e/ue5-sublevel-details.png)

## Visualizing Sublevels

You can set the color of sublevels either in the main **Levels** window or in the **Level Details** window.

To toggle showing the level color, use the **Show** button on the viewport, then select **Advanced > Level Coloration**.

![Level Coloration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/362fcdc6-e682-4714-a74d-b7290ee263e4/ue-level-coloration.png)

The persistent level will be shown in white, while all sublevels will be indicated in their selected colors. **Level Coloration** works in perspective and orthographic viewports, and will be toggled off with **Game Mode**.

![Viewing Level Coloration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60ccc3bf-efd6-4e71-bc94-83502ab519f6/ue5-social.png)