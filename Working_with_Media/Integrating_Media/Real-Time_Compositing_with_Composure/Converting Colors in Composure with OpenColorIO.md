# Converting Colors in Composure with OpenColorIO

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/converting-colors-in-composure-with-opencolorio-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/converting-colors-in-composure-with-opencolorio-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:06

---

This page explains how to apply [OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) (**OCIO**) color conversions to input and output media in [Composure](/documentation/en-us/unreal-engine/real-time-compositing-with-composure-in-unreal-engine).

## Prerequisites

You must set up the following in your project to complete the sections below:

-   An **OpenColorIO Configuration Asset**. Refer to the [OpenColorIO Quick Start](/documentation/en-us/unreal-engine/opencolorio-quick-start-for-unreal-engine) for steps on creating this Asset.
    
-   A **Composure Element** set up with a valid **Media Source** and an **Output**. Refer to the [Real-Time Compositing Quick Start](/documentation/en-us/unreal-engine/real-time-compositing-quick-start-for-unreal-engine) for steps on setting these up.
    

## Converting a Media Element in Composure

This procedure shows how to create a new **Transform Pass** for a Composure Element, and set up that Transform Pass to convert the color space of the Element's media source from one color profile to another.

1.  In the **Outliner**, select your **Composure Element** to open its **Details** panel.
    
2.  In the **Details** panel under the **Composure > Transform/Compositing Passes** section, click **Add (+)** to add a new Transform Pass entry.
    
    ![Add New Transform Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4534c063-21d4-49b4-975f-eb48e5c025c6/add-new-transform-pass.png)
3.  In the settings for your new **Transform Pass**, open the **dropdown menu** and select **OpenColorIO Pass** from the list.
    
    ![Set Transform Pass to OpenColorIO Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b070838-691a-4a32-8743-e8d82fcb1cab/set-opencolorio-pass.png)
4.  Expand the settings for your **Transform Pass**, then expand its **Color Conversion Settings**.
    
    ![Expand Color Conversion Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36283f87-a74a-4ae0-99fa-44909c2d9576/expand-color-conversion-settings.png)
5.  Under Color Conversion Settings:
    
    1.  Set the **Configuration Source** parameter to point to your **OpenColorIO Configuration Asset**.
        
    2.  Set the **Source Color Space** parameter to the color profile you want to convert from. This is typically the color space that the media source was originally captured in.
        
    3.  Set the **Destination Color Space** parameter to the color profile you want to convert to. Typically you will want to use the **linear** color space so your media matches the linear color space used in Unreal Engine.
        
    4.  Toggle the **Enabled** setting on.
        
    
    ![Set Color Conversion Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aa45dca-0ca7-4040-8697-b566651ce843/set-color-conversion-settings.png)
6.  As soon as you set up the source and destination color spaces for your Transform Pass, the colors in your Media Source change in the Composure Element's Preview and in the Level Viewport.
    

## Converting Media Output in Composure

This procedure shows how to set up an output from Composure with a new Color Correction pass that converts the colors of the composited media from one OCIO color profile to another.

1.  In the **Outliner**, select your **Composure Element** to open its **Details** panel.
    
2.  In the **Details** panel under **Composure > Output**, expand your **Output Pass**.
    
    ![Expand Output Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3c493aa-2dce-4717-8c63-a5e17cc0134c/expand-output-pass.png)
3.  In the settings for your new **Output Pass**, open the **dropdown menu** and select **OpenColorIO Pass** from the list.
    
    ![Set Output Pass to OpenColoriO Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/222d6f1d-2259-4847-9ab9-041735c2f2e9/set-opencolorio-output-pass.png)
4.  Expand the **Color Conversion** **Settings** for the **Output Pass**. Under Color Conversion Settings:
    
    1.  Set the **Configuration Source** parameter to point to your **OpenColorIO Configuration Asset**.
        
    2.  Set the **Source Color Space** parameter to the color profile you want to convert from. Typically you will want to use the **linear** color space so your media matches the linear color space used in Unreal Engine.
        
    3.  Set the **Destination Color Space** parameter to the color profile you want to convert to. Typically you will want to match the color space used by the monitor to display the result, or another destination color space that you want.
        
    4.  Toggle the **Enabled** setting on.
        
    
    ![Set Color Conversion Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69bd4e0a-214e-4277-8db4-2eed259e94a3/set-color-conversion-settings.png)
5.  When you display your composited media, the colors are changed.