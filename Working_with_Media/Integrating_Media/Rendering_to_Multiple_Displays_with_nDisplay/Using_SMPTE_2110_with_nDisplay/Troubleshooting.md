# Troubleshooting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/troubleshooting-smpte-2110-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/troubleshooting-smpte-2110-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:07

---

This guide is for troubleshooting problems you might encounter when using SMPTE 2110 with NVIDIA Rivermax.

-   In the log, if you expect your system to support GPUDirect but you see the following message:
    
    `Cuda device doesn't support RDMA. GPUDirect won't be available for Rivermax`
    
    Verify your environment variables and make sure `RIVERMAX_ENABLE_CUDA` is set to 1.
    
-   When opening a RivermaxMediaSource, if you see the following message:
    
    `RTP dynamic header data split is not supported for device IP`
    
    Make sure `INTERNAL_CPU_MODEL` is set to `SEPARATED_HOST(0)` when running this command:
    
    `mlxconfig.exe q | findstr "REAL_TIME_CLOCK_ENABLE INTERNAL_CPU_MODEL"`
    
-   When opening a RivermaxMediaSource, if you get the following warning in the log:
    
    `Could not attach flow to stream. Status: 13.`
    
    You are using a ConnectX-6 card (not a BlueField-2), so verify the **Time Source** in Unreal Engine’s project settings and set it to **System**.
    
    ![The Time Source setting for the Nvidia Rivermax plugin.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97b6a5d6-d1f0-4153-b8ce-3af18460cef3/image_0.png)
    
    The Time Source setting for the Nvidia Rivermax plugin.
    
-   When opening a RivermaxMediaSource, if the displayed image is rainbow-colored and this is not expected, make sure these commands show the same output: `mlxconfig.exe q | findstr "FLEX_PARSER_PROFILE_ENABLE PROG_PARSE_GRAPH"`
    
    ![Validate these commands have identical output.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/336aa985-f3e9-4b3c-a25a-b59df13310bb/image_1.png)
    
    Validate these commands have identical output.
    
-   If you see tearing on the wall when using ST 2110 to drive it, validate PTP on all nodes.
    
    1.  Use Putty to connect to the COM port of your BlueField-2 card and login as root.
        
    2.  In the root folder, run the `firefly_monitor.sh` script. This verifies that the DOCA container is running, and prints out PTP status.
        
        ![The output of firefly_monitor.sh.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f40e953-7b7e-4001-8935-c03e6aa95ae0/image_2.png)
        
        The output of firefly\_monitor.sh.
        
    3.  Validate that each node has the same value for `gmIdentity` (grandmaster clock identity), otherwise they won’t have the same time reference.
        
    4.  Verify that the values of `gmPresent` and `ptp_stable` are valid.
        

## Important Information

-   **For UE 5.3-5.4, will be removed in the future:** There is a limiting factor on network packet size and pixel grouping with respect to SMPTE 2110. Due to that limit, some resolutions will require at least one packet to be of a different size than the rest. This is known to cause an inter-packet jitter in Rivermax. We recommend using standard resolutions, as those resolutions do not face this issue. However, if this isn’t possible, UE will still attempt to divide frame data into evenly sized packets; if that doesn’t work, the last packet per frame will be a different size than the rest. You can disable the ability to send uneven packets by setting the following cvar: `Rivermax.Output.EnableMultiSRD=0` If the resolution isn’t divided into same sized packets, the following message appears in the UE Log: "Due to resolution YOUR\_RESOLUTION, row data will be sent over multiple packets with varied sizes."
    
-   For version 1.41.11 of Rivermax and UE 5.4, the default value of the `Rivermax.Output.ForceSkip` console variable has changed to 0, which is the recommended value. In UE 5.3 Rivermax.Output.ForceSkip=1 was used and was known to cause issues after a prolonged playback. This cvar was an artificial way for UE to handle the issues fixed natively by the `RIVERMAX_TX_DELAY_ADAPTIVE_AUTO_CORRECTION_FACTOR` environment variable provided by Rivermax 1.41.11