# Synchronization in nDisplay

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/synchronization-in-ndisplay-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/synchronization-in-ndisplay-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:19

---

*Synchronization* is a vital part of displaying multiple sections of real-time content over a large display. All systems within the render/display ecosystem must adhere to strict timing, measured in milliseconds, to produce the illusion of a seamless display.

Multi-display setups often require syncing capabilities at both software and hardware levels. Not only should the generated content be ready at the same time on all PCs, using the same timing information for simulation, but the display swap (the changing out of the current image for the next image in the video card buffer) needs to also happen at the correct time to prevent tearing artifacts in the display.

For VR and other types of stereoscopic displays, the issue of synchronization applies doubly since the two different frames—one for each eye—must coordinate perfectly.

## Determinism

There are two types of approach for managing synchronization:

-   **Deterministic:** Each server (PC, rendering node) is set up in such a way that the output is always predictable given a particular set of inputs, which means the only information the server needs to synchronize with other machines in the system is an accurate time, and input/output information for each individual machine.
-   **Non-deterministic:** To ensure synchronization, the system forces replication of the transform matrices and other relevant characteristics of all actors or objects in a scene, and reproduces them throughout the system.

Each approach has pros and cons. The main advantage of a deterministic system is project simplicity, and the data bandwidth saved by not sharing transform data for each object at every frame. The downside is that if one system diverges, the divergence will have unknown issues over time. Rendering uniformity could be severely compromised, leading to visual discontinuity and artifacts.

## Hardware Sync and Genlock

While the *nDisplay primary PC* ensures that all\_ cluster (node) PCs\_ are informed of timing information from a gameplay perspective (for example, which frame to render), specialized hardware sync cards and compatible professional graphics cards are necessary to synchronize the display of those rendered frames at exactly the same time on the physical display devices.

For example, in broadcast applications, it is common to synchronize many devices such as cameras, monitors, and other displays so they all switch and capture the next frame at precisely the same time. In this industry, the use of *generator-locked signals (genlock)* is widely adopted and used.

Typically, the setup is composed of a hardware generator that sends the clock to the hardware that requires synchronization. In the case of PCs used for real-time rendering, professional graphics cards such as those in the NVIDIA Quadro line support this technology alongside the NVIDIA Quadro Sync II card, which will lock to the received timing signal or pulse.

System Topology

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c5c5183-7e0d-45e4-a1b8-f1671dfa2f80/primarynode.png)

Primary Node (house clock generator)

Cluster Nodes (receiving clock from primary node GPU)

When using Quadro Sync:

-   Use "Production Branch/Studio" drivers preferentially because they tend to be more stable than "New Feature Branch" drivers.
-   Trigger sync pulses using "falling edges", because they tend to be more reliable than "leading edges" in detecting the correct signal rate.

## Display Synchronisation Demystified

-   **Framelock only:** Using daisy-chaining techniques across GPUs, this method is what NVIDIA commonly calls *FrameLock/SwapSync*. No genlock is used here. A GPU on the primary nDisplay PC gets a master clock from an output display or processor connected to it, then propagates it to the render-node PC GPUs. All PCs are connected within tree topology, where primary PC is the root. This approach allows the use of NVIDIA swap groups/barriers via the NVIDIA API.
    
    This approach is not well suited for virtual production since it works in isolation from other devices used within the space, with all of them being synced with an external master clock.
    
-   **Genlock only:** With this scheme, all cluster PC GPUs get their own master clock signal (genlock) from the same source. In other words, each PC gets its own BNC cable, and all cables are connected to the same master clock generator.
    
    This approach allows synchronization of VSync; however, NVIDIA barriers are not available via NVIDIA API. Technically, all cluster PCs are framelocked to the received clock. However, this approach has not proven to be 100% reliable because there is no accurate control over frame presentation on the application level.
    
    This is the method used before, and why we had to implement an "advanced" sync policy that would reduce the probability of unsync/glitches.
    
-   **Genlock + framelock: This approach is the most desirable for virtual production.** All stage devices are connected to a master clock, including the primary nDisplay PC GPU. In-cluster synchronization is accomplished using daisy-chain connections between the primary PC and the render node PCs.
    
    This approach provides for the use of the NVIDIA API, and therefore utilizes NVIDIA barriers, which gives UE control over frame presentation on the application level. This provides the most reliable method of synchronizing displays, together with a provided external clock (genlock).
    

## Daisy Chain vs. Direct Genlock

*Daisy-chaining* is a signal-locking technique that is used alongside direct genlock, where the master clock is sent to a single PC or device—in this case, the primary PC. Separate cables then propagate the signal to all other PCs. Although previous experience with nDisplay suggests that direct genlock (where each PC receives the clock directly from the primary source) is simpler and more effective than daisy-chaining, the new hardware approach based on daisy-chaining gives hope to a more reliable and cost-effective solution to signal locking. This solution is called *NVIDIA Swap Sync/Lock*.

## NVIDIA Mosaic and AMD EyeFinity

*Mosaic mode* from NVIDIA and *EyeFinity* from AMD are similar GPU technologies that combine and synchronize multiple outputs within one graphics card so that they appear as a unique display from the OS or software perspective. This virtual display is essentially an aggregation of multiple physical displays acting as one synchronous display that can also be synced to other displays from different systems using underlying framelock or genlock techniques.

The process of locking multiple displays using a house clock is called *framelocking*. *Genlocking* is when an external clock is used instead. In the context of genlock, the external clock is used throughout all devices, including display devices, cameras and tracking sensors.

Assuming GPUs are properly connected using Quadro Sync II cards or Firepro S400 cards, both Mosaic and Eyefinity technologies allow multiple outputs to have the exact same clock, and to be treated as one big display canvas from an operating system perspective. You can create one or as many Mosaic or Eyefinity groups per PC but not across PCs—each PC must have it's own Mosaic or Eyefinity group.

To synchronize displays that are driven by multiple PCs or GPUs using daisy-chaining techniques, one GPU must act as the master clock generator and share its clock to the other GPUs—either on the same PC or different PC—using sync cards like the Nvidia Quadro Sync II or AMD Firepro S400.

For more information, see [Mosaic Technology for Multiple Displays | NVIDIA](https://www.nvidia.com/en-gb/design-visualization/solutions/nvidia-mosaic-technology/) and [Multi-Display Eyefinity Technology](https://www.amd.com/en/technologies/eyefinity).

Although it is possible to have a MOSAIC virtual display spawn across multiple GPUs within one PC, currently, it would be slow to have an application window over that canvas. (Future work may possibly enable this.) Today, this approach would not be recommended for virtual production or in-camera VFX.

## Other Aspects of Display Sync

The game and render threads are always synchronized by what are called thread barriers. This is the core feature for both of the two items below. It is not possible to disable barriers. Consider them as points on a timescale that help the primary node deal with the cluster nodes synchronously to provide a uniform content experience across multiple UE PCs.

| Feature | Description |
| --- | --- |
| **Software/Simulation (what you should see)** | The process of synchronizing all software-related matters. It is about making Unreal Engine and its content properly sync: feature determinism, delta-time synchronization, input replication, custom transforms, thread barriers, cluster events, game logic, and so on. |
| **Hardware/OS (how you should see content)** | The process of synchronizing hardware devices such as GPUs, display devices, and the *DWM* (Desktop Window Manager) using one shared clock—a house sync or genlock signal. It is how to make an operating system and hardware show what you want synchronously, without tearing. This requires NVIDIA Quadro graphics cards, plus Sync II cards, plus a genlock generator. Expect at least a one-frame hardware delay if this is not enabled. |

## Render Sync Policies

Render Sync Policies define how to synchronize the rendering output. This parameter can be set in the Cluster's Details panel in the [nDisplay 3D Config Editor](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine).

The following table describes the available options for **Render Sync Policy**.

| Option | Description |
| --- | --- |
| None (Sync Policy 0) | This means VSync=0. All nodes show their frames after RenderThreadBarrier WITHOUT synchronization to VBlank. This gives maximum FPS at the cost of potential tearing artifacts. |
| Ethernet (Sync Policy 1) | All nodes show their frames after RenderThreadBarrier WITH synchronization to VBlank. Output displays won't have tearing. Note that tearing can still be possible among the displays because of Windows DWM and runtime or driver settings. |
| NVIDIA (Sync Policy 2) | 
NVIDIA hardware framelock (NVIDIA SwapLock API) based on daisy-chain connection. You can use the parameters in the NVIDIA section to tweak some specific hardware settings relating to frame lock.

-   Sync Group: The sync group to use for frame locking. The default value is 1.
-   Sync Barrier: The sync barrier to use for frame locking. The default value is 1.



 |
| Custom | Configures any custom sync policy that nDisplay is not aware of. A policy ID and any amount of key-value parameters are required. |

Previously, we developed a sync mechanism called *Advanced Sync* for specific circumstances where the rendering of a frame on a given nDisplay PC would happen after VBlank, creating tearing on screen. This software mechanism tries to predict those events, and forces all PCs to skip and render on the next VBlank. This mechanism is not 100% perfect and can have a non-desirable performance impact when enabled.

More recently, we implemented the NVIDIA API for synchronization (Sync Policy 2), which is a hardware-supported approach to the problem.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f5e5b85-ac69-46da-bc87-8ae967bedd15/framelockconnectionstimingserver.png)

Framelock connections on a timing server: 1) Timing server 2) Clients.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/887723eb-8971-4a8e-b9f0-f4f5f102f4fe/syncsource.png)

1) Sync source 2) Server 3) Clients

## Getting Sync to Work

For reliable sync in the context of virtual production, you have to use a technique that combines both genlock and framelock. To summarize, you feed the genlock signal to the primary nDisplay PC, then use the daisy-chaining hardware method to dispatch the incoming sync signal to all remaining cluster PCs so that they are properly framelocked. This implies an NVIDIA Render Sync Policy that needs to be properly defined within the configuration asset.

### Workflow

1.  Set up daisy-chain connection among cluster GPU sync boards using regular ethernet cable with regular RJ45 connectors.
2.  Enable MOSAIC, and configure synchronization via NVIDIA control panel (set a primary PC, then set sync cluster nodes).
3.  Enable DirectX Swapgroup PrePresentWait using the following steps:
    1.  Download [nVidia Configure Driver Utility](https://www.nvidia.com/en-us/drivers/driver-utility/).
    2.  Run **ConfigureDriver.exe** as administrator.
    3.  Type "11" and press **Enter**.
4.  In the nDisplay 3D Config Editor, set the Cluster's **Render Sync Policy** to **NVIDIA**.
5.  *Optional:* For complex systems, it's possible to customize the NVIDIA swap group and sync barriers in the Cluster settings.

By default, sync group 1 and sync barrier 1 are used.

The NVIDIA Render Sync Policy cluster setting enables an NVIDIA swap group over cluster nodes.

### Additional Comments

A 0 value is not allowed. A 0 value is used internally to detach/leave a group/barrier. Only natural numbers are allowed. On a simple system with one GPU and one sync board, you have single sync group #1 and single sync barrier #1. Those are used by default.

## Synchronization Testing

Testing synchronization for a scaled display can be tricky because desynchronization can result from any number of issues, including:

-   The wrong frame is simulated due to incorrect timestamp (software issue).
-   The display device timing is off (display or hardware issue).

To test sync, we use a simple test project displaying a single object that moves quickly across the entire display surface. When systems are properly in sync, the object retains its form as it passes across boundaries. Otherwise, the display will show artifacts at shared edges.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1aeb3abe-62f2-4250-adb9-1e5453553ce1/screenonescreentwo.png)

When systems are properly in sync, the object retains its form as it passes from Screen 1 to Screen 2.

## Links to Additional Information

-   [NVIDIA QUADRO G-SYNC II](https://www.nvidia.com/content/dam/en-zz/Solutions/design-visualization/quadro-product-literature/Quadro_GSync_install_guide_v4.pdf)
    
-   [Chapter 30, Configuring Frame Lock and Genlock](https://download.nvidia.com/XFree86/Linux-x86_64/304.137/README/framelock.html)
    
-   [QUADRO SYNC II](https://images.nvidia.com/content/quadro/product-literature/user-guides/Quadro-Sync-II-User-Guide.pdf)
    
-   [NVIDIA Recommended Display Adapters](https://nvidia.custhelp.com/app/answers/detail/a_id/4449/~/nvidia-recommended-display-adapters)