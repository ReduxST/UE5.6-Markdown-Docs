# DMX Conflict Monitor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-data-conflict-monitoring-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-data-conflict-monitoring-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:58

---

The DMX Conflict Monitor checks for potential DMX data collisions on all enabled Universes and Patch ranges when sending DMX data from the engine to an external device. Conflicts can occur between the different DMX tools in Unreal Engine (such as Control Console, Pixel Mappers, and Blueprints) if they are writing DMX data to the same address.

To open the Conflict Monitor, click **DMX** > **Conflict Monitor** in the **Main Toolbar**.

![Conflict Monitor in the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3af7f954-9af6-4f23-80bf-dfc7ecc1bf69/open-monitor.png)

The Conflict Monitor opens as a dockable window. Click the **ellipsis (...)** to configure the options.

-   **Play/stop**: Start and stop the monitoring process.
-   **Options**
    -   **Auto Pause**: Pause when a conflict is detected.
    -   **Print to Log**: Print conflicts to the UE Output Log. Only available when Auto-Pause is enabled.
-   **Monitor**
    -   **Run when opened**: Monitoring automatically starts when opened.
    -   **Depth**: Controls how much detail is included in the log entry.

When the Conflict Monitor is running, the **Objects Sending DMX** section updates to show which assets are currently sending DMX. You can then open the asset or navigate to it in the **Content Browser**.

![The Objects Sending DMX section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57bcb3fe-207f-4576-aae9-32cac3953df7/objects-sending-dmx.png)

Conflict monitoring can be CPU intensive. You can check the current CPU usage in the top right of the Conflict Monitor.

![The CPU usage bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11c2adcf-9234-4168-bcad-b6f9c838e80a/cpu-usage.png)

If the Conflict Monitor detects a conflict, then the monitor logs information about the conflict, including the conflicting DMX tools and the affected ports.

![Conflict Monitor log with information about a conflict](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ea545e9-7fee-4434-9ed2-616177dda90e/conflict-log.png)

If the **Print To Log** option is selected, then the Conflict Monitor also sends the same information to the UE Output Log.

![UE Output log with Conflict Monitor information](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a5b1306-7402-4568-882e-f23fe5d2b23c/ue-log.png)