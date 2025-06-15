# Orthographic Camera

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/orthographic-camera-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/orthographic-camera-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:44

---

Unreal Engine supports Orthographic camera projection, which can be used for projects like isometric games and architectural visualization projects. The orthographic camera works with other Unreal Engine features, including Lumen, Nanite, Virtual Shadow Maps (VSMs), Temporal Super Resolution, reflections, volumetrics, path tracing, and the water system.

## Example scenes

![Orthographic camera example 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49346d49-a07a-44bc-adee-8000fc71b172/example1.png) ![Orthographic camera example 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2465a4e0-d52d-4d62-b6d0-6958a70385ae/example2.png) ![Orthographic camera example 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e05ab47c-ea53-48e8-bb24-03a4b2dcb1b9/example3.png) ![Orthographic camera example 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/def70ccd-5f2e-49dd-92a1-b7b36465b103/example4.png)

## Set Up A Camera With Orthographic Projection

To set up a camera with Orthographic projection, follow these steps:

1.  Place a **Camera** actor in the level.
2.  Select the placed camera in the level editor **Outliner**.
3.  In the **Details** panel under **Camera Settings**, use the **Projection Mode** dropdown to select **Orthographic**.
4.  Move and rotate your camera using the **Actor Transforms** in the Details panel.

Cinematic cameras do not have an option to use an orthographic view.

![Orthographic camera settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d7e9c8d-ca15-4268-a89c-c9415c4c8c17/ortho_camera_settings.png)

You can change the following settings to adjust the Orthographic rendering.

| Setting Name | Description |
| --- | --- |
| **Ortho Width** | Expand this to see the details about your media's resolution, frame rate, size, method, format, combined level of detail bias, and its number of mips and tiles. |
| **Auto Calculate Ortho Planes** | When selected, automatically resolve depth clip planes on the specified Ortho Width. When not selected, you can manually set the near clip plane and far clip plane of the Orthographic camera. |
| **Auto Plane Shift** | Manually adjust the planes of this camera, maintaining the distance between them. Positive values move out the far plane, and negative values move towards the near plane. |
| **Ortho Near Clip Plane** | When **Auto Calculate Ortho Planes** is not selected, this sets the location of the near clip plane of the Orthographic camera. |
| **Ortho Far Clip Plane** | When **Auto Calculate Ortho Planes** is not selected, this sets the location of the far clip plane of the Orthographic camera. |
| **Update Ortho Planes** | Adjust the near and far planes and the view origin of the current camera automatically to avoid clipping and causing lighting artifacts. |
| **Use Camera Height as View Target** | When **Update Ortho Planes** is selected, this setting uses the camera’s current height to compensate for the distance to the general view (as a pseudo distance to the view target when one isn’t present). |
| **Aspect Ratio** | Set a width to height ratio for the camera view masking, or use the dropdown to select one of the common preconfigured aspect ratios. |

## Auto Calculating Ortho Planes

The **Auto Calculate Ortho Planes** property scales the near clip plane based on the angle of the camera compared to the ground surface. The near clip plane distance is evaluated to a negative value using the Ortho Height. The default minimum near clip plane location is around 1.4 times the size of the ortho height being applied behind the camera. This can be compensated for using the console variables below.

The far clip plane distance initially determines the ratio of Unreal units (measured in centimeters by default) per pixel. This value is used to scale the distance between the near and far clip planes to a multiple of the max FP16 value (66504.0f). Depending on the Ortho Width and the Unreal unit to pixel ratio, this can scale up to the UE\_OLD\_WORLD\_MAX distance (21 kilometers). The smaller the scene, the shorter the far clip plane distance should be to preserve depth precision when downscaled to a 16-bit buffer.

### Auto Calculating Ortho Planes Console Variables

| Console Variable Name | Description |
| --- | --- |
| `r.Ortho.AutoPlanes` | Globally allow orthographic cameras to use the automatic near and far clip plane calculations. |
| `r.AutoPlanes.ClampToMaxFPBuffer` | When automatically calculating orthographic planes, this determines whether 16-bit depth scaling should be used. 16-bit scaling helps with any depth downscaling that occurs. For example, HZB downscaling uses 16-bit textures instead of 32-bit textures. This feature calculates the maximum depth scale needed based on the Unreal unit (centimeters by default) to pixel ratio. Smaller scenes don't need 32-bit depth range, because most actors will be within a reasonable visible frustum, so a 16-bit depth range is used instead. For larger scenes, the plane distance scales up to a maximum of UE\_OLD\_WORLD\_MAX (21 kilometers), which is the typical full range of the depth buffer. |
| `r.Ortho.AutoPlanes.DepthScale` | Adjust the 16-bit depth scaling from the default FP16 Max (66504.0f). This is useful if the far clip plane doesn't need to be as far away, so it will improve depth deltas. |
| `r.Ortho.AutoPlanes.ShiftPlanes` | Shift the whole frustum in the Z direction. This can be useful if you need the near clip plane closer to the camera, at the reduction of the far clip plane value (for example, in a horizontal 2.5D scene). |
| `r.AutoPlanes.ScaleIncrementingUnits` | Select whether to scale the near or far plane's mininum and maximum values as we increase in unit to pixel ratio. For example, going from centimeters to meters to kilometers. |

## View Origin Correction

Orthographic cameras have an issue with the camera’s world position not lining up correctly with the actual view location due to the lack of depth. This can be seen visually when lighting and other effects do not resolve correctly between the view position and the camera’s real world position. As a result, you can use console variables to correct the camera’s view origin to represent the true view position rather than the camera world location.

![World position not aligned with view location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73fa64b1-2b27-4d62-ba24-a7747cc457d5/view-origin1.png) ![World position aligned with view location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c5e1da9-0a93-4d22-a3de-41288d288b3b/view-origin2.png)

### View Origin Correction Console Variables

| Console Variable Name | Description |
| --- | --- |
| `r.Ortho.AllowNearPlaneCorrection` | When enabled, orthographic cameras automatically update to match the near plane location, and force the camera position to be replaced by the near clip plane location for the projection matrix calculation. This is useful since orthographic near clip planes can be behind the camera position, which causes some issues with the engine resolving lighting behind the camera position. |
| `r.Ortho.DefaultUpdateNearClipPlane` | The orthographic near clip plane value to update to when using near plane correction. |
| `r.Ortho.CameraHeightAsViewTarget` | When enabled, use the camera height as the view target when calculating near plane correction. Primarily helps with VSM clipmap selection and avoids overcorrecting near planes. |

## Virtual Shadow Maps

When using a mix of Nanite and non-Nanite geometry, Virtual Shadow Maps can be tricky with orthographic rendering, mirroring how tricky they can be in perspective mode. It can be difficult to get the right balance of settings. The following console variables allow some custom control over how VSMs resolve and select the correct draw resolutions for the scene.

### Virtual Shadow Maps Console Variables

| Console Variable Name | Description |
| --- | --- |
| `r.Ortho.VSM.EstimateClipmapLevels` | When enabled, calculate the First Level VSM based on the current camera Ortho Width. |
| `r.Ortho.VSM.ClipmapLODBias` | The LOD bias to use for adjusting the VSM first level. |
| `r.Ortho.VSM.ProjectViewOrigin` | When enabled, move the WorldOrigin of the VSM clipmaps to focus around the ViewTarget (if present). |
| `r.Ortho.VSM.RayCastViewOrigin` | When enabled, estimate the ViewOrigin with a raycast if the ViewTarget is not present (such as for a standalone camera). |

## Debug Camera Views

The orthographic camera includes debug options that you can use to force all cameras (excluding editor views) to resolve to orthographic. These options are disabled in shipping builds.

### Debug Camera Views Console Variables

| Console Variable Name | Description |
| --- | --- |
| `r.Ortho.Debug.ForceAllCamerasToOrtho` | When enabled, force all cameras in the scene to use Orthographic views. |
| `r.Ortho.Debug.ForceOrthoWidth` | When enabled, adjust the Ortho Width when using the ForceAllCamerasToOrtho option. |
| `r.Ortho.Debug.ForceUseAutoPlanes` | When enabled, use the automatic near and far clip plane evaluation when using the ForceAllCamerasToOrtho option. |
| `r.Ortho.Debug.ForceCameraNearPlane` | When enabled, adjust the near clip plane when using the ForceAllCamerasToOrtho option. Ignored if ForceUseAutoPlanes is enabled. |
| `r.Ortho.Debug.ForceCameraFarPlane` | When enabled, adjust the far clip plane when using the ForceAllCamerasToOrtho option. Ignored if ForceUseAutoPlanes is enabled. |
| `r.Ortho.EditorDebugClipPlaneScale` | Only affects the editor orthographic debug viewports in Lit modes. Set the scale to proportionally alter the near clip plane based on the current **Ortho Width**. This changes when geometry clips in the scene as the orthographic zoom is changed. Helpful for visualizing illuminated meshes of varying sizes in the debug plane views. Other light artifacts may appear when this value changes. |

## Limitations and Additional Notes

Unreal Engine’s priority has always been perspective view cameras, and as new engine features are added, they might not be optimized for Orthographic cameras, though we will strive for feature parity going forward.

The following console variables can be useful in certain scenarios.

| Console Variable Name | Description |
| --- | --- |
| `r.Ortho.DepthThicknessScale` | Adjust the depth thickness scale of the scene. Orthographic scene depth typically scales proportionally lower than perspective, on a scale of 1/100. For instance, Lumen depth difference testing works better at this scale. In some cases, like if very small surface-to-surface depth differences are being used, you might need to use this value to adjust the scale of depth thickness testing values simultaneously across various screen trace passes. |
| `r.Ortho.CalculatingDepthThicknessScale` | Whether to automatically derive the depth thickness test scale from the near / far plane difference. This is enabled by default. However, when disabled (0), the scaling specified for `r.Ortho.DepthThicknessScale` is used. |
| `r.Ortho.FogHeightAdjustment` | When enabled, the orthographic camera height is used to determine the fog cutoff height. |
| `r.Ortho.UsePreviousMotionVelocityFlattenPass` | Sets whether the orthographic camera motion blur pass should use the previous falttened textures (such as those from temporal super resolution). Note that this can cause shimmering on planes in the distance when disabled. |

### Volumetric Clouds with Orthographic Camera

Volumetrics can present problems with orthographic camera views, especially with volumetric clouds. This is mostly caused by the way the scene scales when using an orthographic view. For example, if you were to look at volumetric clouds in an orthographic view, you don't get the perspective part of the cloud, and instead get something like a 10 meter by 10 meter window.