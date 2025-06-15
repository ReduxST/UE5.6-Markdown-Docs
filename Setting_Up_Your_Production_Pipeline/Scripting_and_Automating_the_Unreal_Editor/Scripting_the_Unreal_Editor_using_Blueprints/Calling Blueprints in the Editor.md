# Calling Blueprints in the Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/calling-blueprints-in-the-unreal-editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/calling-blueprints-in-the-unreal-editor)  
**Processed:** 2025-06-14 16:11:46

---

You can call **Blueprint Custom Events** and **Blueprint Custom Functions** on demand in the **Unreal Editor**. This can be especially useful any time you need to run the same **Blueprint Graph** both at runtime and in the Editor. For example, you can test or preview your runtime gameplay within the **Editor UI**. However, it can also be a simple way to trigger Blueprints within the Editor that require an **Actor** or a location in 3D space as a context.

## Supported Blueprint Classes

Not all **Blueprint Classes** allow their Custom Events and Functions to run in the Unreal Editor.

-   The steps described below work for any Blueprint Class that you can place in a Level—that is, any class that derives directly or indirectly from **Actor**.
    
-   If you need access to Editor-only features like working with **Assets** in the **Content Browser**, you can derive your Blueprint Class from a placeable Editor-only base class, such as `EditorUtilityActor`. However, keep in mind that you won't be able to trigger your Blueprint at runtime when you use an Editor-only base class, because Editor-only classes are not included in packaged Unreal Engine applications.
    

**Editor Utility Blueprint** classes that derive from the **Actor** base class don't expose buttons in the **Details** panel for any Functions or Custom Events that are marked as callable in the Editor. If you absolutely need to use a button in the Details panel to drive your Blueprint logic, create your graphs in a normal Blueprint class and not in an Editor Utility Blueprint class. However, for a much more flexible and powerful approach to creating a custom UI to drive Blueprint logic in the Unreal Editor, consider using an [Editor Utility Widget](/documentation/en-us/unreal-engine/editor-utility-widgets-in-unreal-engine) instead.

## Steps

1.  Any time you use a **Custom Event** node in the **Event Graph** of your Blueprint Class, you can set the **Graph > Call in Editor** option in the Details panel:
    
    ![Custom Event Call in Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af13f0ac-07fc-4a35-964d-8b3ce1938502/01_custevent_callineditor.png "Custom Event Call in Editor")
    
    Similarly, when you create a new function on your Blueprint Class, you can select the node for your new function and set the same option in the Details panel:
    
    ![Function Call In Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e8941ec-7da4-44c1-8668-82a9d639b0ac/02_custfunction_callineditor.png "Function Call In Editor")
2.  Add an instance of your Blueprint Class into your **Level** if you haven't already.
    
3.  Select the **Blueprint Actor** in the **Level Viewport** or in the **World Outliner**. The Details panel shows a button for each of the **Call in Editor** events and functions you've set up. You'll typically find them in the **Default** section, where Blueprint Classes also expose variables that are marked as Instance Editable.
    
    ![Custom event in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a28f4fd-877a-41b9-a89b-cf89fbeea798/03_bpdefaultcall.png "Custom event in the Details panel")
    
    If your Custom Event or function has any inputs, it will not be shown in the Details panel.
    
4.  Click these buttons to trigger execution of the Event Graphs starting from your Custom Event nodes, or to trigger your custom functions.