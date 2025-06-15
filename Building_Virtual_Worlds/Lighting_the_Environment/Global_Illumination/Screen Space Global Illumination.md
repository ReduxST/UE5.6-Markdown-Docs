# Screen Space Global Illumination

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:58

---

**Screen Space Global Illumination** (SSGI) is an **Unreal Engine** feature that aims to create natural-looking lighting by adding dynamic indirect lighting to objects within the screen view. SSGI also makes it possible to have dynamic lighting from emissive surfaces, such as neon lights or other bright surfaces.

Screen Space Global Illumination works best as a supplimental indirect lighting illumination method to precomputed lighting from [Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine).

![SSGI Disabled with Baked Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d654c308-b491-47d4-87ab-1fa766eb5ebc/01-screen-space-disabled.png)

![SSGI Enabled with Baked Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39af55d7-5363-4376-8b38-edd9c5728fe5/02-screen-space-enabled.png)

## Using SSGI

Use the following properties and console variables when working with SSGI.

You can enable Standalone SSGI in the **Post Process Volume** settings by enabling the **Method** and choosing **Screen Space (Beta)** from the dropdown menu.

![Enable Global SSGI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fb7bb8a-e000-404d-b72c-a15a4fa49b64/03-screen-space-enable-ssgi.png)

### Controlling Quality

SSGI has several quality settings that you can enable using the following command:

```
	`r.SSGI.Quality`

Copy full snippet
```
r.SSGI.Quality

Use a value between 1 and 4 to change the quality:

   ![Quality level 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1346d4a-02e0-453f-a5d8-5d37942d4769/04-screen-space-quality-1.png) ![Quality level 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40ba9dcc-a55a-4555-96c8-4e46f791a386/05-screen-space-quality-2.png) ![Quality level 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5d4b18c-4e2c-4753-aeda-cf2e3f024a79/06-screen-space-quality-3.png) ![Quality level 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d7c6ca1-b431-4b8d-a4c2-7bc74b7c3955/07-screen-space-quality-4.png)

**Dragging the slider shows SSGI's quality levels from 1 to 4.**

-   **1 -** Ray Steps: 8; Ray Count: 4
-   **2 -** Ray Steps: 8; Ray Count: 8
-   **3 -** Ray Steps: 8; Ray Count: 16
-   **4 -** Ray Steps: 12; Ray Count: 32

### Additional Console Commands

You can also use the following commands to control SSGI:

-   The HalfRes command to render SSGI at half resolution.
    
    ```
              `r.SSGI.HalfRes`
    		
    Copy full snippet
    ```
    r.SSGI.HalfRes
-   The Leak Free Project uses previous frame's scene color to achieve better quality results.
    
    ```
              `r.SSGI.MinimumLuminance`
    		
    Copy full snippet
    ```
    r.SSGI.MinimumLuminance

## Additional Notes

-   **Large occluders and fallback techniques, such as precomputed lighting.**
    
    SSGI, like other screen space effects, is best used in conjunction with other indirect lighting techniques, such as [precomputed lighting from lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine). When you have large objects that block portions of the screen, SSGI becomes apparent when it's being used as the sole indirect lighting illumination for the scene. For example, using baked lighting reduces screen space artifacts when transitioning behind a large occluder where a bright object may be located. SSGI is recommended as a means to improve indirect lighting illumination in your scene but not as a sole indirect lighting method.