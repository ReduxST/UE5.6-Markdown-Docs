# Compositing Passes Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/compositing-passes-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/compositing-passes-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:14:44

---

A Compositing Pass is an object belonging to a compositing Element. Passes are individual steps that are executed when rendering the Element, and are run in sequential order.

There are three compositing pass types:

-   Inputs
    
-   Transforms
    
-   Outputs
    

![Compositing Pass Types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f82ad8a9-07b6-4add-91bd-63fe57514d95/01-composure-refrences.png "Compositing Pass Types")

Most Passes are responsible for rendering an image. For Inputs and Transforms, those images are available to subsequent passes and can be referenced in rendering materials.

## Blueprintable

Passes are Blueprintable, so you can easily create your own Pass and use it with the compositing system. Just create a Blueprint and inherit from **CompositingElementInput**, **CompositingElementTransform**, or **CompositingElementOutput**.

## Shared Settings

Each Pass has its own set of properties, but every Pass shares the below properties:

| Property | Description |
| --- | --- |
| **Enabled** | Like Elements, individual Passes can be disabled. When turned off, the Element behaves as if the Pass is not there. |
| **Pass Name** | Passes have names so that they can be referenced by other subsequent Passes. A Pass must be uniquely named if you want to reference it in a render material. |
| **Intermediate** | For each render Pass, a render target is allocated. By default, it assumes that you only need that result through the next Pass. After that, to save on render resources, it releases its render target so it can be used by another pass. If you need the Pass's result to be accessible longer, uncheck this box. |

## Inputs

### Media Texture Compositing Input

This Pass is responsible for routing video into the compositing system. It requires a media texture to reference. Its Media Source is processed through the Pass's Material.

![Media Texture Compositing Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7b167c5-918b-464e-b372-ba5437c56e03/02-media-texture-compositing-input.png "Media Texture Compositing Input")

Without a **Media Source**, the media Pass will be blank. However, you can set up a default still image in your game config file: `[/Script/Composure.ComposureGameSettings] StaticVideoPlateDebugImage="/Game/Path/To/My/TextureAsset"`

### Texture Input

This Pass provides you with an easy way to source static textures into the compositing system.

![Texture Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b2f2d6b-f38f-4e2f-b33d-0c6ad1542f7b/03-texture-input.png "Texture Input")

## Transforms

Transforms are responsible for taking input image(s) and spitting out a processed image. Traditionally, this is where compositing is done – a Material Pass that references sub-Elements, combining them.

### Compositing Element Material Pass

This Pass lets the user author a custom material, in which they can reference other Elements/Passes. This is the bread-and-butter of the compositing system.

![Compositing Element Material Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20cbbede-a1ea-4269-a1da-fb79ce85ca4c/04-compositing-element-material-pass.png "Compositing Element Material Pass.png")

### Compositing Post Process Pass

This Pass applies a set of post processing effects on the previous Pass (inoperable if it's the first pass).

![Compositing Post Process Pass ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09d38a08-a3f3-4c96-bb67-22f3cd980328/05-compositing-post-process-past.png "Compositing Post Process Pass")

Only certain effects are available (Bloom and Tonemapping). Users can create more effects by creating a sub-class of **ComposurePostProcessPassPolicy**.

### Compositing Tonemap Pass

This Pass applies finishing post-process tonemapping on the previous Pass.

![Compositing Tonemap Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8a2a4a1-621b-46da-b821-e15667379f1a/06-compositing-tonemap-pass.png "Compositing Tonemap Pass")

This is helpful for converting images back from linear color space. It is useful as a preview transform, or on an output Pass (intermediate material operations expect linear colors).

### Multi Pass Chroma Keyer

This Pass is used by the **Media Plate Element** to key an image. The **Key Colors** property specifies the color(s) to turn transparent.

![Multi Pass Chroma Keyer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0589bcb7-fc15-4d75-803a-6db43c92440c/07-multi-pass-chroma-keyer.png "Multi Pass Chroma Keyer")

If needed, you can switch out the material for your own chroma keyer using the parameters listed in the **Required Material Parameters** field.

This Pass runs multiple times, once for each key color.

### Multi Pass Despill

This Pass removes chroma bounce from the image ("spill" from the green screen).

![Multi Pass Despill](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1644450e-3b08-42ea-b92d-3c731fc14be8/08-multi-pass-despill.png "Multi Pass Despill.png")

Much like the **Chroma Keyer Pass**, you specify **Key Colors** that you want removed. Also like the **Chroma Keyer Pass**, this Pass runs multiple times – once for each key. You can switch out the material for your own despill process (it just requires the parameters listed in the "Required Material Parameters" field).

You can find information on chroma keying and despill in UE4 in [this blog post](https://www.unrealengine.com/en-US/blog/setting-up-a-chroma-key-material-in-ue4).

### OpenColorIO Pass

This Pass is used to apply a color conversion (color space transform) onto the input image pixel colors.

![OpenColorIO Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6aa8d128-49b1-4445-851a-c261f45cc260/09-open-color-io-pass.png "OpenColorIO Pass")

## Outputs

Output passes define a destination for the Element's fully processed image to be broadcast to. Some outputs perform a transform of their own before routing the image.

### Compositing Media Capture Output

This Pass routes the Element's result to a media capture target. The **Capture Output** field expects a media output asset, which is a configuration file detailing where to route the image to (capture card, port ID, pixel format etc.). 

![Compositing Media Capture Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28071a7d-d063-43e4-aa58-ebc3226ff9b4/10-compositing-media-capture-output.png "Compositing Media Capture Output")

This Pass has a **Color Conversion** transform associated with it, that runs prior to outputting the image.

### EXRFile Compositing Output

This Pass will save a .EXR image file to your hard drive for each frame the Element renders.

![EXRFile Compositing Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2397467b-4625-4993-883f-d0acd43ffd3d/11-exrfile-compositing-output.png "EXRFile Compositing Output")

This Pass will start writing out images (one for each frame) as soon as it has an **Output Directory**. For more control, disable the Pass first.

### Player Viewport Compositing Output

Use this Pass to take over the player's viewport in game, and replace the display with the Element's result.

![Player Viewport Compositing Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed7b4cee-97b1-42b3-96e1-51b2e99ed68a/12-player-viewport-compositing-output.png "Player Viewport Compositing Output")

This Pass has a **Color Conversion** transform associated with it that it runs before displaying the image. Play in Editor to see it in action.

### Render Target Compositing Output

This Pass will write the Element's result to a render target.

![Render Target Compositing Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dbab018-d828-44e6-933c-58840eef5d32/13-render-target-compositing-output.png "Render Target Compositing Output")

Use the **Render Target** field to specify which asset.