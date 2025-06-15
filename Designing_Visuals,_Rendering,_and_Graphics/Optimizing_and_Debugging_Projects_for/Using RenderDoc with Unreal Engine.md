# Using RenderDoc with Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-renderdoc-with-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-renderdoc-with-unreal-engine)  
**Processed:** 2025-06-14 17:00:47

---

RenderDoc is a free standalone open-source graphics debugger that you can use to perform single-frame captures of an application, such as Unreal Engine. The capture is loaded into RenderDoc to inspect what is happening on the GPU through the events, API, and much more, in full detail.

## Install RenderDoc

RenderDoc is an open-source graphics debugger that is free, and available to download and install from [RenderDoc.org](https://renderdoc.org/).

The list of supported operating systems and APIs below reflect what RenderDoc currently supports, which may differ from what Unreal Engine supports. For the latest updates, see [RenderDoc's FAQ](https://renderdoc.org/docs/getting_started/faq.html?highlight=support#what-apis-does-renderdoc-support) page.

RenderDoc supports the following Operating Systems:

-   Windows 7, 10, and 11
-   Linux
-   Android
-   Nintendo Switch

RenderDoc supports the following APIs:

-   Vulkan
-   D3D11
-   D3D12
-   OpenGL 3.2+
-   OpenGL ES 2.0 — 3.2

## Enable RenderDoc in Your Project

The **RenderDoc** plugin is included with the engine and enabled by default. There are two ways you can run RenderDoc with your project: by command line argument, or a project setting.

When RenderDoc attaches on startup, you'll see the RenderDoc icon in the upper-right corner of the Level Viewport.

![RenderDoc Level Viewport Icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72f17f69-512a-41d9-8164-70463a6a5fa7/renderdoc-icon.png)

Follow the steps below to see how each is enabled.

### Enabling with Plugin Project Settings

In the Project Settings in **Plugins > RenderDoc** under **Advanced Settings**, enable **Auto attach on startup**. This method is ideal when you want to run RenderDoc on startup anytime the project loads.

![RenderDoc Plugin Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bb67d6c-f4b4-4728-8b0f-6fbc5cc3e176/enable-auto-attach-projectsettings.png)

### Enabling with Command Line

Enable command line arguments using an editor shortcut. In the **Shortcut** tab, add the following to the **Target** line: `-AttachRenderDoc`. This method is ideal when you only want to run RenderDoc some of the time.

![RenderDoc Project Shortcut Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/868b67e3-20c2-4efc-a61a-0cffb407a60b/attachrenderdoc-commandline.png)

## Performing a Frame Capture

The steps below describe at a high level how to perform a single-frame capture with your Unreal Engine project using the integrated RenderDoc plugin or directly from RenderDoc application.

Further details on functionality and use of RenderDoc can be found in [RenderDoc Documentation](https://renderdoc.org/docs).

### RenderDoc Plugin

The following steps are used to capture a frame using Unreal Engine's RenderDoc Plugin:

1.  Enable the RenderDoc plugin for your project.
2.  Open your project and scene where you want to perform a capture.
3.  Click the **RenderDoc Capture** button in the Level Viewport.
    
    Click image for full size.
    

### RenderDoc Application

The following are the high-level steps required to capture a frame using Unreal Engine with the standalone RenderDoc executable:

1.  Configure RenderDoc to launch your game or the UEEditor.exe with the appropriate command line arguments.
    
    Enable **Capture Child Processes** when launching with the UEEditor.exe.
    
2.  Launch the executable.
3.  Press the **F12** hotkey to perform a frame capture.

For full details on setting up RenderDoc, launching an application and performing a frame capture, see the [RenderDoc Getting Started Guide](https://renderdoc.org/docs/getting_started/quick_start.html).

## Project Settings

Use the Project Settings window to set additional RenderDoc Plugin settings. From the main menu, select **Edit** > **Project Settings** and then under the **Plugins** category, select **RenderDoc**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4be076d5-3436-401d-9d0c-f9b29c53968c/renderdoc_projectsettings.png)

| Property | Description |
| --- | --- |
| Frame Capture Settings |   |
| **Capture all activity** | When enabled, RenderDoc captures all activity in all viewports and Editor windows for the entire frame instead of only the current viewport. |
| **Capture all call stacks** | When enabled, RenderDoc captures call stacks for all API calls. |
| **Reference all resources** | 
When enabled, RenderDoc includes all rendering resources in the capture, even those that have not been used during the frame.

Enabling this property will significantly increase capture size.



 |
| **Save all initial states** | 

When enabled, RenderDoc always captures the initial state of all rendering resources, even if they are not likely to be used during the frame.

Enabling this property will significantly increase capture size.



 |
| Advanced Settings |   |
| **Show help on startup** | When enabled, a help window with RenderDoc is shown on Editor startup. |
| **Use the RenderDoc crash handler** | 

If enabled, the RenderDoc crash handler is used if a crash occurs.

This should only be used if you know the problem is with the RenderDoc application and would like to notify the RenderDoc developers.



 |
| **RenderDoc executable path** | 

Sets the path to the RenderDoc executable to use.

This should automatically fill in when with the correct path when RenderDoc is installed.



 |

## Additional Notes and Resources

-   See [RenderDoc Documentation](https://renderdoc.org/docs) for further reading on RenderDoc use and analysis of frame captures.
-   The RenderDoc Plugin was created and developed by Fredrik Lindh ("Temaran") for Unreal Engine. For additional information, see the RenderDoc [GitHub respository](https://github.com/Temaran/UE4RenderDocPlugin).