# XR Best Practices

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:23

---

Virtual reality (VR) is an immersive new medium, with unique aspects to consider when authoring and presenting content to users on these platforms. Considerations include user comfort, content optimization, and limitations of the platforms. Use this page as a reference for these topics as you develop your projects for VR.

## VR Project Settings

VR projects can be created as a Blueprint or C++ project.

When you create a new project targeting VR platforms, start with the **VR Template** in the **Games** category. The VR Template provides everything you need to start develping VR projects in Unreal Engine 5.

If you don't want to use the VR Template as a base for your project, you can create a new blank C++ or Blueprint project with the following settings:

-   Quality Preset: Scalable
-   Raytracing: Disabled
-   Starter Content: Disabled

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de4d5346-7100-4b43-9a32-d8c029cc97d6/projectsettings.png)

These settings create an Unreal project with minimal rendering features enabled. This ensures that the project starts with a good framerate, and you can add any other rendering features you need.

After you create the project, set the following project settings to improve the performance of your apps:

-   Go to **Edit > Project Settings > Description**, and enable **Start In VR**.
-   From **Edit > Project Settings > Rendering > Forward Renderer**, enable [Forward Shading](/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine).
-   In **Edit > Project Settings > Rendering > Default Settings**, set the **Anti-Aliasing Method** to [Multisample Anti-Aliasing](/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine#enablingmultisampleanti-aliasing) (MSAA).
-   From **Edit > Project Settings > Rendering > VR**, enable [Instanced Stereo](https://docs.unrealengine.com/5.0/en-US/vr-performance-testing-in-unreal-engine).
-   For mobile VR experiences, enable [Mobile Multi-View](/documentation/en-us/unreal-engine/vr-performance-testing-in-unreal-engine) in **Edit > Project Settings > Rendering > VR**.
    -   Also set Mobile HDR to False

## VR .ini Settings

See the [Scalability Reference](/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine) for explanations and examples on scaling the graphics of your app to improve its performance or quality. The following table describes some console variables and their recommended values for VR projects.

| **Console Variable** | **Recommended Value** | **Description** |
| --- | --- | --- |
| **vr.PixelDensity** | 1 | **1** is the ideal resolution for the HMD that is currently being used. Lower values will perform faster but will be undersampled (more blurry), while values over **1** will perform slower and will supersample (extra sharp). |
| **r.SeparateTranslucency** | 0 | This can be expensive for mobile VR experiences because of fill rate limits. It's recommended to disable this feature. |
| **r.HZBOcclusion** | 0 | See the Hierarchical Z-Buffer Occlusion section in the [Visibility Culling](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine) page for more details. |

The following .ini settings are from the UE4-powered VR demo [Showdown](https://www.fab.com/listings/5935f4c1-3b3f-4ef3-8291-c21503af0d77). You can use these settings as a starting point by copying them to your project's **Config/DefaultEngine.ini** file under **SystemSettings**.

```
	`[SystemSettings]  	vr.PixelDensity=1 	r.SeparateTranslucency=0 	r.HZBOcclusion=0 	r.MotionBlurQuality=0 	r.PostProcessAAQuality=3 	r.BloomQuality=1 	r.EyeAdaptationQuality=0 	r.AmbientOcclusionLevels=0 	r.SSR.Quality=1 	r.DepthOfFieldQuality=0 	r.SceneColorFormat=2 	r.TranslucencyVolumeBlur=0 	r.TranslucencyLightingVolumeDim=4 	r.MaxAnisotropy=8 	r.LensFlareQuality=0 	r.SceneColorFringeQuality=0 	r.FastBlurThreshold=0 	r.SSR.MaxRoughness=0.1 	r.rhicmdbypass=0 	sg.EffectsQuality=2 	sg.PostProcessQuality=0`

Copy full snippet
```
\[SystemSettings\] vr.PixelDensity=1 r.SeparateTranslucency=0 r.HZBOcclusion=0 r.MotionBlurQuality=0 r.PostProcessAAQuality=3 r.BloomQuality=1 r.EyeAdaptationQuality=0 r.AmbientOcclusionLevels=0 r.SSR.Quality=1 r.DepthOfFieldQuality=0 r.SceneColorFormat=2 r.TranslucencyVolumeBlur=0 r.TranslucencyLightingVolumeDim=4 r.MaxAnisotropy=8 r.LensFlareQuality=0 r.SceneColorFringeQuality=0 r.FastBlurThreshold=0 r.SSR.MaxRoughness=0.1 r.rhicmdbypass=0 sg.EffectsQuality=2 sg.PostProcessQuality=0

## VR Frame Rate Optimization

Most VR applications implement their own procedures to control the VR frame rate. Because of this, you should disable several general UE4 project settings that can interfere with VR applications.

Follow these steps to disable general framerate settings in UE:

1.  From the editor's main menu, choose Edit > Project Settings to open the Project Settings window.
    
2.  In the Project Settings window, choose General Settings in the Engine section.
    
3.  In the Framerate section:
    
    -   Disable Smooth Frame Rate.
        
    -   Disable Use Fixed Frame Rate.
        
    -   Set Custom TimeStep to None.
        

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32cc0560-6e2b-4c8d-a52e-c04821f0db43/framerate.png)

## VR World Scale

Ensuring the correct scale of your world is one of the most important ways to help deliver the best user experience possible on VR platforms. Having the wrong scale can lead to all kinds of sensory issues for users, and could even cause simulation sickness. Objects are most easily viewed in VR when they are in a range of 0.75 to 3.5 meters from the player's camera. Inside of UE4, 1 Unreal Unit (UU) is equal to 1 Centimeter (CM). This means that objects inside of Unreal are best viewed when they are 75 UU to 350 UU away from the player's camera (when using VR).

| **Distance** | **Distance in Unreal Units (UU)** |
| --- | --- |
| 1 centimeter | 1 Unreal Unit |
| 1 meter | 100 Unreal Units |
| 1 kilometer | 100,000 Unreal Units |

You can adjust the scale of your world using the **World to Meters** variable located under **World Settings**. Increasing or decreasing this number will make the user feel larger or smaller in relation to the world around them. Assuming your content was built with 1 Unreal Unit = 1 cm, setting **World To Meters** to **10** will make the world seem very large, while setting World To Meters to **1000** will make the world seem very small.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f561a73e-97ea-4f85-bb67-b7dca7934714/worldscale.png)

## VR and Simulation Sickness

Simulation sickness is a form of motion sickness that can affect users during immersive experiences. The following list describes some best practices to limit the discomfort that users can experience in VR.

-   **Maintain framerate:** Low framerates can cause simulation sickness. Optimizing your project as much as possible can improve the experience for the user. See the following table for the recommended frame rates that you need to target for your XR platform.

| **HMD Device** | **Target Frame Rate** |
| --- | --- |
| Oculus Rift S | 90 |
| Oculus Quest 1 | 72 |
| Oculus Quest 2 | Situational: 72/80/90/120 |
| HTC Vive | 90 |
| HTC Vive Pro | 90 |
| Valve Index | 90 minimum, up to 144 |
| HP Reverb | 90 |
| Windows Mixed Reality VR | 90 |
| PSVR | Situational: 60/120, 90/90, and 120/120 |

\* **User testing:** Test with many different users, and monitor any discomfort they might experience from the VR app to prevent simulation sickness.

-   **Keep users in control of the camera:** Cinematic cameras, or anything that takes control of camera movements away from the player, contribute to user discomfort in immersive experiences. Camera effects, such as head bobbing and camera shaking, should be avoided because they can lead to user discomfort if the user is not controlling them.
    
-   **Field of View (FOV) must match the device:** The FOV value is set through the device's SDK and internal configuration, and matches the physical geometry of the headset and lenses. Because of this, the FOV should not be modified in UE, and should not be modifiable by the user. If the FOV value is changed, the world can appear to warp when you turn your head, leading to discomfort.
    
-   **Use lights and colors that are more dim, and avoid smearing:** When designing elements for VR, you might need to use dimmer lights and colors than you normally would. Strong and vibrant lighting in VR can cause simulation sickness to occur more quickly. Using cooler shades and dimmer lights can help prevent user discomfort. This also helps with preventing smearing between bright and dark areas on the display.
    
-   **Movement speed should not change:** Users should start at full speed instead of gradually accelerating to full speed.
    
-   **Avoid post process effects that greatly affect what the user sees:** Avoid post process effects such as Depth of Field and Motion Blur to prevent user discomfort.
    
-   Visual Effects such as Motion Blur and Depth of Field should be avoided.
    
-   Consider things like character height, width, speed, and camera location as they need to be slightly modified for VR characters.
    

## VR Camera Setup

VR camera setup in UE4 depends entirely on whether your VR experience is seated or standing:

-   **Seated experience:** You will need to artificially raise the camera origin to the desired player height for the project. And call the Set Tracking Origin function, with Origin set to "Eye Level".

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3100704d-9b6b-41d5-a147-cddfec7a83f5/vr_seated_experience.png)

-   **Standing experience:** Make sure the camera origin is set to **0**, relative to the pawn's root, which is typically on the ground. Attach a camera component to a scene component at the base of the pawn, at the ground level. And call Set Tracking Origin with the Origin parameter set to Floor Level.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1f0ab20-0fd0-4b3c-ac68-778894203b04/vr_standing_experience.png) ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc0e3238-a2cd-4053-93c2-38a8f8a8549f/trackingorigin.png)

## VR Content Considerations

When creating VR content, remember that users can look at that content from multiple angles. Use the following list as a reference as you create content for VR:

-   **Scale:** The scale of objects in a VR world should mimic reality as closely as possible. Making objects bigger or smaller than their real world counterparts could lead to confusion or [simulation sickness](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine#vrandsimulationsickness).
    
-   **Missing Polygon Faces:** In non-immersive experiences, it is a common practice to remove polygon faces from objects that cannot be seen by the player. However, in VR experiences, players may have more freedom to look around. Missing polygon faces can sometimes lead to users being able to see things that they're not supposed to see.
    
-   **Lighting Types:** You should use [Static Lights](/documentation/en-us/unreal-engine/static-light-mobility-in-unreal-engine) and Lightmaps for VR projects. This is the cheapest lighting option to render. If you need to use dynamic lighting, make sure to limit the amount of dynamic lights to as few as possible, and make sure that they never touch one another.
    
-   **VR and VFX:** Some VFX tricks, like using SubUV Textures to simulate fire or smoke, do not hold up very well when viewed in VR. In many cases, you will need to use static meshes instead of 2D particles to simulate effects like explosions or smoke trails. Near-field effects, or effects that happen very close to the camera, work well in VR, but only when the effects are made up of Static Mesh particles.
    
-   **VR and Transparency:** In 3D graphics, rendering transparency is extremely costly, because transparency will generally have to be reevaluated per frame to ensure that nothing has changed. Because of this reevaluation, rendering transparency in VR can be so costly that its cost outweighs its benefits. However, to get around this issue, you can use the **DitherTemporalAA** Material Function. This Material Function will allow a Material to look like it is using transparency and can help avoid common transparency issues, such as self-sorting. ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45292a40-c394-4d68-827c-3566dc9942cf/vr_dither_trans_aa.png) *Click for full image.*
    
    -   **Fake everything you can:** Finding clever ways to recreate expensive rendering options, like dynamic shadows or lighting, can be a huge win for hitting your performance goals in VR. In [Showdown](https://www.fab.com/listings/5935f4c1-3b3f-4ef3-8291-c21503af0d77), having the characters cast dynamic shadows proved to be too expensive per-frame, which meant that dynamic shadows had to be cut from the project. However, this made the characters look like they were floating while moving. To fix this, fake blob shadows were introduced that could dynamically adjust their position and intensity based on how close the character was to an object in the world. This helped give the illusion that a character was casting shadows when they came close to the ground (or other objects).
-   ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1aaf0bc5-6686-4cae-a967-6c51e7e80caf/vr_fake_shadow_material.png) *Click for full image.*
    

## Known Limitations

Below you will find a list of features that might not work as expected in VR because of how HMDs are designed, along with possible workarounds to address them.

-   **Screen Space Reflections(SSR):** While SSR will still work in VR, the reflections they produce could have issues matching up to what it is reflecting in the world. Instead of using SSR, use Reflection Probes as they are much cheaper and suffer less from reflection-alignment issues.
    
-   **Screen Space Global Illumination:** Screen space techniques can generate differences between the displays for the two eyes in the HMD. These differences can cause user discomfort. See [Lighting Types](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine) for recommended lighting types in VR for replacements.
    
-   **Ray Tracing:** VR apps using ray tracing currently aren't able to maintain the resolution and frame rate needed for a comfortable VR experience.
    

### Normal Mapping Issues

When viewing Normal maps on objects in VR, you will notice that they do not have the impact that they might have once had. This is because Normal mapping does not account for having a binocular display or motion parallax. As a result, Normal maps often look flat when viewed with a VR device. However, that does not mean that you should not or will not need to use Normal maps; it just means that you need to more closely evaluate if the data in the Normal map would be better off made out of geometry. Below, you will find a technique that can be used in place of Normal maps.

-   **Parallax Mapping:** Parallax mapping takes Normal mapping to the next level by accounting for depth cues that Normal mapping does not. A Parallax mapping shader can better display depth information, making objects appear to have more detail than they do. This is because no matter which angle you look at, a Parallax map will always correct itself to show you the correct depth information from your viewpoint. The best use of a Parallax map would be for things like cobblestone pathways and surfaces with fine detail.