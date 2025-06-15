# Capture Manager Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/capture-manager-quick-start](https://dev.epicgames.com/documentation/en-us/unreal-engine/capture-manager-quick-start)  
**Processed:** 2025-06-14 16:12:16

---

This page provides the basic steps to get started using **Capture Manager** and ingest a take. It assumes you are already familiar with [Live Link Hub](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-hub-in-unreal-engine), and have captured footage ready to ingest.

## Enable Capture Manager Editor Plugin

The **Capture Manager Editor** plugin is required to use Capture Manager in **Live Link Hub**. It is shipped with **Unreal Engine** 5.6 or later.

Follow these steps to enable the Capture Manager Editor plugin in your Unreal Engine project:

1.  Create or open an Unreal Engine project.
    
2.  From the Unreal Editor menu bar, navigate to **Edit > Plugins**. This will open the **Plugins** window. 
    
3.  In this window, search for “Capture Manager Editor.”
    
4.  Enable the **Capture Manager Editor** plugin.
    

For more information about how to enable plugins in your project, refer to the [Working with Plugins](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) page in the Unreal Engine documentation.

When enabling plugins, a warning message may appear stating, "You must restart Unreal Editor for your changes to take effect." If you have enabled all the plugins you want and you are ready to restart the Unreal Editor, click **Restart Now**.

## Capture Manager Workflow

The Capture Manager workflow to ingest a take consists of the following steps:

1.  To open **Capture Manager**, select it from the **Layouts** drop down.
    
    [![UE Capture Manager](https://dev.epicgames.com/community/api/documentation/image/a74f96a2-2939-449a-9c57-326228fd88ed?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a74f96a2-2939-449a-9c57-326228fd88ed?resizing_type=fit)
    
2.  Click **Add Device** and select the option that matches the data to be ingested.
    
    [![UE Capture Manager Add Device](https://dev.epicgames.com/community/api/documentation/image/301b7d29-3b11-4c6d-bf3a-2ce02ccf7ce4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/301b7d29-3b11-4c6d-bf3a-2ce02ccf7ce4?resizing_type=fit)
    
    -   **Mono Video**: Ingest individual video files as mono takes. If the video contains an audio track it will also be extracted during ingest.
        
    -   **Live Link Face**: Ingest takes directly from a connected iOS device running the [Live Link Face App](https://dev.epicgames.com/documentation/en-us/metahuman/live-link-face-app).
        
    -   **Take Archive**: Ingest an arbitrary take of video, audio, depth, and calibration data identified using a take metadata file (`.cptake`).
        
    -   **Stereo Video**: Ingest pairs of video files as stereo takes. An audio file (`.wav`) may also be provided alongside the video.
        
    
    The **Take Archive** device is backwards compatible with takes created for use with Capture Manager and **MetaHuman Animator** in Unreal Engine 5.5 and earlier.
    
3.  Select the **Pipeline** to define the stages that are executed during ingest. The supported pipelines are:
    
    -   **Ingest**: Download (from Live Link Face — if applicable), convert (to formats required for Unreal Engine), and create assets (in Unreal Engine).
        
    -   **Download**: Download only (from Live Link Face — if applicable).
        
4.  Select one or more takes in the **Take Browser** and click **Add to Queue** to add them to the ingest queue. 
    
    [![Capture Manager Add To Queue](https://dev.epicgames.com/community/api/documentation/image/8dc5f5f7-c7ee-4012-9ce0-0de0fe4179c3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8dc5f5f7-c7ee-4012-9ce0-0de0fe4179c3?resizing_type=fit)
    
5.  Ingest options can be edited in the **Job Details** panel.
    
    [![Capture Manger Job List](https://dev.epicgames.com/community/api/documentation/image/b471ab67-1e4c-4e9e-ad6a-2d5cb81f24ef?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b471ab67-1e4c-4e9e-ad6a-2d5cb81f24ef?resizing_type=fit)
    
6.  With takes in the **Jobs List** ready to ingest, click on **Start** to begin processing.
    
    |  |  |
    | --- | --- |
    | 
    [![Job List Start](https://dev.epicgames.com/community/api/documentation/image/29c4bac2-2a6b-46e3-8c59-04d4d547d6dc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/29c4bac2-2a6b-46e3-8c59-04d4d547d6dc?resizing_type=fit)
    
    
    
     | 
    
    [![Job List In Progress](https://dev.epicgames.com/community/api/documentation/image/32190356-901a-4535-bb92-40aea6927f7c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/32190356-901a-4535-bb92-40aea6927f7c?resizing_type=fit)
    
    
    
     |
    

On successful ingest of the selected takes, assets will be created and visible in the **Content Browser** for the current project.