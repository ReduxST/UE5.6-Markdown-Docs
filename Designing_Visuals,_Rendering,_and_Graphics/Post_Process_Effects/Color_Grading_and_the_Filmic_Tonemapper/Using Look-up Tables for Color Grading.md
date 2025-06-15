# Using Look-up Tables for Color Grading

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lookup-tables-for-color-grading-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lookup-tables-for-color-grading-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:41

---

A **Lookup Table** (LUT) can be used to achieve color correction using a Post Process Volume. Instead of using three one-dimensional (1D) lookup tables, a single three-dimensional (3D) Lookup Table is used. This offers more sophisticated color transformation, which can be used for something like desaturation.

|  |  |
| --- | --- |
| 
[![Neutral LUT](https://dev.epicgames.com/community/api/documentation/image/f467cf98-2bde-4f48-add4-f2f9ce4630a6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f467cf98-2bde-4f48-add4-f2f9ce4630a6?resizing_type=fit)



 | 

[![Sepia Tone LUT](https://dev.epicgames.com/community/api/documentation/image/1784b16a-7a60-49bd-a44e-d84e0d173a80?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1784b16a-7a60-49bd-a44e-d84e0d173a80?resizing_type=fit)



 |
| 

Color Neutral LUT

 | 

Sepia Toned LUT

 |

A Lookup Table used in Unreal Engine is a 16x16x16 color neutral LUT unwrapped to a 256x16 texture. These examples show a color neutral and a sepia toned one. If you were to apply the neutral LUT, you wouldn't see any changes to a default scene, however, if you used the sepia toned one, you'd get something like this:

![Color Neutral LUT](https://dev.epicgames.com/community/api/documentation/image/428a2d4f-497f-4432-97e8-ed0bc1a63580?resizing_type=fit&width=1920&height=1080)

![Sepia Tone LUT](https://dev.epicgames.com/community/api/documentation/image/781f5cef-5515-4c89-88fa-a474ea5e89ab?resizing_type=fit&width=1920&height=1080)

Color Neutral LUT

Sepia Tone LUT

## Using a LUT Texture

To make use of a LUT, use the following properties to assign the LUT texture to the Post Process Volume you want to use it with and adjust its intensity.

| Property | Description |
| --- | --- |
| 
**Color Grading LUT Intensity**

 | 

A scaling factor that controls the effect of the color correction.

 |
| 

**Color Grading LUT**

 | 

The LUT texture to use as a lookup table for color correction. [See below for examples.](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lookup-tables-for-color-grading-in-unreal-engine)

 |

#### Color Grading LUT

|  |  |  |
| --- | --- | --- |
| 
[![Natural Scene](https://dev.epicgames.com/community/api/documentation/image/fe0e5ed2-a78b-473e-88d9-2725cb40920d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fe0e5ed2-a78b-473e-88d9-2725cb40920d?resizing_type=fit)

*Click image for full size.*

 | 

[![Greenish Scene](https://dev.epicgames.com/community/api/documentation/image/709746d3-0f93-46c8-9aab-ff6ebc0fe5c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/709746d3-0f93-46c8-9aab-ff6ebc0fe5c8?resizing_type=fit)

*Click image for full size.*

 | 

[![Reddish Scene](https://dev.epicgames.com/community/api/documentation/image/9a9b475b-90a3-4084-80e0-222503779cd8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a9b475b-90a3-4084-80e0-222503779cd8?resizing_type=fit)

*Click image for full size.*

 |
| 

[![Neutral LUT](https://dev.epicgames.com/community/api/documentation/image/71705a7e-dcd8-48ee-88ac-a58c5c54ce70?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71705a7e-dcd8-48ee-88ac-a58c5c54ce70?resizing_type=fit)



 | 

[![Greenish LUT](https://dev.epicgames.com/community/api/documentation/image/0ef27e52-24fb-4871-8c37-49b7709a7848?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ef27e52-24fb-4871-8c37-49b7709a7848?resizing_type=fit)



 | 

[![Reddish LUT](https://dev.epicgames.com/community/api/documentation/image/61c2d136-c1d4-45d4-b6f7-540fd7fa22f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/61c2d136-c1d4-45d4-b6f7-540fd7fa22f7?resizing_type=fit)



 |

## Creating Your Own LUT Texture

To create your own LUT texture, you'll first need an image editing application (like Photoshop or GIMP) that can make color adjustments to a captured image. For this demonstration, the **Sun Temple** project available in the Epic Games Launcher via the **Learn** tab will be used, and Photoshop will be the application of choice for the LUT image editing. Some terms may be specific to Photoshop in this example.

1.  Start by taking at least one screenshot that is representative of your scene that you want to apply color correction too. You can use the Screenshot Tool available in the Editor to capture a high-resolution image of your scene.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f9427441-7d57-4187-8444-9208af7e8f98?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f9427441-7d57-4187-8444-9208af7e8f98?resizing_type=fit)
    
2.  Open the screenshot in Photoshop and proceed to add your own **Adjustment** layers from the Adjustments tab located above the Layers panel on the right. Here you'll find many different icons that represent the various types of changes you can make to your images, such as brightness and contrast, hue, saturation, and many others.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/07c10562-bae3-4e6b-976f-9956a3b0c6c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/07c10562-bae3-4e6b-976f-9956a3b0c6c8?resizing_type=fit)
    
    *Click image for full size.*
    
3.  From the **Adjustments** panel, click any of the icons to add a layer to the Layers panel. You can use these to make specific color corrections to the final image. For this example, **Vibrance** and **Brightness/Contrasts** have been added and adjusted. Once these are added to your Layers panel, select them from the list to expose their properties, or if these aren't visible, you can right-click and choose **Edit Adjustment** to expose them.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/88d537bd-b398-41c3-b161-689ef3b3739f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/88d537bd-b398-41c3-b161-689ef3b3739f?resizing_type=fit)
    
4.  Any adjustments you make will be visible in the viewport. Adjust the properties of the Adjustment layers until you get the color correction you desire. In the example below, the adjustments for Vibrance and Brightness/Contrast have been adjusted to give the captured screenshot more color saturation and definition for visual appeal.
    
    ![Before](https://dev.epicgames.com/community/api/documentation/image/8ec65f41-4454-40bb-b574-870b2404863e?resizing_type=fit&width=1920&height=1080)
    
    ![After](https://dev.epicgames.com/community/api/documentation/image/2c4c59a6-912f-4cd3-bcc5-be97fcbbd2c2?resizing_type=fit&width=1920&height=1080)
    
    Before
    
    After
    
5.  Now that you've achieved your desired look with the Adjustment layers, you'll need to open a copy of the **Neutral Color LUT** on its own. The adjustment layers that were created for your screenshot can be dragged onto the neutral color LUT.
    
    If you do not have a Neutral Color LUT available to use, you can use the RGBTable16x1.png image shown in the introduction to this page. \* [LUT Texture Example Zip File](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/3e919734-8431-4ed4-bf84-d49c925e2498/neutral-color-lut-example.zip) Right-click and **Save as**.
    
    With your Screenshot with the adjustment layers and the Neutral Color LUT opened, **drag and drop** the Adjustment layers from your Screenshot Layers panel onto the Neutral Color LUT image. You should now see them populate in the LUT's Layer panel.
    
6.  Now, navigate to **File** > **Save As** and give your LUT with the color corrections a name.
    
7.  Import your color corrected LUT into the Editor using the **drag and drop** method into the Content Browser or by using the **Import** button that is also available in the Content Browser.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/6f71b95f-27b1-4779-a983-fb7dc2a15a72?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6f71b95f-27b1-4779-a983-fb7dc2a15a72?resizing_type=fit)
    
8.  For the best results using your LUT in a Post Process Volume, open the LUT image in the Texture Editor and set the following properties:
    
    |  |  |
    | --- | --- |
    | 
    [![](https://dev.epicgames.com/community/api/documentation/image/35f942cb-b672-49b7-b038-714c266d73b5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35f942cb-b672-49b7-b038-714c266d73b5?resizing_type=fit)
    
    
    
     | 
    
    -   Mip Gen Settings: **NoMipMaps**
        
    -   Texture Group: **Color Lookup Table**
        
    
     |
    
9.  Next, in the Post Process Volume, use the **Details** panel and under the **Color Grading** > **Global** section, enable **Color Grading LUT** and apply your LUT.
    
    |  |  |
    | --- | --- |
    | 
    [![](https://dev.epicgames.com/community/api/documentation/image/0d53e1b7-ee09-40bd-8439-36ac6c8fb182?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0d53e1b7-ee09-40bd-8439-36ac6c8fb182?resizing_type=fit)
    
    
    
     | 
    
    ![Default](https://dev.epicgames.com/community/api/documentation/image/41d22da2-d161-4b69-b77d-381e34cfda6d?resizing_type=fit&width=1920&height=1080)
    
    ![With Created LUT](https://dev.epicgames.com/community/api/documentation/image/2239ad24-7987-4533-8ad7-4e43ff75b204?resizing_type=fit&width=1920&height=1080)
    
    Default
    
    With Created LUT
    
    
    
     |
    

## Additional Notes

The following are some things you should be aware of when using LUTs in your projects:

-   Since LUTs happen in Low Dynamic Range (LDR) and on the final image color that was output to the monitor in sRGB space, this means that it's just a snapshot in time for what display support is and will not necessarily look the same on any display its output to, unlike [High Dynamic Range](https://dev.epicgames.com/documentation/en-us/unreal-engine/high-dynamic-range-display-output-in-unreal-engine) (HDR) which is processed so that any color correction happens before tone mapping. For this reason, it is recommended to use the latest [Color Grading](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine) color correction tools available in Unreal Engine 4.16 and later in place of using LUTs.
    
-   LUTs can be a good way to quickly target a particular look for your project on your current display but then you should make final adjustments using the color correction properties found under the **Color Grading** section of the Post Process Volume to guarantee the look is consistent across different types of displays.
    
-   Consistency is lost when using a LUT because any color corrections that have taken place will not work for an HDR display. The color grading properties in the Post Process Volume all operate in what is referred to as **Scene Referred Linear Space**. It means that the colors are consistent because they happen before tone mapping and before they are transformed into a particular display's color space. For example, if you wanted to output to a tv that uses Rec709 instead of sRGB, the color corrections would not carry over if using a LUT since color correction happens after the image has already been output to the display. For this reason, LUTs are being moved away from as a way of doing color correction image processing.