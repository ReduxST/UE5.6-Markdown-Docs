# Compositing Elements Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/compositing-elements-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/compositing-elements-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:14:41

---

Elements are the individual building blocks used to construct a composite. Each Element represents either a layer of a comp, or the comp itself. They are level actors individually responsible for rendering a piece of the composited scene.

![Composure Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2f3f9c4-3e5e-4b16-8b82-b402751028c1/ue5_01-composure-window.png "Composure Window")

There are many different Element types. All of which, you can configure and change. Elements are Blueprintable, and you can create your own custom Elements inheriting from by `ACompositingElement` (or its sub-classes).

## Basic Compositing Elements

### Empty Comp Shot

This acts as the starting point for most comps. It doesn't contain any Passes, and requires the user to fill it out.

![Empty Comp Shot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5982b0c1-6d52-4a36-b664-ca062d5ef250/ue5_02-empty-comp-shot.png "Empty Comp Shot")

### Media Plate Element

This preset Element comes with all the Passes needed to pipe a video into the compositing system, and apply **Chroma Keying** on top of it.

![Media Plate Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/178d489d-abf4-4ed3-8a83-b6e5aeba608c/ue5_03-new-media-plate.png "Media Plate Element") ![Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/983f85ed-3500-4efe-8464-744e383fabfa/ue5_04-composure-details.png "Details panel")

### CG Layer Element

This preset Element is responsible for rendering actor objects from the virtual scene. Use the **Capture Actors** property to specify which actors you want to include/exclude.

![CG Layer Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da2d969a-06a0-402b-8d7b-f4a80217795b/ue5_05-cg-layer.png "CG Layer Element") ![Capture Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dafc890-696e-4acb-864d-2007626dd700/ue5_06-capture-actors.png "Capture Actors")

### CG Matte Element

This Element is like a plain **CG Layer** Element, but it renders the CG objects into a black/white mask texture. This is helpful for garbage matting, or setting up a holdout mask to be used with a keyer.

![CG Matte Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38c8b2cd-a57b-49ea-b909-b1c330b41ae2/ue5_07-add-cg-matte.png "CG Matte Element") ![Matte Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d05b58ce-c453-4829-9871-da1701f6f7da/ue5_08-matte-type-holdout.png "Matte Type")

Change the Element's **Matte Type** property to invert the mask.

## Advanced Element Types

The Advanced Elements are available via the **All Classes** toggle in the **New Element** dialog. These additional Elements were created via Blueprints, and can be modified to suit specific use cases.

For the Advanced Elements to be listed, your first have to load their respective Blueprints. You can find the Advanced Element Blueprints in the content browser under the Composure Plugin's Blueprints/CompositingElements folder (make sure your content browser is set to view Engine and Plugin content).

### Texture Element

This Element is a utility Element for introducing an external texture into the compositing system.

![Texture Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c36c664-ec7b-4dc2-b9c1-0f34d81f7df6/ue5_09-black-exr-texture.png "Texture Element")

### Depth Element

The Depth Element is similar to the CG Layer element, but produces an image which expresses the depth of the included actors.

![Depth Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffdd5deb-c6c8-4d15-a124-92b44032907e/ue5_10-bp-depth-comp-element.png "Depth Element") ![Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f53257a-87f3-4eba-b4ba-23e22dcbbd60/ue5_11-composting-element-material-pass.png "Details panel")

### Radial Element

![Radial Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa8a30a9-b1b8-4924-a655-f87294b54a77/ue5_12-bp-radiall-comp-element.png "Radial Element") ![Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99a3dc4c-4682-4cec-9f54-52040c07575b/ue5_13-m-radial-details-panel.png "Details panel")

### Ramp Element

![Ramp Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08b6d4c6-a775-4b9c-84bf-eda1d54582f0/ue5_14-bp-ramp-comp-element.png "Ramp Element") ![Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4a0c2fa-4dbe-411b-a3ab-8fbd97c7f385/ue5_15-ramp-element-details.png "Details panel")

### Roto Paint Element

![Roto Paint Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e58ca3c-6ed5-49ab-9949-5b73a78cab0f/ue5_roto.gif "Roto Paint Element") ![Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ff72f12-3d78-4d51-ad53-565f1ffd2af8/ue5_16-composure-media-plate.png "Details panel")