# Capture Data Asset

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/capture-data-asset](https://dev.epicgames.com/documentation/en-us/unreal-engine/capture-data-asset)  
**Processed:** 2025-06-14 16:12:11

---

The **Capture Data** asset is created by **Capture Manager** as part of the ingest process. It tracks the assorted set of data and metadata that is required when working with performance capture data. Some of that data is optional but commonly available (such as audio). 

A Capture Data asset can be input to the [MetaHuman Identity](https://dev.epicgames.com/documentation/en-us/metahuman/metahuman-identity-asset) and [MetaHuman Performance](https://dev.epicgames.com/documentation/en-us/metahuman/metahuman-performance-asset) asset.

Although the asset is typically created by an automated process, it can be created manually if required. While a Capture Data asset can be configured manually, be mindful of the fact that incompletely or incorrectly configured information will create unpredictable issues that might be difficult to troubleshoot.

[![Footage Capture Data](https://dev.epicgames.com/community/api/documentation/image/42bd6dd2-33b5-4f3a-8147-651f003a0d82?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/42bd6dd2-33b5-4f3a-8147-651f003a0d82?resizing_type=fit)

A **Capture Data** asset may reference one or more of the following other assets depending on the data it represents:

-   **Img Media Source** (for depth and/or RGB video)
    
-   **Sound Wave** (for audio tracks)
    
-   **Camera Calibration**
    

 It is important to not confuse the difference between the **Device Class** and the **Device Model** for iOS devices. The **Device Class** inside a **Capture Data** asset is a fixed choice from limited options, and it’s the commonly known name of the model from a consumer point of view. The **Device Model** is a less visible versioning that **doesn’t necessarily line up** with the public-facing model number. This is usually ahead of the consumer branding. For example, an iPhone 12 device is likely to have a model number of iPhone 13,N.

## Timecode Information

The Timecode for the Image and Depth Sequences can be viewed and set via the **ImgMediaSource** asset editor.

[![Timecode](https://dev.epicgames.com/community/api/documentation/image/515c6634-0f6e-45e1-8f40-ca522a459e6a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/515c6634-0f6e-45e1-8f40-ca522a459e6a?resizing_type=fit)

The Timecode and Timecode Frame Rate for SoundWave assets can be viewed and set selecting **Scripted Asset Actions > Set Timecode Info**.

[![Scripted Asset Actions](https://dev.epicgames.com/community/api/documentation/image/531c8a32-e28a-4942-abd3-5b1f6245714f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/531c8a32-e28a-4942-abd3-5b1f6245714f?resizing_type=fit)

Enter the desired Timecode and Timecode Frame Rate values and click **OK** to set the values.

[![Set Timecode Info](https://dev.epicgames.com/community/api/documentation/image/c71dd437-a0a6-4964-b036-aa0cc4c54f9f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c71dd437-a0a6-4964-b036-aa0cc4c54f9f?resizing_type=fit)