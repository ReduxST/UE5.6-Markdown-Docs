# Using Remote Session Plugin for iOS Development

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-remote-session-plugin-for-ios-development-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-remote-session-plugin-for-ios-development-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:50

---

The Remote Session Plugin is meant to replicate the inputs from an iOS device, connected on the same network as your PC, so you can test your game or app from the editor, or from a locally running packaged version of the game or app. The Unreal Remote 2 app works with the Remote Session Plugin to help you test your game or app.

## Getting the Unreal Remote 2 App

1.  Go to the App store on your iOS device. Search for **Unreal Remote 2**. Tap **Get** to download.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94f066f5-9d6a-49c0-b578-e2cdf05ba4ac/unrealremote_appstore.png)
2.  The **Unreal Remote 2** app downloads and installs on your device. The device should be connected to the same network as your PC.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6015b64e-e1e1-45d4-98e4-2c4965817117/unrealremote_installed.png)
3.  Start the application on the iOS device, and enter your PC's IP address. Then tap **Connect**.
    
    ![UnrealRemote_IPAddress.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39b1794a-c955-4f4a-b63d-9e2de242548f/unrealremote_ipaddress-opt.png)

## Enable Remote Session Plugin

1.  In the Unreal Editor, click **Edit > Plugins**. The **Plugins** panel displays.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9c09124-8f34-47da-951b-c824c85f44cd/editplugins.png)
2.  In the left navigation panel, scroll down to **Experimental**. Locate the **Remote Session Plugin**.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e00281b-bb04-4391-9137-54782b9f24cf/enableremotesessionplugin.png) You can also use the **Search** bar to locate the Plugin by typing in "remote".
    
    If you use the Search bar and type in "remote," you might see the Slate Remote Plugin in your search results. This is an older version of the plugin and should not be enabled--**only enable the Remote Session Plugin**.
    
3.  Check the box for **Enabled**. A warning message appears stating that you need to restart the Editor for the change to take effect.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2383ab09-a98d-4bf6-9db3-0b89ae6756ed/enableslateremoteplugin-2.png)
4.  Click **Restart Now** to restart the Editor.
    
5.  In the Unreal Editor, click the dropdown arrow on the **Play** button. This displays a menu of play state options. Select either **New Editor Window (PIE)** or **Standalone Game**. A new window opens.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bbfc81b-38e2-4106-9e5b-42b97a0c9e66/enableslateremoteplugin_step5.png)
6.  Make sure Unreal Engine Editor is the active window. The interaction from the Unreal Remote app on the iOS device will be received by the input manager. All Blueprint nodes (and corresponding C++ APIs) in the following categories will return usable values:
    
    -   Touch events
    -   Touch input
    -   Gesture events
    -   Motion events
    -   Motion values