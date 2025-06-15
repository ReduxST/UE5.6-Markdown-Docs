# Animation Compression

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-compression-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-compression-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:57

---

When creating animation systems in **Unreal Engine**, Animation Compression is the process of transforming animation data from Animation Sequence assets, in order to lower your animation system's overall file sizes and memory cost. Using animation compression, you can see significant improvements across your project's performance, especially when scaling projects across multiple hardware targets of varying power.

You can use this document to learn more about **Animation Compression** in Unreal Engine.

## Overview

Generally speaking, animations with minimal movement can benefit greatly from animation compression, with little impact on the overall quality of the animations, while animations with a lot of movement undergo a more significant reduction in quality. When approaching animation compression its important to tailor the kind of compression you implement, based on the type of quality loss your project can afford.

In Unreal Engine there are two data assets that are used to apply compression to Animation Sequences, the **Bone Compression Settings** and **Curve Compression Settings** assets. Using these assets, you can apply **compression codecs** which will test different methods of compression, seeking the optimal balance between quality loss and file size reduction, and only appling the best result.

![compression settings assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/749047f1-5a29-4c94-a60d-69a13a78436c/assets.png)

Unreal Engine comes pre-packaged with a set of general use Compression Settings assets, that you can use on your project's Animation Sequences. These default assets can be found in the **Engine** > **Content** > **Animation** folder.

![default compression settings assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dc3982a-e77e-42df-baed-5444eda76b8a/defaultassets.png)

Optionally, you can create your own Compression Assets, for more control over how you compress your animations. To create an Animation Compression Settings asset, use (**+**) **Add** in the **Content Browser**, navigate to **Animation** > **Advanced** and select either the **Bone** or **Curve Compression Settings** asset.

![create compression settings assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f3d71e1-a80d-4bd4-ab58-857e939f487d/createassets.png)

To apply compression to an animation in Unreal Engine, you can assign a Compression Settings asset to an Animation Sequence, using the **Compression Settings** properties in the [Animation Sequence Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine)'s **Asset Details** panel.

![set compression settings assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/083f5cdc-b505-4fc3-b57c-f4fd690a2bc2/setassets.png)

By changing the Compression Settings asset registered to an Animation Sequence, the new compression settings will be applied automatically. Compression is also automatically applied during load if the Compression Settings have changed since the asset was last compressed, if the [Derived Data Cache](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) (DDC) notices a new Compression Settings asset registered to an Animation Sequence, or during a cook.

When changing a Compression Codec's properties, compression will not be automatically applied, as the asset could be assigned to many assets. To manually compress all assets that are registered with a specific Animation Settings asset, you can use the **Compress** button in the Compression Settings asset's **Toolbar**.

![compress button toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c7178d5-a9cb-41ef-a6ae-e968f7d24704/compressbutton.png)

After clicking the Compress button, a dialogue box will appear, prompting you to confirm the total number of assets that will be compressed.

## Bone Compression

Bone Compression is used to reduce the amount of data the Animation Sequence asset contains about the Skeletons movement. Bone Compression codecs look to optimize animation data on specific bones that experience no or small movements between keys, where techniques such as interpolation will suffice.

After creating and assigning the Bone Compression Settings asset to an Animation Sequence, you can double click the Bone Compression Settings asset to access its properties where you can select and tailor different methods of compressing your animation's skeletal motion data.

![bone compression settings properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c84bcac9-00e9-410f-9ac9-752aeedef2b3/bonesettings.png)

| Property | Description |
| --- | --- |
| **Codecs** | 
Here you can define a list of animation bone compression codes to try. To add a new Codec array, use **Add** (**+**) in the **Codecs** property. After adding a codec, additional properties will populate the field, relevant to the codec you have selected.

Empty entries in the list are ignored when running bone compression on the animation sequence. However, the list must contain at least one codec in order to compress bone data.

For a detailed description of each available codec, and a description of their additional properties, see the [Bone Compression Codec Reference](/documentation/en-us/unreal-engine/animation-compression-codec-reference-in-unreal-engine#bonecompressioncodecreference) documentation.



 |
| **Error Threshold** | When compressing, the best codec below this error threshold will be used. Value of `.1` is the default value. |
| **Force Below Threshold** | When enabled, any codec, even one that may increase the file size of an Animation Sequence, with a lower error will be used, until it falls below the threshold. |

## Curve Compression

Curve Compression is used to compress the Animation Sequence's curve data. Curve Compression codecs look to reduce curve data by optimizing data using a variety of methods that target values with little or no changes between keys, where techniques such as interpolation will suffice.

After creating and assigning a Curve Compression Settings asset to an Animation Sequence, you can double-click the Curve Compression Settings asset to access its properties where you can select and tailor different methods of compressing your animation's curve data.

![curve compression settings assets properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b3e64a2-a7f2-43f8-9b6b-47b36ea2adf6/curvesettings.png)

| Property | Description |
| --- | --- |
| **Codec** | 
Here you can define a curve compression codec. To set a Codec array, use the drop-down menu to select a codec. After adding a codec, additional properties will populate the field, relevant to the codec you have selected.

Empty entries in the list are ignored when running bone compression on the animation sequence. However, the asset must contain a codec in order to compress curve data.

For a detailed description of each available codec, and a description of their additional properties, see the [Curve Compression Codec Reference](/documentation/en-us/unreal-engine/animation-compression-codec-reference-in-unreal-engine#curvecompressioncodecreference) documentaion.



 |
| **Max Curve Error** | Set the maximum error threshold allowed when compressing **Rich Curves**. By default this value is `0`. |
| **Use Anim Sequence Sample Rate** | When enabled, the **Error Sample Rate** property's value will be used to determine the Animation Sequence's sample rate during compression. |
| **Error Sample Rate** | When the **Use Anim Sequence Sample Rate** property is enabled, the Animation Sequence will use this property's defined value as the sample rate to use when measuring the curve error. By default this value is `60`. |

## Compression Codecs

For a reference about all of the Bone and Curve Compreesion Codecs in Unreal Engine, see the [Animation Compression Codec Reference](/documentation/en-us/unreal-engine/animation-compression-codec-reference-in-unreal-engine) documentation.