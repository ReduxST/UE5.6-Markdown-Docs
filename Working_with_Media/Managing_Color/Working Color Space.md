# Working Color Space

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-color-space-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-color-space-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:30

---

Working Color Space lets you define the color space of the Unreal Engine(UE) Renderer. You can change the color space of the UE Renderer if you are working with textures created in a different color space, or to work in a specific color space for the display you are using.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/506fb3b5-8d5d-43a6-b297-8427fd4957d0/workingcolorspacewindow.png)

Unreal Engine defaults to sRBG/REC709 but you can choose to use another color space from the provided list, or you can define a custom color space using chromaticity coordinates.

To adjust the Working Color Space:

1.  Navigate to **Edt > Project Settings > Rendering > Working Color Space.**
    
2.  Select the Working Color Space dropdown and choose the color space you want to use for your project.
    

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90f4d2b9-727f-4f67-b556-52ec13f4d36f/workingcolorspaceselect.png)

Unreal Engine supports the following color spaces:

| **Color Space** | **Description** |
| --- | --- |
| sRGB / Rec709 | sRGB / Rec uses the parameter values for the HDTV standards for production and international programme exchange from the International Telecommunication Union (ITU). |

For more information, refer to the [ITU parameter values](https://www.itu.int/rec/R-REC-BT.709/en) |

<table class="table" style="--columns-count: 2;"><tbody><tr><td>Rec2020</td><td>Rec2020 uses the<strong> </strong>parameter values for ultra-high definition television systems for production and international programme exchange from the ITU.</td></tr></tbody></table>

For more information, refer to the [ITU parameter values](https://www.itu.int/rec/R-REC-BT.2020-0-201208-S/en) |

<table class="table" style="--columns-count: 2;"><tbody><tr><td>ACES AP0</td><td>For more information about the ACES color spaces, refer to the <a href="https://docs.acescentral.com/">Academy Color Encoding Specification documentation</a></td></tr><tr><td>ACES AP1 / ACEScg</td><td>&nbsp;</td></tr><tr><td>P3DCI</td><td>For more information about the P3DCI color space, refer to the <a href="https://www.color.org/chardata/rgb/DCIP3.xalter">International Color Consortium website</a></td></tr><tr><td>P3D65</td><td>For more information about the P3DCI color space, refer to the <a href="https://www.color.org/chardata/rgb/DCIP3.xalter">International Color Consortium website</a></td></tr><tr><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>Custom</td><td>To use a custom color space, enter the Red, Green, Blue and White Chromaticity coordinate values that you want to use for your custom color space.</td></tr></tbody></table>

## Texture Settings: Input Conversions

-   (Advanced) Source Color Settings
    
    -   Color Space
        
        -   When the Color Space is set to None (default), no conversions are applied.
            
        -   When the Color Space is manually specified, conversions to the working color space are automatically applied when the texture is serialized. If the working color space is changed, textures are automatically re-serialized with the updated conversion.
            
    -   Encoding Override
        
        -   Source encoding of the texture, exposing more options than just sRGB.
            
        -   *Note: This differs from the sRGB checkbox, which specifies the stored encoding of the texture resource in the engine.*
            

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6d67b32-2054-4016-90aa-032df949c3ec/workingcolorspacesettings.png)