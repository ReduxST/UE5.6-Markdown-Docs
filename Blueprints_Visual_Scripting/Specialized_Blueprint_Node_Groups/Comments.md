# Comments

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/comments-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/comments-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:18

---

**Comments** can be added directly to single Blueprint nodes, or they can be added as comment boxes to group related nodes and provide descriptions about their functionality. These can be used solely for organizational purposes to make the **Graphs** more readable, but they can also be used for informational purposes as they allow for textual descriptions to be added just like adding comments to code.

## Node Comments

### Creating Node Comments

To add a comment directly to a node in a Blueprint graph:

1.  **Right-click** on the node.
    
2.  Type a comment into the **Node Comment** text box in the menu that appears, then press **Enter**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d28cfbcb-1e9b-4132-a3ad-05e6763607fb/type_node_comment.png)
    
    Your comment will appear in a small comment bubble above the node. Node comments will not scale when the graph zooms.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1138907-9a91-4b08-ac92-94a43effb3c9/commented_node.png)

### Editing and Removing Node Comments

**Right-click** on the node again and change the text in the **Node Comment** text box in the **Right-click** menu to change the comment. Deleting the text and pressing **Enter** will remove the comment.

## Comment Boxes

### Creating Comment Boxes

Creating a comment box is easy:

1.  Select a group of nodes you would like to comment. It is also possible to create an empty comment box first and then arrange the comment box around nodes later or use it as a floating comment in a given area.
    
2.  **Right-click** and choose **Create Comment from Selection** (or **Add Comment...** if no nodes are selected). A new comment box will appear.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c52cafc6-3f98-4fc8-87cf-e80ed2657284/create_comment_from_selection.png)
    
    You can also press **C** to create a comment.
    
3.  Enter your comment into the header of the comment box that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7621530a-3db6-4ff0-a470-016301d97f1f/type_box_comment.png)
4.  The comment box can be resized by dragging the lower right corner. Note that if trying to move the comment box, any nodes that are within the boundaries of the box will move along with it. This serves as a very useful way to rearrange coordinated groups of nodes. This behavior can be changed per-comment in the **Details** tab for the comment box.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a029bb52-4cf1-4113-b4aa-41dc7da10f15/finished_comment_box.png)
    
    The text of comment boxes will scale as the graph is zoomed, so these can be very helpful for at-a-glance overviews of a zoomed-out graph's functionality.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47925e2a-f492-40e6-bf81-afecb22f407c/zoomed_many_boxes.png)

### Editing Comment Box Text

**Right-click** on the header of the comment box, and change the text in the **Node Comment** text box of the **Right-click** menu to change the text of your comment. Press **Enter** to save your new comment.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75b56b01-5ef4-446c-8a9e-df9e6ade701e/rtclick_comment_box_change.png)

Alternatively:

-   Press **F2** with the comment box selected to edit the comment.
-   **Double-click** on the header of the comment box to edit the comment.

### Deleting Comment Boxes

Click on any comment box and press the **Delete** key, or **Right-click** on the header of the comment box and select **Delete** from the **Right-click** menu. Both of these options will delete the comment box but have no effect on the nodes contained within the comment box.

### Comment Box Properties

These comment box properties can be adjusted in the **Details** tab for each comment box. Simply click on the comment box to show its properties in the **Details** tab.

| Item | Description |
| --- | --- |
| **Properties** |   |
| Comment Color | This allows you to change the background color of the comment box. Remember to use Alpha to adjust the transparency of the background. |
| Color Comment Bubble | If this is checked, the **Comment Color** is applied to the comment box. |
| Move Mode | This allows you to set whether moving the comment also moves nodes within the comment (**Group Movement**) or whether the comment can be moved independently without affecting the nodes within it (**Comment**). |