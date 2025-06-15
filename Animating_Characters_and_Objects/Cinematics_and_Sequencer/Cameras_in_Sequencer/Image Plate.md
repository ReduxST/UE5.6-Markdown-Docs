# Image Plate

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/full-screen-movies-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/full-screen-movies-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:28

---

The **Image Plate Actor** supports the playback of movies and image sequences from a plate attached to the frustum of a **[Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)**. Using these image plates, you can playback full-screen videos and image sequences, as well as including foreground elements within the camera's perspective.

#### Prerequisites

-   The Image Plate plugin must be enabled prior to use. Navigate in the Unreal Engine menu to **Edit > Plugins**, locate **Image Plate** in the **Rendering** section, and enable it. You may need to restart the editor for this change to come into effect.
    
    ![image plate plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3d309ec-4ca2-417f-9f05-a62fcb7f53ca/plugin.png)
    
-   You are familiar with **[how to set up a video asset for playback](/documentation/en-us/unreal-engine/play-a-video-file-in-unreal-engine)**, or **[how to set up image sequences for playback](/documentation/en-us/unreal-engine/play-an-image-sequence-in-unreal-engine)**.
-   You are familiar with the usage of the **[Media Track](/documentation/en-us/unreal-engine/cinematic-movie-media-track-in-unreal-engine)**.
-   You are familiar with the basics of **[Materials](/documentation/en-us/unreal-engine/unreal-engine-materials)**.
-   You have an understanding of **[Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)** and its **[Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine)**.

## Creation

To fully set up the Image Plate Actor, you will need to add both a **[Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)** and an **Image Plate Actor** to a Level, then attach the plate to the Cine Camera Actor.

First, add a Cine Camera Actor to your Level by navigating to the **Cinematic** tab in the **[Place Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine)** panel, and locate **Cine Camera Actor**. Drag it from the panel and into your viewport.

![create cine camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7ccf323-5c7f-47e0-9f6e-1e2d0b68e165/createcam.png)

Next, add an **Image Plate** to your Level by dragging it from the **Place Actors** panel.

![create image plate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab270fba-039f-47be-a1ee-ddfc140cb0c5/createplate.png)

After both Actors have been added to your Level, attach the plate to the camera by dragging it onto the camera in the [World Outliner](/documentation/en-us/unreal-engine/outliner-in-unreal-engine) panel. Once that is done, the Image Plate will snap to the front of the camera and resize to fit its view frustum.

![attach image plate to camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/180ba7ee-3621-4911-9eb8-dc75a9e1058c/attachplate.gif)

## Behavior

By default, the Image Plate will automatically adjust its size to fit the Cine Camera Actor's [**Sensor Dimensions**](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#properties), ensuring it will always be fully in the camera's view.

![image plate sensor size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19aa1155-8ee7-48fe-8c33-5cd807ceb197/sensorsize.gif)

You can also move the plate toward and away from the camera to control the spacing between the plate and the camera. This spacing will allow more foreground elements to be included in the camera's view. The plate will also dynamically adjust its scale to ensure it will remain fully in view.

![move image plate foreground](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb427553-5b9c-43d5-aab3-b45ea8c8aee8/moveplate.gif)

When **Piloting** the camera, the image plate will fill the screen and will stretch to conform to the camera's aspect ratio. You may also need to adjust your camera's focus distance to match the plate distance to ensure it remains in focus.

![image plate viewport view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8ae2d28-35ea-4f01-9746-1136efac7975/pilotview.png)

### Properties

Selecting the Image Plate Actor will reveal its details in the Details panel.

![image plate details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e80f5b5-5997-43af-aeda-904216d789aa/properties.png)

The **Fill Screen** property enables automatic plate sizing to fit the camera's full view. When this is disabled, you can instead use the **Fixed Size** property to manually set the plate's size.

![image plate fill screen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79ac7e40-92bd-433b-b627-650cc68019c3/fillscreen.png)

If **Fill Screen** is enabled, then you can use the **Fill Screen Amount** property to offset the plate's size as a percentage of the screen. **X** controls the percentage of the **width** of the screen, and **Y** controls the **height**.

![image plate screen space size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c15620f4-b534-400d-9cf6-0324496b036d/fillamount.png)

### Material

Expanding the advanced section of the **Image Plate Details** will reveal its **[Material](/documentation/404)** properties. You can adjust the default material or texture here.

![image plate material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46f5220d-869c-4171-8152-01066b8182eb/materialproperties.png)

## Material Setup

Regardless of if you are displaying an image sequence or a video on your plate, you will need to create a new **Material** that references a **Media Texture**. The Media Texture must also reference a **Media Player**.

### Media Texture and Player

First, create the **Media Player** by clicking **Add/Import** in the **[Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine)**, navigating to the **Media** category, and selecting the **Media Player** asset. Once selected, a dialog window will appear. Ensure that **Video output MediaTexture asset** is enabled, and click **OK**.

![create media player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dd9f7d7-c604-4423-9508-505a71a313d5/createmediaplayer.png)

Doing this will ensure that both a **Media Texture** and **Media Player** are created and linked.

![media texture link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44900685-688a-445a-8230-8cecf4227d7b/mediatexture.png)

### Material Graph

Create a new **Material** asset by clicking Add/Import in the Content Browser, and selecting **Material**. Once it is created and opened, set the **Shading Model** to **Unlit**, and enable the **Two Sided** property in its details. This is done so that the image plate is not affected by any lighting in the Level.

![image plate material unlit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92fcc8f4-552e-49af-80d8-be9c088363fc/materialsetup.png)

Drag the **Media Texture** asset into the material graph and connect its **RGB** pin to the material's **Emissive Color** input pin.

![image plate media texture material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/856c5ef5-7580-41d0-ab55-7181807d257b/materialgraph.png)

Lastly, you will need to assign the media material to the **Material** property of the Image Plate Actor.

![image plate assign material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fd2caa5-cd04-4dd2-afa7-0c62956c69e9/assignmaterial.png)

## Playback

Videos and image sequences can be played on the image plate through Sequencer's **[Media Track](/documentation/en-us/unreal-engine/cinematic-movie-media-track-in-unreal-engine)**.

### Media Track Setup

Start by creating a new Level Sequence, then click **\+ Track** and select **Media Track**.

![image plate media track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75ac2d6a-a225-4e23-b51a-1aafae581d5a/createmedia.png)

Next select a **File Media Source** (for videos) or **Image Media Source** (for image sequences) asset to play by clicking **\+ Media** and selecting a source. If you do not have one of these assets, refer to their setup instructions in either the **[Video](/documentation/en-us/unreal-engine/play-a-video-file-in-unreal-engine)** or **[Image](/documentation/en-us/unreal-engine/play-an-image-sequence-in-unreal-engine)** playback documents.

![media track add media](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45815e46-9168-4022-9ffb-bf2df30335fd/mediaselector.png)

Right-click the media section, navigate to its properties category, and assign your media texture to the **Media Texture** property.

![assign media texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aadbaf2a-ffd3-4573-84c3-bd462771eba1/assignmediatex.png)

### Examples

Once finished, you will be able to play your sequence and preview the video or image sequence displayed on your image plate.

![image plate video](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bba3f4b3-bdb9-4382-ba23-b4519e05e10b/videoexample.gif)

Video Example

![image plate image sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e7ef7a0-4e3e-4c45-a65d-5a3f26e1d111/imagesequenceexample.gif)

Image Sequence Example