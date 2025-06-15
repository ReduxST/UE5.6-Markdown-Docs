# Refraction Using Pixel Normal Offset

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/refraction-using-pixel-normal-offset-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/refraction-using-pixel-normal-offset-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:19

---

By default, Unreal Engine uses a physically based refraction model derived from **Index of Refraction** values. The physical **Index of Refraction** model mimics the way light rays refract as they transfer between mediums. This works well for small objects, like jars, glasses, and other curved surfaces. However, when used with large flat surfaces it can produce unpredictable results and artifacts as the scene color is being read from off screen.

**Pixel Normal Offset** is an alternative Refraction Mode available in the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide). It uses the vertex normal as a reference and then computes the refraction offset by calculating how different the per-pixel normal is from the vertex normal. This is useful for large flat surfaces, like water, where you do not want a constant offset that is reading data from off screen.

## Physical vs Non-Physical Refraction Model

You can change the **Refraction Mode** of your Material in the Details Panel. Scroll down and expand the **Refraction** section, and then choose between the two options in the Refraction Mode drop-down. All Materials use **Index of Refraction** by default.

For additional information about the physical model of refraction, and how to use it in your Materials, you can read the page on [Using Refraction](/documentation/en-us/unreal-engine/using-refraction-in-unreal-engine).

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/907556ad-fd20-41bb-adb4-ad5be3d4435c/refraction-mode-ior.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fa141e4-ed75-4d51-9402-7ed5f8b3530c/refraction-mode-pno.png) |
| Physical Refraction Model: Index of Refraction | Non-Physical Refraction Model: Pixel Normal Offset |

The comparisons below demonstrate the differences in how the normal is read in the Material when the Refraction Mode is changed from **Index of Refraction** to **Pixel Normal Offset.**

![Refraction Mode: Index of Refraction without Normal Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a19cab2-4763-4e0f-8266-944aab3352f5/ior_withoutnormals.png)

![Refraction Mode: Pixel Normal Offset without Normal Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a594a3eb-fdc1-4418-82fb-1642c9a298df/pno_withoutnormals.png)

Above you will notice that the image is shifted when using the **Index of Refraction** mode compared to the **Pixel Normal Offset** mode where you do not read from off screen so much. Note that **Index of Refraction** will work without a Normal map plugged into the Material, whereas with **Pixel Normal Offset**, if there is no Normal map you will not get any refraction.

![Refraction Mode: Index of Refraction with Normal Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1f0143c-5a07-47bc-b8c2-950c53ebb616/ior_withnormals.png)

![Refraction Mode: Pixel Normal Offset with Normal Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aef32af9-3225-470e-974c-7813f491f628/pno_withnormals.png)

When you add a Normal map to your Material with a value greater than 1 plugged into the Refraction input, the normal will translate along the surface when using **Pixel Normal Offset**. However, you will notice that with **Index of Refraction**, you will still have an offset that reads from off screen, which is not a desirable effect for flat surfaces using refraction.

### Final Result

In this example, the refraction amount is adjusted between a value of 1.0, which is no refraction at all, to a value of 2.0, for some refraction along the surface without shifting the image while using **Pixel Normal Offset**.

## Pixel Normal Offset and Glass

Pixel Normal Offset is also beneficial for large flat glass surfaces, such as the windows in the cafe scene below. The first image in the slider uses the default **Index of Refraction** setting. The window refraction is chaotic and contains an artifact in the bottom right corner. When the refraction mode is changed to **Pixel Normal Offset,** the windows appear much more true to life and the artifact disappears.

 ![Cafe glass with IOR](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/205714df-3219-4e35-8846-971172b25a12/bistro-glass-ior.png) ![Cafe glass with Pixel Normal Offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4c47528-f8c0-4c36-abcd-8f95f0fcf53b/bistro-glass-pixel-normal-offset.png)

**Move the slider to see how the glass changes when the Refraction Mode is changed from Index of Refraction (image 1) to Pixel Normal Offset (image 2).**

In **Pixel Normal Offset** mode, the refraction in this example is extremely slight because the normal map for this glass only contains micro abrasions and minor surface imperfections. This is an expected result for clean architectural glass.

However if you wanted a textured or patterned glass effect you could use a more representative normal map and raise the **Refraction** value to something around **1.52**.

This is how the normal map affects the refraction in the glass windows.