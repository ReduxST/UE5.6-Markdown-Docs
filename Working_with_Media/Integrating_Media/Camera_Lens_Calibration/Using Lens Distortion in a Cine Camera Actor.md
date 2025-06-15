# Using Lens Distortion in a Cine Camera Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lens-distortion-in-a-cine-camera-actor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lens-distortion-in-a-cine-camera-actor-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:29

---

1.  Select your **CineCamera Actor** in the **Outliner** and go to the **Details** panel.
    
    ![Select the CineCamera Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d66ebcfc-b45f-42b8-8040-1de2a6274e89/ue5_01-cine-camera-actor.png "Select the CineCamera Actor")
2.  Select the **LiveLink Component Controller component** and scroll down to the **Camera Role** category. Verify that the correct **Lens File** is assigned to the **Lens File** slot. In this example the **LumixLens** file is used from the [Quick Start Guide](/documentation/en-us/unreal-engine/camera-lens-calibration-quick-start-for-unreal-engine).
    
    ![Select the Live Link Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f034d12d-2704-4a11-bf12-c3bff00a6d2e/ue5_02-live-link-controller.png "Select the Live Link Component")
3.  Click the **Add Component** button, then search for and select **Lens Distortion** to add the component.
    
    ![Add the Lens Distortion component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fed68a59-10c8-4479-9abe-8386d7217b36/ue5_04-lens-distortion.png "Add the Lens Distortion component")
4.  Scroll down to the **Default** section and click the dropdown next to **Distortion Source**. Select the **LumixLens** file and **enable** the **Apply Distortion** checkbox.
    
    ![Add the Lens Distortion Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48d6f86f-89d1-4bc4-b109-9056f00e54e4/ue5_05-distortion-source.png "Add the Lens Distortion Source")
5.  You should now see the lens distortion applied to the CineCamera Actor in the viewport.
    

## Section Results

In this guide you learned how to apply the lens distortion effect from the Camera Calibration plugin to the CineCamera Actor.