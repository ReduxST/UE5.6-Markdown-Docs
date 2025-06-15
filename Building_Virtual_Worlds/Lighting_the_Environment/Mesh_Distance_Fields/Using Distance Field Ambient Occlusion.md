# Using Distance Field Ambient Occlusion

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-distance-field-ambient-occlusion-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-distance-field-ambient-occlusion-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:59

---

In your games, you may rely mostly on screen space techniques to provide dynamic Ambient Occlusion (AO) or even precomputed lighting to make objects feel grounded in the world. These techniques are very useful but have their limitations. [Screen Space Ambient Occlusion](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine) (SSAO) is limited to using scene depth and can only work within the visible screen space. Precomputed methods only work for static objects in the world, which means they can't update in realtime. [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine) (DFAO) is a fully dynamic AO method using [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) for movable Static Meshes. It is also not limited to only being used in dynamically lit worlds; it can be used with precomputed lighting.

In this guide, you'll learn how to enable DFAO for your scene with a Sky Light and then explore the settings that can be adjusted.

## Steps

This feature requires that **Generate Mesh Distance Fields** be enabled in your **Project Settings** in the **Rendering** section. See how to [enable Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#enablingdistancefields) here, if you have not done so already.

1.  Start by navigating to the **Place Actors** panel, then in the **Lights** tab, select and drag a **Sky Light** into the Level Viewport.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19d43ea3-6cec-46cb-8349-b5bef0ab32c2/addskylight.png)
2.  With the Sky Light selected, navigate over to its **Details** panel and set its **Mobility** to **Movable**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/103ae942-3453-43e1-9af1-b4e8aff6965d/transformmobility.png)

## End Result

Once the Sky Light is set to Movable, Distance Field Ambient Occlusion will automatically be enabled for your level.

![Sky Light | without | Distance Field Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d784b701-66f0-4bcc-a968-c87ad7f2eaa4/nodfaoscene.png)

![Sky Light | with | Distance Field Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/548d172b-198f-47f6-a4e6-4e407962b601/dfaoenabledscene.png)

You can see in this comparison example how much of a difference adding a Sky Light to your scene can make when Distance Field Ambient Occlusion is enabled.

## Additional Sky Light Settings

Use the [Distance Field Reference](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine#skylight) to learn about settings specific to [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine) for Sky Lights. These settings enable you to have artistic control over your scene, like controlling the accuracy of the occlusion, its tint and contrasts, and more.