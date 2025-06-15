# Adding nDisplay to an Existing Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-ndisplay-to-an-existing-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-ndisplay-to-an-existing-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:03

---

You don't have to use the nDisplay Template Project in order to render through nDisplay. If you already have a different Project set up with your content, you can adjust that Project so that it can take advantage of nDisplay.

To set up an existing Project to use nDisplay:

1.  Enable the nDisplay plugin.  
    In the Unreal Editor, choose **Edit > Plugins** from the main menu. Search for "nDisplay", and check the **Enabled** checkbox.
    
2.  Enable nDisplay for your Project.  
    Choose **Edit > Project Settings** from the main menu, and find the **Plugins > nDisplay** section. Check the **Enabled** checkbox.
    
3.  Restart the Unreal Editor and reopen your Project.
    
4.  Drag and drop the previously-generated config file (.cfg or .ndisplay) into your **Content Browser**. It will be automatically converted to a **UAsset**. Alternatively, add a new **nDisplay Config** UAsset, found in the **nDisplay** media category in the Content Browser
    
5.  Continue on with the rest of the setup instructions in the [Quick Start Guide](/documentation/en-us/unreal-engine/ndisplay-quick-start-for-unreal-engine).