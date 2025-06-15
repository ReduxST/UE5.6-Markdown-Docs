# Setting Up Explode Animations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-xr-explode-animations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-xr-explode-animations-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:03

---

A common way to interact with an assembly made up of smaller parts is to *explode* it: to break its component parts apart from each other in space, so that viewers can see each individual part on its own as well as how they all fit together.

The Collab Viewer Template includes a Blueprint class that you can use to set up an exploded view of your parts, and to toggle the assembly smoothly between its default view and its exploded view at runtime.

## Setting Up Initial and Exploded Positions

To set up an exploded view for your own content:

1.  Remove any **BP\_Explode** Actors that you have in your scene already. (You can have multiple **BP\_Explode** Actors in your Level, but the Interaction Menu currently only lists one explode animation at a time.)
2.  Make sure you're working in the same Level as the content that you want your Actor to manage. The **BP\_Explode** Blueprint can only work for content within the same Level as itself. For example, if you're working with the default sample content, open the **Levels** window (**Window > Levels**) and double-click **SampleLevel**.
    
    ![SampleLevel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b9956ec-20ad-4e59-9287-91e09a29c2cc/01-levels-window_ue5.png "SampleLevel")
3.  Find the **BP\_Explode** Blueprint class in the **Content Browser**, under the **CollaborativeViewer/Blueprints/Commands/Explode** folder, and drag it into the Viewport. ![Drag and drop a BP_Explode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/924e862c-21d7-4083-b5d1-a1f286800536/02-add-bp-explode_ue5.png "Drag and drop a BP_Explode")
4.  Select the new Blueprint Actor in the Viewport or the **Outliner**.
    
    ![Select the BP_Explode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c91043bc-00af-4672-b8f7-e250c03ffb68/03-bp-explode_ue5.png "Select the BP_Explode")
5.  At the top of the **Details** panel, give your Actor a descriptive name. This name will be visible at runtime in the Interaction Menu so you can trigger and reverse the explode animation.
    
    ![Rename BP_Explode Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adcd4662-0eda-4208-8986-43d97892061f/04-rename-bp_ue5.png "Rename BP_Explode Actor")
6.  In the **Details** panel, find the **Explode** group. You'll use this group of controls to set up the default and exploded views for your assembly.
    
    ![BP_Explode Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54a78e42-01c2-4d10-97ea-75d114014c67/05-explode-details_ue5.png "BP_Explode Details")
7.  In the **Actors Root** list, you'll need to identify which Actors this Blueprint should animate in the Level.
    
    -   You can add each Actor to the list separately.
    -   If all the Actors you want to animate are children of the same parent Actor in the **World Outliner**, you only need to add the parent to this list.
    
    For example, in the image shown above for the previous step, the **Building\_Parrent** Actor is selected. This Actor is the parent of all the default content items that are part of the building. This makes the Blueprint capable of animating all the Actors that make up that building, but not the trees, the transmission assembly, or the exterior ground.
    
8.  When you have all the Actors you need in the list, move them all in the Viewport (if necessary) so that they appear in the arrangement that you want to be their default starting position. Click the **Set Initial Location** button to record these transforms.
    
9.  Now, move all the Actors in the Viewport to the positions you want them to be in when exploded. Click the **Set Explode Location** button to lock in these transforms.
    
10.  You can test the recorded transforms in the Unreal Editor by clicking the **View Explode** and **View Initial Location** buttons. When you click these buttons, all the animated parts should swap between the preset positions in the Level Viewport. They won't animate smoothly the way they do at runtime, but you'll be able to check that the Actor positions in 3D space are set up the way you're expecting.
    
    ![Select View Explode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66e5002c-fbf1-49e9-b404-372085e9bdfd/08-view-explode_ue5.png "Select View Explode")

The **BP\_Explode** Actor keeps lists of the Actors it manages. If you need to modify the objects owned by the **BP\_Explode**—for example, to delete some Actors from the Level or change their parenting hierarchy—you must re-set **both** the initial and explode locations right away *before* you attempt to view either the initial or explode locations in the Editor. If you don't, these lists of Actors may become out of date. This may result in losing the desired placement of some Actors in your scene.

You can add multiple **BP\_Explode** Actors to your Level to animate different parts of your assembly. However, only the first one will appear in the Interaction Menu.

If you do create multiple **BP\_Explode** Actors, don't include any Actor in more than one **BP\_Explode**. If you do, its positions may not end up where you're expecting.

## Switching Between Positions at Runtime

To switch between the exploded and default views at runtime:

1.  Run or test your game, and open the Interaction Menu. (In desktop mode, press **Spacebar**. In VR mode, press the shoulder buttons on the right-hand controller.) You'll see an item at the bottom of the menu with the name of the **BP\_Explode** Actor you created.
2.  Highlight this menu item and select **Execute** to make all parts registered with the same **BP\_Explode** move smoothly from their current location in the Level to their exploded position.
    
    ![Execute command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c1606e7-f1fb-4356-b8ad-925a99002487/collabviewer-explode-menuexplode.png "Execute command")
3.  If you re-open the Interaction Menu while the assembly is exploded, you'll see a **Execute command** option. Select this to return the exploded parts from their current location back to their default starting positions.
    
    ![Back to default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30a2774e-70b5-40f7-aacf-7cc9c14855e5/collabviewer-explode-menubuild.png "Back to default")

The following video shows the custom animation we built in the previous section in operation at runtime.