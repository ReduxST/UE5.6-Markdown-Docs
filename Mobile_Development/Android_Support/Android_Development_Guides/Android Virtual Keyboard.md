# Android Virtual Keyboard

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-android-virtual-keyboard-in-unreal-engine-projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-android-virtual-keyboard-in-unreal-engine-projects)  
**Processed:** 2025-06-14 16:49:18

---

All **Unreal Engine** (UE) Android-based projects offer support for using either the standard pop up dialog input box or the operating system's virtual keyboard. The following document shows how to set up and call either virtual keyboard in your UE projects.

![New Keyboard Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8ded930-32ad-416a-b1e9-2ebf5aa9cab3/virtual-keyboard-new.png)

![Old Keyboard Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f5efb85-f44b-4f8f-b2fe-3ec7e3b61781/virtual-keyboard-old.png)

## Steps

To enable the Virtual Keyboard in your project, you will need to do the following:

1.  From the **Main Menu** go to **Edit** and then click on the **Project Settings** option.
    
    ![Open Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31a8ac02-d89f-4079-9290-e9a1438c5175/ue5_1-01-open-project-settings.png "Open Project Settings")
2.  In the **Project Settings** menu go to **Platforms > Android** and under the **APK Packaging** section look for and click on the check mark box next to the **Enable improved virtual keyboard** option to enable it.
    
    Click for full image.
    
3.  Right-click in the **Content Browser** and then go to **User Interface > Widget Blueprint** option, giving this new Blueprint a name of **InputText**.
    
    Click for full image.
    
4.  Double - click on the **Input Text** UMG widget to open it up and from the **Palette** drag a **TextBox** into the UMG graph.
    
    Click for full image.
    
5.  Position the **TextBox** so that it is in the middle of the **Canvas** panel and then press the **Compile** and **Save** buttons.
    
    Click for full image.
    
    Keep in mind that your application is responsible for ensuring input elements are visible and not obscured behind the virtual keyboard. You can use the supplied **OnVirtualKeyboardShown** and **OnVirtualKeyboardHidden** event handlers to make sure that UI elements do not obscure the virtual keyboard.
    
6.  Open up the **Level Blueprint** and add the following nodes to the **Event Graph**.
    
    -   **Event Begin Play**
    -   **Create Widget**
    -   **Add to Viewport**
        
        Click for full image.
        
7.  Connect the **Event Begin Play** node to the **Create Widget** node and then connect the **Create Widget** node to the **Add Viewport** node. When completed your **Level Blueprint** should look like the following image.
    
    Click for full image.
    
8.  Next, in the **Create Widget Blueprint** node, in the **Class** input, add the **InputText** Widget Blueprint that was created earlier.
    
    Click for full image.
    
9.  Save the level, giving it a name of **AndroidVirtualKeyboard** then open up your **Project Settings** and go to **Maps & Modes**. In the **Default Maps** input the **AndroidVirtualKeyboard** map into the **Editor Startup Map** and the **Game Default Map**.
    
    Click for full image.
    
      
    
10.  Click on the **Platforms** button small and from the displayed list, select the Android device you want to deploy your UE project to.
    

Click for full image.

## End Result

Once your project launches on your Android device, press on the text input box and when you do, you should now be able to input the text you want using the Android system keyboard like in the following video.

You can also disable the virtual keyboard using the **Android.NewKeyboard** console variable followed by one of the following numbers. Doing this is particularly useful when the user is using a language requiring a different IME (Input Method Editor).

| Command Name | Input | Description |
| --- | --- | --- |
| **Android.NewKeyboard** | 0 | Uses the check mark box setting that was set in the UE editor. |
| **Android.NewKeyboard** | 1 | Forces the new keyboard to be used. |
| **Android.NewKeyboard** | 2 | Forces the dialog to be used. |