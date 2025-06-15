# nDisplay Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:38:21

---

This page describes how to get up and running with nDisplay for the first time.

**Prerequisites:**

-   Make sure you have your physical equipment — screens, projectors, and so on — set up and working correctly.
    
-   Make sure that the Windows account you intend to use on the primary computer has administrative rights on *all* computers you intend to use in the nDisplay network.
    
-   Make sure that all computers you want to use in the nDisplay network can receive TCP/IP communications over ports 41000, 41001, 41002, and 41003. (You can use different ports instead; see [Changing nDisplay Communication Ports](/documentation/en-us/unreal-engine/changing-ndisplay-communication-ports-in-unreal-engine).)
    

## Step 1 - Set Up Your Project for nDisplay

The easiest way to get a Project setup to use nDisplay is to create it from the [nDisplay Template Project](/documentation/en-us/unreal-engine/ndisplay-template-in-unreal-engine). You'll find this Template in the Film, Television, and Live Events category in the New Project window.

Click image for full view.

This Template automatically enables the nDisplay and Switchboard plugins, configures some helpful additional settings, and includes some sample configuration assets.

This guide uses the **NDC\_Basic** nDisplay Config Asset to show how to launch nDisplay with one Cluster Node and one Viewport.

If you have an existing Project that you want to use with nDisplay, you can do the same configuration by hand. See [Adding nDisplay to an Existing Project](/documentation/en-us/unreal-engine/adding-ndisplay-to-an-existing-project-in-unreal-engine).

## Step 2 - Set up the Configuration File

The template project already includes an nDisplay Root Actor for the NDC\_Basic configuration. Select the actor and move it around the scene to preview it in the nDisplay cluster configuration. This real-time config preview is meant to be a replica of your nDisplay setup that you can preview in any level or project.

To preview other nDisplay Configurations, you can drag the nDisplay Config asset from the **Content Browser** into the **Viewport**.

## Step 3 - Package and Deploy

A core concept with nDisplay is that it does not run in the Editor. Instead nDisplay runs as a separate instance of Unreal Engine launched with [Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine). Switchboard and its companion application SwitchboardListener also run outside of Unreal Engine.

These examples do not use the loopback address 127.0.0.1, because its use cannot be combined with other non-loopback addresses, such as those belonging to other machines, in the same Switchboard configuration. Loopback may be used, but only in a simple configuration where it is the only address used, and every device is local to the machine running Switchboard. Mixing loopback and non-loopback addresses in a multi-machine setup leads to connectivity errors.

Follow these steps to launch your nDisplay cluster.

1.  In the **Toolbar**, click the dropdown arrow next to **Switchboard** and choose **Launch SwitchboardListener**. SwitchboardListener launches and immediately minimizes itself. SwitchboardListener needs to be launched on every computer that will be in the nDisplay cluster.
    
    ![Switchboard menu options in the toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60d125b0-023c-47df-88ef-a181a22a4013/02-lauch-swithchboard-listener_ue5.png)
    
    If you don't see the Switchboard options in the Toolbar, click the double right arrow to see more options.
    
    ![Switchboard menu options under the toolbar arrow](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8ad8834-0178-43f6-b9fb-2ff01cee4a06/02-launch-1_ue5.png)
2.  In the **Toolbar**, click the **Switchboard** button to launch the Switchboard application on your computer.
    
    ![Launch Switchboard button in the toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1666bbc5-292d-4dbf-a393-8fea8f89cd9f/03-swithchboard_ue5.png)
    
    When launching Switchboard for the first time, a command prompt window may appear, installing required dependencies before the Switchboard window opens.
    
3.  When Switchboard opens, the **Add new Switchboard Configuration** window appears. In the window, ensure the **Config Path**, **uProject**, and **Engine Dir** fields are correct, and click **OK** to open a blank configuration.
    
    ![Add new Switchboard Configuration window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f906570-92d5-4b02-9258-8ed320963021/04-swithchboard-configuration_ue5.png)
    
    Switchboard Configurations are a collection of settings for Switchboard and are saved to disk. They can be reloaded and switched out at any time. Typically, you will want to create a Switchboard Configuration per project.
    
4.  In Switchboard, click **Add Device** in the top left and choose **nDisplay** to open the **Add nDisplay Device** window.
    
    ![Add Device and choose nDisplay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56c117bc-3386-4c84-9f83-5c9a2998616a/05-add-device_ue5.png)
5.  Browse and select the **NDC\_Basic.uasset** configuration file in your project, and click **OK** to add all the nDisplay devices described in the configuration asset to Switchboard.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e186f297-9a88-4b6a-b6d7-1ee3095828ce/06-add-ndisplay-browse_ue5.png)
6.  Since only one nDisplay Cluster Node is specified in the configuration asset, only one nDisplay device appears in Switchboard under **nDisplay Devices**. Set the IP address to your computer's external IP address. You must use your computer's external IP address instead of the default localhost IP address 127.0.0.1, if you want to add more computers to your nDisplay cluster later, because you cannot use both loopback and non-loopback addresses in a multi-machine setup. These steps use the IP address 192.0.2.0 as an example.
    
    ![Switchboard showing one nDisplay Cluster Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1520277-e1af-44c9-b533-63940dcb925f/07-ndisplay-devices_ue5.png)
7.  Click the **Connect to listener** button to connect to the SwitchboardListener on the computer.
    
    ![Connect to SwitchboardListener](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a9d5310-e2ee-4f1e-9284-c2669c8d1df8/08-connect-to-listener_ue5.png)
8.  Click the **Start Unreal** button launch Unreal with the nDisplay renderer on the computer.
    
    ![Click arrow button to launch the nDisplay instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52538be6-a728-4294-af60-f59392924f7f/09-start-unreal-button_ue5.png)
9.  When the nDisplay instance launches, all other windows on the computer minimize and the nDisplay viewport appears on the desktop.
    

The default Switchboard launch mechanism described above uses -game mode. You can also work with cooked builds. This will require you to specify the file path of the cooked executable instead of the uproject file.

When working with cooked builds, you must update Switchboard settings to include the path of the .exe file and empty the UProject path. This tells Switchboard to ignore project location and use the cooked .exe file instead.

![Path to a cooked build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9013b86-b577-4aa7-831e-8c5f5a378a76/10-ndisplay_settings.png)

## Step 4 - On Your Own

This guide covered setting up and launching one nDisplay cluster node on one computer with Switchboard.

-   Use the other nDisplay configurations available in the [nDisplay Template](/documentation/en-us/unreal-engine/ndisplay-template-in-unreal-engine) to see how to set up nDisplay on multiple machines. Ensure you have SwitchboardListener running on every machine, to connect to them from Switchboard.
-   To create a seamless view across multiple displays, see [Synchronization in nDisplay](/documentation/en-us/unreal-engine/synchronization-in-ndisplay-in-unreal-engine#gettingsynctowork) for information on setting up display sync and genlock on the machines.
-   To use a tracking system with your nDisplay cluster, you must add a LiveLinkComponent to your Cluster configuration. See [Live Link](/documentation/en-us/unreal-engine/live-link-in-unreal-engine) for more.