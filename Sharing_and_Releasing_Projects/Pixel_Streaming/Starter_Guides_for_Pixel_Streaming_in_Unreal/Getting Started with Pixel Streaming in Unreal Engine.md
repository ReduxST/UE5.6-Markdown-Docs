# Getting Started with Pixel Streaming in Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/getting-started-with-pixel-streaming-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/getting-started-with-pixel-streaming-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:56

---

Follow the steps below to stream the rendered output from your Unreal Engine project over your local network to browsers and mobile devices.

The images for the steps on this page illustrate the procedure using a project built from the **Third-Person Blueprint** template. However, the same steps should work for any Unreal Engine project.

## Prerequisites

-   **Check your OS and hardware:** The Pixel Streaming plugin can only encode video on computers running Windows, Linux, or Mac operating systems, with certain specific types of GPU hardware. For details, see the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference).
-   **Open network ports:** Make sure you have the following network ports open for communication on your local network: 80, 8888. If you need to change these defaults, see the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference).
-   **Stop other web servers:** If your computer is running any other Web servers, stop them for now.
-   **IP addresses:** You'll need to know the IP address of your computer if you intend to test Pixel Streaming over the Internet.  
    It's a good idea to get started with Pixel Streaming within a LAN or VPN first, which means you can use `localhost` or `127.0.0.1` as your Pixel Streaming IP address. If you are trying to connect from a machine on a different network, you'll likely need to configure your signalling server to use a STUN / TURN server. See the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference) for details on how to configure your signalling server with `peerConnectionOptions` that specify a STUN / TURN server.

## 1 - Prepare Your Unreal Engine Application

In this step, you will create a standalone executable file for your Project.

The Pixel Streaming Plugin only works when you run your Project as a packaged application, or when you launch it from the Unreal Editor using the **Standalone Game** option.

The procedure below shows how to set this up for both scenarios.

1.  Open your Project in the Unreal Editor.
2.  From the main menu in the Unreal Editor, select **Edit > Plugins**.
3.  Under the **Graphics** category, find the **Pixel Streaming** or **Pixel Streaming 2** Plugin and check its **Enabled** box.
    
    ![Enable the Pixel Streaming plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d70c7352-a07a-458b-8184-d85c4b81453e/pixelstreaming-gs-prepare-enable.png "Enable the Pixel Streaming plugin")
4.  Click **Restart Now** to restart your Project and apply the change.
    
    ![Restart now](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0f0afee-3bf5-4988-b08c-6987ae6b25a2/pixelstreaming-gs-prepare-restart.png "Restart now")
5.  Back in the Unreal Editor, choose **Edit > Project Settings** from the main menu.
    
6.  If your Project involves a character, and you want to enable input from touch devices such as phones and tablets to move that character around the Level, you may want to show the on-screen touch controllers.  
    Under the **Engine > Input category**, find and enable the **Always Show Touch Interface** setting.
    
    ![Always Show Touch Interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a417f396-c851-43c0-b581-6df8fde08193/pixelstreaming-gs-prepare-showtouch.png "Always Show Touch Interface")

This is optional, and not required for all Projects. However, for Projects like the Third-Person Template, this makes sure that users with touch devices can control the streamed application (as long as the Project's Player Controller supports touch input).

1.  From the main menu, choose **Edit > Editor Preferences...**
    
2.  Under the **Level Editor > Play** category, find the **Additional Launch Parameters** setting, and set its value to `-PixelStreamingURL=ws://127.0.0.1:8888`.
    
    ![Additional Launch Parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1dddb12-7d34-4db4-ad21-bf3b5a6bfd4d/pixelstreaming-gs-prepare-audiomixer.png "Additional Launch Parameters")
3.  Package your Project for Windows. From the main menu in the Unreal Editor, choose **Files > Package Project > Windows (64-bit)**.
    
    ![Package for Windows 64-bit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99903366-44cc-4b2f-9df0-3e5a4f3c4c82/pixelstreaming-gs-prepare-package.png "Package for Windows 64-bit")
4.  Browse to the folder on your computer where you want the Unreal Editor to place the packaged version of your Project, and click **Select Folder**.
    

![Select a folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41a62878-ce13-42db-b45a-0c7debccea4f/pixelstreaming-gs-prepare-selectfolder.png "Select a folder")

1.  The Unreal Editor begins the packaging process.

![Packaging progress indicator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6610a3e4-e4b2-40f5-8ac6-cf7c8fcacb6e/multiuserviewer-packagestatus.png "Packaging progress indicator")

1.  When the packaging process is finished, go to the folder that you selected in step 10 above. You'll find a folder called `Windows` with contents similar to the following:

![Packaged output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bb0884b-892b-4585-b75c-04a8b28af474/pixelstreaming-gs-package.png "Packaged output")

1.  Every time you start your packaged application, you need to pass it the same command-line flags set in step 8 above. One way to do this is to set up a shortcut: 1. Press **Alt** and drag your *.exe* file to create a new shortcut in the same folder (or anywhere else you like on your computer).
    
    ![Create a shortcut](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b12ff0ec-fd87-45d1-aca9-9a8207b3707b/pixelstreaming-gs-prepare-shortcut.png "Create a shortcut")

2\. Right-click the shortcut and choose **Properties** from the context menu.

![Shortcut properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c6e3f5e-4b50-495c-90ac-eba914d24633/pixelstreaming-gs-prepare-shortcutprops.png "Shortcut properties")

3\. On the **Shortcut** tab of the **Shortcut Properties** window, append the text `-PixelStreamingURL=ws://127.0.0.1:8888` at the end of the **Target** field, and click **OK**.

![Command line parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6de6643f-9861-437b-8b94-a35286c5b54f/pixelstreaming-gs-shortcut-target-424.png "Command line parameters")

Once you've got the Pixel Streaming system up and running, you may want to add the `-RenderOffScreen` command-line parameter. If your Unreal Engine application window ever gets accidentally minimized, the Pixel Streaming input stream may stop working. `-RenderOffScreen` avoids this possibility by running the application in a headless mode without any visible window.

### End Result

You now have a packaged, standalone Unreal Engine application that has the Pixel Streaming plugin enabled, ready to stream its rendered frames and audio.

## 2 - Get the Pixel Streaming Servers

Recent changes to Pixel Streaming have moved the frontend and web server elements of Pixel Streaming to an external repository. We refer to this as the Pixel Streaming infrastructure.

There are a few ways to access the Pixel Streaming infrastructure.

1.  Directly access the github repository as found here: [https://github.com/EpicGamesExt/PixelStreamingInfrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/)
2.  Use `git clone --branch UEX.Y https://github.com/EpicGamesExt/PixelStreamingInfrastructure.git` in your preferred terminal (make sure you have git installed). Replace UEX.Y with your desired branch, such as 5.5.
3.  Navigate to `\Engine\Plugins\Media\PixelStreaming\Resources\WebServers` and run the `get_ps_servers` command (make sure to use the `.bat` script for Windows and `.sh` script for Linux or Mac accordingly). This will automatically pull the relevant branch of the Pixel Streaming infrastructure into that folder.

For more information about the Pixel Streaming frontend and web server changes, see [Pixel Streaming Infrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure)

## 3 - Start the Servers

In this step, you will start the web services that will help to establish peer-to-peer connections between your Unreal Engine application and clients' browsers. If you have not done the previous step, you will not have access to these servers.

The following steps assume you are using Windows. However, Linux and Mac both use the same process except that you run the scripts in the `SignallingWebServer\platform_scripts\bash` folder instead.

1.  In the location you pulled the Pixel Streaming Infrastructure, find the location of the Signalling Server under the folder `SignallingWebServer`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84f2d85d-3a04-4f0a-8fdb-50ad5ca9e0fc/sslocal.jpg)
2.  To prepare for the Signalling Server, start by opening PowerShell as Administrator and running `SignallingWebServer\platform_scripts\cmd\setup.bat`. This will install all the required dependencies.
    
3.  Start the Signalling Server by running `SignallingWebServer\platform_scripts\cmd\start_with_stun.bat`. When the server has started and is ready to accept connections, you'll see the following lines in the console window:
    
    ```
            `WebSocket listening to Streamer connections on :8888         WebSocket listening to Players connections on :80         Http listening on *: 80`
    Copy full snippet
    ```
    WebSocket listening to Streamer connections on :8888 WebSocket listening to Players connections on :80 Http listening on \*: 80
4.  Now, start the Unreal Engine application from the shortcut that you created in the previous section. Or, if you prefer to launch your application from the command line, execute the following command:
    
    ```
            `MyPixelStreamingApplication.exe -PixelStreamingURL=ws://127.0.0.1:8888`
    Copy full snippet
    ```
    MyPixelStreamingApplication.exe -PixelStreamingURL=ws://127.0.0.1:8888

For convenience, when you package your Unreal Engine application, these servers are also copied to the folder that contains your packaged executable. You'll find them under the *Engine* sub-folder, at the same paths indicated above. You can launch the servers from there instead of launching them from your Unreal Engine installation folder.  
However, remember that if you need to modify any files in these folders, particularly the player page or configuration file for the Signalling and Web Server, you should modify them in the original location. If you modify them in your package folder, your changes may be overwritten the next time you package your application.

### End Result

When the Unreal Engine application connects to the Signalling and Web Server, you should see the following line of output in the console window opened by the Signalling and Web Server:

`Streamer connected`

This means that you now have the Unreal Engine application running with the Pixel Streaming plugin enabled, and the frontend Signalling and Web Server is ready to route connecting clients to the Unreal Engine application.

If necessary, you can stop and restart the Unreal Engine application and the Signalling and Web Server independently. As long as they're both running at the same time, they should be able to reconnect automatically.

At this point, you have everything you need set up and working on your computer. All that's left is to connect a browser.

## 4 - Connect!

In this step, you'll connect Web browsers running on multiple different devices to your Pixel Streaming broadcast.

1.  On the same computer running your Unreal Engine application, press alt-tab to switch the focus away from the Unreal Engine application, and start a supported Web browser (Google Chrome and Mozilla Firefox are safe choices).
    
2.  In the address bar, navigate to `http://127.0.0.1`. This IP address of the local machine, so the request should be served by the Signalling Server:
    
    ![Connect to the localhost](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1684eb3-c735-4954-a656-b2d1f5d500fe/pixelstreaming-gs-connect-127001.png "Connect to the localhost")
3.  Click the page to connect, then click again on the Play button to start the stream.
    
4.  You'll now be connected to your application, and you should see the rendered output streaming into the middle of the player Web page:
    
    ![Media streaming to localhost](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/974ff9cd-6310-4279-8648-26d4005130d4/pixelstreaming-gs-connect-streaming.png "Media streaming to localhost")
    
    The default player page is already set up to forward keyboard, mouse, and touchscreen input to the Unreal Engine, so you can control the application and navigate around exactly the way you would if you were controlling the app directly.
    
5.  Click the **Add (+)** button at the left of the window to expand some built-in options for controlling the stream. For a breakdown of the options available, please refer to the repository here: [https://github.com/EpicGamesExt/PixelStreamingInfrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure)
    
    To see how frontend controls are implemented, study the contents of [Frontend/](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/Frontend)
    
6.  Now, find other computers and/or mobile devices in your network. Repeat the same steps, but instead of using `http://127.0.0.1`, direct the browser to the IP address of the computer running the Unreal Engine application and the Signalling Server.
    
    ![Media streaming to remote host](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e88251c8-7969-4f99-945a-029b022e6db8/pixelstreaming-gs-connect-others.png "Media streaming to remote host")

### End Result

You now have one instance of Unreal Engine running on your computer, broadcasting a media stream to multiple devices over your local network. Each connected device sees the same view of the same Level, all rendered on the same original desktop PC.

By default, all connected devices share control over the Unreal Engine application, forwarding all keyboard, mouse, and touchscreen inputs.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/582aeee4-ee80-44b1-9dc2-ced93c782666/pixelstreaming-endresult-chrome.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5dc1e84-23b6-43bc-98d6-15b687fa3277/pixelstreaming-endresult-iossafari.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75805c2b-3e4c-42c3-84e3-91b894c029f7/pixelstreaming-endresult-gpixel.png) |
| Desktop | iPhone | Android |

## 5 - On Your Own

The steps above walk you through a relatively simple setup that uses a single server host and a default player page. With a little more effort, you can take the Pixel Streaming system much farther. For example:

-   You can completely redesign the player HTML page to meet the needs of your project. Control who can send input to the Unreal Engine application, and even create HTML5 UI elements on the page that emit custom gameplay events to the Unreal Engine.  
    For details, see [Customizing the Player Web Page](/documentation/en-us/unreal-engine/customizing-the-player-web-page-in-unreal-engine). For a working example, see the [Pixel Streaming Demo](/documentation/en-us/unreal-engine/pixel-streaming-sample-project-for-unreal-engine) available in the **Learn** tab of the Epic Games Launcher.
    
-   If you need to provide Pixel Streaming services over the open Internet, or across subnets, you will likely need to do some more advanced network configuration. Or, you may prefer to have each connecting client stream content from a separate instance of the Unreal Engine, or through a separate player page that offers different controls.  
    For details on topics like these, see the [Hosting and Networking Guide](/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine).
    
-   Each component of the Pixel Streaming system has a number of configuration properties that you can use to control encoding resolution, screen size, IP addresses and communication ports, and more.  
    For information on all these properties and how to set them, see the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference).
    
-   To check out new experimental features in Pixel Streaming, see the [Experimental Pixel Streaming Features](/documentation/en-us/unreal-engine/experimental-pixel-streaming-features) page.
    
-   The [Stream Tuning Guide](/documentation/en-us/unreal-engine/stream-tuning-guide) page can help provide extra control over your stream quality and settings.