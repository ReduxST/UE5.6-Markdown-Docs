# SteamVR Profiling & Performance

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/steamvr-profiling-and-performance-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/steamvr-profiling-and-performance-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:36

---

On this page, you will find information about how to profile the performance of your SteamVR projects in Unreal Engine .

## SteamVR Frame Timing

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6afb78fb-d3c0-4731-9d89-01c1c478ddbb/steamvr_propref_00.png)

The SteamVR Frame Timing tool can be used to help track down what is causing your UE project to perform poorly. Whether in the editor or packaged builds, the SteamVR Frame Timing tool can help verify the actual CPU and GPU timings while accounting for things like throttling being done by the application. For a more in-depth look at everything you can do with the SteamVR Frame Timing tool, check out the official documentation on the [SteamVR Frame Timing Tool](https://developer.valvesoftware.com/wiki/SteamVR/Frame_Timing).

To display the SteamVR **Frame Timing** tool, you will need to do the following.

1.  Right-click on the SteamVR tools and from the displayed menu, select the **Settings** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/815f0237-8483-4568-8f4a-4361bceee4fd/steamvr_propref_01.png)
2.  Then from the Settings menu, click on the **Display Frame Timing** button to display the Frame Timing tool.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2451afa4-db74-4f84-98ce-8bdda31070a4/steamvr_propref_02.png)
3.  Once the Frame Timing tool is open, you can then launch your UE4 project and check to see what is happening in the Frame Timing tool.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62b03706-6679-4176-90cc-875e02418b21/steamvr_propref_00.png)

## Saving SteamVR Frame Timing

You can save the information that is generated from the **Frame Timing** tool so that it can be reviewed later or sent to someone else for review. To save the SteamVR Frame Timing, you will need to do the following.

1.  Right-click on the SteamVR tools and from the displayed menu, select the **Settings** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0a76f50-3a7c-4839-affa-d4fa08b94ffd/steamvr_propref_01.png)
2.  Then from the Settings menu, click on the **Save Frame Data Now** button to save the Frame Data.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2844579d-9fad-4901-aec9-f1be9567ae24/steamvr_propref_03.png)
3.  The Frame Timings will then be saved to a .CSV file called **VRFrames.csv** which can be found under, **C:\\Program Files (x86)\\Steam\\logs**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62c94558-f923-49ec-a6a3-a2cee1cedd7a/steamvr_propref_04.png)