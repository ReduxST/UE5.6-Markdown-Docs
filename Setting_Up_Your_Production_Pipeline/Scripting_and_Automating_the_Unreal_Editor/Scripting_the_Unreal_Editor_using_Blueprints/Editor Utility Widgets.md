# Editor Utility Widgets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/editor-utility-widgets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/editor-utility-widgets-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:49

---

If you want to modify the User Interface (UI) of the **Unreal Editor**, you can use **Editor Utility Widgets** to add new UI elements. Editor Utility Widgets are based on **Unreal Motion Graphics** (UMG), so you can set up Widgets in a Blueprint like you would for any other UMG Widget Blueprint.

These Widgets are specifically for the Editor UI, and you can use them to create custom Editor tabs. You can then select these custom tabs from the Windows menu, like you would select existing Editor tabs.

## Create an Editor Utility Widget

1.  Right-click in the **Content Browser** and select **Editor Utilities > Editor Utility Widget**.
    
    ![Add Editor Utility Widget asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a65d26f-7c6d-4ba1-bbc1-c38d83315395/ue5_1-01-add-asset.png "Add Editor Utility Widget asset")
2.  Name your Editor Utility Widget Asset. In this example, the Asset is named **TestEditorUtility**. Double-click the **Editor Utility Widget Asset** to open the Widget Blueprint for editing.
    
    ![Name your Editor Utility Widget Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bff14ee9-2a4e-44f9-a6cd-7c1eb03cdfb1/ue5_1-02-name-asset.png "Name your Editor Utility Widget Asset")
3.  Edit your Widget Blueprint as needed.
    
4.  Right-click the **Editor Utility Widget Asset** and select **Run Editor Utility Widget** to open an Editor tab with your Editor Utility displayed. The tab is only dockable with Level Editor tabs.
    
    ![Run Editor Utility Widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc4a3195-88a9-4d5e-af10-e62e8cfe84f0/ue5_1-04-run-editor-utility-widget.png "Run Editor Utility Widget")
5.  Once you have run the Editor Utility Widget, it appears in the Level Editor's **Tools** dropdown, under the **Editor Utility Widgets** category.
    
    ![Test Editor Utility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6375cbf4-2555-4116-bf7a-c0d3b380f67a/ue5_1-05-enable-test.png "Test Editor Utility")