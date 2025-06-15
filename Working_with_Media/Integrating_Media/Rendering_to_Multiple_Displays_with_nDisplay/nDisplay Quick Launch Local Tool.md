# nDisplay Quick Launch Local Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-quick-launch-local-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-quick-launch-local-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:20

---

When you're creating virtual production projects in **Unreal Engine**, it can be helpful to test the project's appearance and functionality on your local hardware, before launching the project on a virtual production stage. The **nDisplay Quick Launch Local Tool** is designed to quickly and efficiently launch your virtual production project without requiring a full virtual production stage environment. This gives you a safe, manageable environment for testing and debugging.

This document provides an example workflow of how you can use the Quick Start Local Tool to launch virtual production projects in Unreal Engine.

#### Prerequisites

-   Enable, both the **nDisplay** and **nDisplay Launch** [Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). In the **Menu Bar**, navigate to **Edit** \> **Plugins** \> **Virtual Production**, and locate the **nDisplay** and **nDisplay Launch** plugins. Alternatively, you can use the **Search Bar**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a996bcf0-6ea8-4fb4-ba94-a073ca43e791/ndisplayplugin.png) ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9584565-06ee-4008-bff8-6d3b66db7608/ndisplaylaunchplugin.png)

-   Enable both plugins and restart the editor.
    
-   You must have a functional virtual production project containing at least a Config File with a working Cluster Display node. If you do not have one, you can use the [nDisplay Template](/documentation/en-us/unreal-engine/ndisplay-template-in-unreal-engine) project.
    

## Set the nDisplay Launch Assets

After installing the nDisplay and nDisplay Quick Launch plugins, you can now select the nDisplay Config assets, and cluster nodes you will use to launch and render the virtual production project.

To set the nDisplay Launch Assets:

1.  In the **Quick Launch Options Menu**, ensure your **Config File** is toggled under **Configuration**, and that the correct **Cluster Node** is selected under **Nodes** > **Select nDisplay Nodes**.For this workflow example, the Config File and Cluster Node are using the default asset names, and are `nDisplayConfig` and `Node_0` respectively.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c9d1db1-284a-4718-9f4a-ef0ffdc419d1/confignode.png)

In multi-display instances, using multiple Cluster Nodes, you can toggle each node independently in the **Select nDisplay Nodes** menu.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b53eb842-b463-437c-ad1f-552d1702af6a/multidisplay.png)

Any selected display Nodes are rendered at their native resolution across your desktop's display. If the combination of nodes' resolution is greater than the extent of your monitors' resolution, some nodes may be rendered beyond your monitors' field of view.

1.  After ensuring the correct Config File and Nodes are selected, **Save** your project. You can now launch nDisplay using the **nDisplay Launch** button in the toolbar.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c9a85f3-3e9f-4aa1-89fc-9c7eb96fca1d/confignode.png)

To improve your project's render performance, you can enable the **Close Editor on Launch** option for the [Quick Launch Options Menu](/documentation/en-us/unreal-engine/ndisplay-quick-launch-local-tool-in-unreal-engine#quicklaunchoptionsmenu).

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ad01bc1-4a92-41fb-b059-49279d56f1dc/dots.png)

Running a single nDisplay node saves computational resources when you are testing a project.

When working with multi-user projects, the Multi-User server launches automatically when you launch a project with the nDisplay launch tool. You can also track your projects data and performance, for debugging purposes by toggling **Enable Unreal Insights** in the nDisplay Quick Launch Options Menu.For more information about setting up a Multi-User project, refer to the [Virtual Camera Multi-User Quick-Start Guide](/documentation/en-us/unreal-engine/virtual-camera-multi-user-quick-start-guide-in-unreal-engine) documentation. For a technical reference guide on how multi-user server sessions are created, reference to the [nDisplay Multi-User Technical Reference](/documentation/en-us/unreal-engine/ndisplay-multi-user-technical-reference-in-unreal-engine).

## Settings and Options

These are the settings for the nDisplay Launch plugin.

### Quick Launch Options Menu

Using the drop down menu of the **nDisplay Launch** button, you can manage and set the Config File, Cluster Nodes, and nDisplay Quick Launch behaviors.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fec170f-2ef0-43ad-a360-94ecc1fc57b8/dots.png)

| Setting | Description |
| --- | --- |
| **Configuration** | Select which **Config File** to use when launching the nDisplay render. |
| **Connect to Multi-User** | 
When enabled, the nDisplay Quick Launch Tool attempts to connect to a [Multi-User editing environment](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine). If a Multi-User session is not set in the nDisplay Launch Project Settings, or Unreal Engine cannot connect to the server, the nDisplay Quick Launch tool will start the Multi-User server.

To manually set a session name, see the **Multi-User** property section in the **Advanced Settings**.



 |
| **Enable Unreal Insights** | 

When enabled, **Unreal Insights** debugging tools reads and reports on the nDisplay render.

The [Unreal Insight plugin](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) must be installed to use this feature.

To set the file directory and the behaviors of the Unreal Insights report, use the **Unreal Insights** property section in the Advanced Settings.



 |
| **Close Editor on Launch** | 

When enabled, the Unreal Editor closes when launching the nDisplay render. Closing the editor can reduce your computer's computational workload and increase the render's performance.

We recommend that you launch nDisplay with the fewest possible render nodes to reduce the computational load for a single machine.



 |
| **Advanced Settings** | You can access the nDisplay Launch tools [Advanced Settings](/documentation/en-us/unreal-engine/ndisplay-quick-launch-local-tool-in-unreal-engine#projectsettings). You can also access these settings by navigating in the **Menu Bar** to **Edit** > **Project Settings** and selecting the **nDisplay Settings** under the **Plugins** section. |

### Project Settings

These are the nDisplay Launch plugins settings. You can access these settings using the **Advanced Settings** menu option from the [Quick Launch Options Menu](/documentation/en-us/unreal-engine/ndisplay-quick-launch-local-tool-in-unreal-engine#quicklaunchoptionsmenu). Alternatively you can access the nDisplay Launch settings in the **Menu Bar** by navigating to **Edit > Project Settings** and selecting the **nDisplay Launch** settings under the **Plugins** section.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6637620-5371-4218-879a-ba1ba41ace47/settings.png)

| Setting | Description |
| --- | --- |
| **Close Editor on Launch** | When enabled, the Unreal Engine **Editor** will close when launching the nDisplay render. Closing the editor can reduce your computer's computational workload, and increase the render's performance. |
| **Connect to Multi User** | 
When enabled, the nDisplay Quick Launch Tool will attempt to connect to a [multi-user editing environment](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).

To set a specific Multi-User session name to connect to, see the **Explicit Session Name** property.



 |
| **Explicit Session Name** | 

Give your session a name to be used when connecting to a [Multi-User editing environment](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).

If this field is left empty, the Editor automatically generates a name.



 |
| **Enable Unreal Insights** | 

When enabled, **Unreal Insights** debugging tools reads and reports on the nDisplay render.

The [Unreal Insight plugin](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) must be installed to use this feature.

Use the **Unreal Insights** property section in the Advanced Settings to set the file directory and the behaviors of the Unreal Insights report.



 |
| **Enable Stat Named Events** | Enables the Unreal Insight [Stat Named Events](/documentation/en-us/unreal-engine/unreal-insights-reference-in-unreal-engine-5#controllingunrealinsights) feature. |
| **Explicit Trace File Save Directory** | 

Set a directory path to store the **Unreal Insights Trace Files**. If empty, Unreal Insights automatically stores the files locally.

If you want to store the Trace Files locally, the Unreal Insights plugin must be installed and launched.

In order to specify a socket to connect to, use Command Line Arguments.



 |
| **Console Variables Preset** | 

Set a **Console Variables Asset** to apply by default during an nDisplay launch.

All available commands and variables contained within the set Console Variables Asset will be executed before any variables and commands under the **Additional Console Variables** and **Additional Console Commands** properties.

For more information on managing and editing Console Variables, refer to the [Console Variable Editor](/documentation/en-us/unreal-engine/console-variables-editor) documentation.



 |
| **Additional Console Variables** | 

Specify and set additional console variables. These variables are defined and set after any present in the **Console Variable Asset** property.

Setting additional console variables is useful for overriding variables in your defined Console Variables Asset.



 |
| **Additional Console Commands** | 

Specify and set additional console commands. These commands are executed after any present in the **Console Variable Asset** property.

Setting additional console commands is useful for overriding variables in your defined Console Variables Asset.



 |
| **Command Line Arguments** | 

Set a list of Switchboard command line arguments, that the nDisplay Launch tool will execute, mimicking the Switchboard application's functionality, on a single workstation.

Do not include an en-dash ("-") in any commands.The editor automatically adds a dash when calling the command.

If your workstation possesses more than 1 GPU, you can use the following command to run the nDisplay Launch tool using multiple GPUs to render your project.

`MaxGPUCount=2`

If you do not specify this manually, nDisplay will not recognize the second GPU, and operate as a 1 GPU workstation.



 |
| **Log File Name** | 

Set the name of the log file Unreal Insights writes logs about the launched node in.

If you do not specify a name, the resulting log file will be called the same name as the node.



 |
| **Logging** | 

Set which logs should be recorded in the generated log file and the style of verbosity for recording logs.

You can add a new log using (**+**) **Add**.

Select the log **Category** by typing the log's type in the provided field.

Select the verbosity from the associated **Verbosity Level** drop down menu.



 |