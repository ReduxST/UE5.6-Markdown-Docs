# Camera Shakes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-shakes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-shakes-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:03

---

You can add a camera shake effect to your cameras using Unreal Engine's Camera Shake Blueprints. This guide provides an overview of how to create a **CameraShakeBase** Blueprint, the type of shakes that are available, and how to play them in Sequencer, Blueprints, and Camera Shake Sources.

#### Prerequisites

-   You have an understanding of **[Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)** and know how to **[Create Camera Animation](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine)**.
    
-   You have an understanding of **[Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)**.
    
-   If you are using custom sequence-based shakes, then you must have an understanding of **[Template Sequences](/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine)**.
    
-   If you want to test camera shakes in gameplay, you can create a project using the **[Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine)**.
    

## Camera Shake Creation

To create a shake asset, click **Add/Import** in the **[Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine)** and select **Blueprint Class**. In the next window, locate or search for the **CameraShakeBase** class and click **Select**.

![create camera shake base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e414054-56b2-49c1-a8cc-505a0d8da4ec/createshake.png)

Once the asset is created, name and open it to view the camera shake details.

![shake blueprint details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b0a48d7-5ea0-4696-b775-5f8f6ccaf5bf/openshake.png)

### Details

Camera shake assets have the following base details:

| Name | Description |
| --- | --- |
| **Single Instance** | Enabling this will allow only a single instance of this shake to play at a time. Subsequent attempts to play this shake will restart it, instead of layering it additively. |
| **Root Shake Pattern** | The [**Shake Type**](/documentation/en-us/unreal-engine/camera-shakes-in-unreal-engine#rootshakepatterntypes) to use. |

## Root Shake Pattern Types

Shake patterns control the shape and behavior of the camera shake. You are able to select from the following patterns to create a camera shake.

### Perlin Noise

Perlin generates noise over time by sampling random points based on a specified amplitude and frequency. These points are blended to by using the **[Smootherstep](https://en.wikipedia.org/wiki/Smoothstep)** easing function. Typically, Perlin noise is useful for high-intensity camera shakes such as rumbles or nearby explosions.

![perlin noise graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df0b4ed4-70ca-40b2-bdd2-605d7a85fd7d/perlin.png) ![perlin camera shake example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff620a09-fe81-4a88-83ac-7d621d9cb212/perlinexample.gif)

When you select **Perlin Noise Camera Shake Pattern** for your **Root Shake Pattern**, additional details will appear which you can use to control the Perlin noise shake behavior. It is possible to create a shake effect for the location, rotation, and Field of View (FOV) properties of a camera.

![perlin noise camera shake pattern](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac221de1-dc0c-427c-b010-96ee8a4152ac/perlindetails.png)

Both **Location** and **Rotation** property categories have their individual axes displayed, and you can expand them to reveal the **Amplitude** and **Frequency** properties.

-   **Amplitude** controls the size of the shake pattern. Increasing this will cause the shake on that axis to move a larger distance from the center.
    
-   **Frequency** controls the speed of the shake. Increasing this will cause the shake's movement to appear more rapid.
    

![shake amplitude frequency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42839d84-3904-458b-9455-f01aaa4992ff/axisampfreq.png)

Additionally, you can multiply the combined Amplitude and Frequency results on your Location and Rotation axes by using their **Amplitude** and **Frequency Multiplier** properties. These properties are useful if you want to make global changes to your shake instead of needing to change each individual axis.

![multiply amplitude frequency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ebf5fe33-39af-4be3-9334-fb1b0cdd07e1/perlinmultipliers.png)

The timing of a shake can be controlled by expanding the **Timing** category.

-   **Duration** controls the length of the shake. If it is 0 or less than 0, then the shake will play infinitely.
    
-   **Blend In/Out Time** controls the length of a linear blend at the start and end of the shake. A value of 0 means no blending will occur.
    

![perlin noise timing details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c7a55cc-e87b-4c7a-85b4-c686d8ebef25/perlintiming.png)

### Sinusoidal Wave

Sinusoidal Wave generates noise over time using a continuous wave with smooth periodic oscillation. Typically, wave noise is useful for lower-intensity shakes such as a rocking boat, or a dream-like drifting effect.

![sine wave graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f908564-1d94-4953-8cab-2f1e33b3eda1/wave.png) ![sine wave camera shake example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/152ab071-0128-431e-8c41-1b08ba0ea1b1/waveexample.gif)

When you select **Wave Oscillator Camera Shake Pattern** for your **Root Shake Pattern**, additional details will appear which you can use to control the wave shake behavior. Similar to Perlin noise, it is possible to create a wave shake effect on the location, rotation, and Field of View (FOV) properties of a camera.

![wave oscillator camera shake pattern details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8cf3fd7-a42e-47b0-8c83-145407eb20ae/wavedetails.png)

The properties of **Location**, **Rotation**, **FOV**, and **Timing** for Sinusoidal Wave noise are the same as [**Perlin Noise**](/documentation/en-us/unreal-engine/camera-shakes-in-unreal-engine#perlinnoise). However, when an axis is expanded, there is an additional property called **Initial Offset Type** from which you can specify if you want your waveform to begin at **Zero** or at a **Random** point along the curve.

![sine wave initial offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/318b5271-42aa-401f-ba2b-8ad8e7506ec9/waveoffset.png)

### Sequence Shake

Sequence shakes generates shakes using camera animation contained within [**Camera Animation Sequences**](/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine#cameraanimationsequence). Sequence noise is useful in cases where you want full control over the camera's shake style and behavior.

![sequence shake graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/071271cb-4414-4de2-9319-1618d3476b49/cenoise.png)

When you select **Sequence Camera Shake Pattern** for your **Root Shake Pattern**, additional details will appear which you can use to select the Camera Animation Sequence asset, and control its behavior. The duration of the shake is based on the length of the camera animation sequence.

![sequence camera shake pattern details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dc9ff1a-8830-4268-bdda-22efbcdb9147/sequenceshakedetails.png)

| Name | Description |
| --- | --- |
| **Sequence** | Specifies your [**Camera Animation Sequence Asset**](/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine#cameraanimationsequence). |
| **Play Rate** | The speed of the shake effect. A value of 1 is normal speed, values less than 1 will play the shake slower, and values higher than 1 will play faster. |
| **Scale** | A multiplier applied to the shake intensity. A value of 1 is normal intensity, values less than 1 will be less intense and values higher than 1 will be more intense. |
| **Blend In/Out Time** | **Blend In/Out Time** controls the length of a linear blend at the start and end of the shake. A value of 0 means no blending will occur. |
| **Random Segment Duration** | The duration of the random segment used if **Random Segment** is enabled. |
| **Random Segment** | Enabling this will start playing the shake at a random point in the camera animation sequence. You must also set a value in the **Random Segment Duration** property to define a new length for the shake. This is useful if you have a very long camera shake animation and want to play random smaller segments from it. |

Unlike in typical **Template Sequence** workflows, when creating a Camera Animation Sequence for use as a camera shake pattern, you do not need to set the section to additive.

### Composite

Composite shakes enable the combining of **Perlin**, **Wave**, and **Sequence** shakes in a layer system. Using Composite shakes, you can create more varied shakes that include elements from each shake type.

![composite shake example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68716c19-8249-4435-a782-c84f012ff8e1/compositeexample.gif)

When you select **Composite Camera Shake Pattern** for your **Root Shake Pattern**, additional details will appear which you can use to add child patterns and layer different shake types together.

![composite camera shake pattern details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cde753f-0fc7-4c1c-8bb9-8bc53f39c97d/compositedetails.png)

Clicking the **+** button next to **Child Patterns** will add a new shake pattern to the array. You can add as many shake patterns as you want. Each element contains details relevant to that pattern.

![composite shake array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02fc6004-0b6b-4215-ae78-5c67a6c8f168/compositearray.png)

## Playing Your Shake

Once you have created your camera shake, there are a couple of ways to play it.

### Playing from Sequencer

You can add your shake to a camera in Sequencer by clicking the **\+ Track** button on the **Cine Camera Actor** track, and selecting your camera shake asset in the **Camera Shake** menu.

![sequencer camera shake](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4873668-2c4b-40c9-834a-a82cdeaa63d4/addshakeseq.png)

You can also add the shake to the **CameraComponent** track, which produces the same result.

![sequencer camera component shake](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07c4c9b7-1fc0-4dad-bc47-4d2defcf842e/addshakecomp.png)

Once added, you can play your sequence to see your shake in action.

![sequencer camera shake example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6dbe4fc-950c-48e3-91b9-e6f56929c907/seqshake.gif)

The camera shake section contains visualizations for its duration and blend in / out times determined by the Blueprint details. Changing these properties will update the section display.

![sequencer shake section visualize](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a99df0a-7f09-426d-8f7c-efc6ab4567b8/sectionediting.gif)

Right-clicking the shake section and navigating to the **Properties** menu will reveal the shake properties in Sequencer.

![sequencer shake section details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5469147d-e4c0-42f6-ac6d-f43b997010f4/sectiondetails.png)

| Name | Description |
| --- | --- |
| **Shake Class** | Specifies the shake Blueprint class to use. You can change this shake to a different asset if another is available. |
| **Play Scale** | A global multiplier for the shake intensity. A value of 1 is normal intensity, values less than 1 will be less intense and values higher than 1 will be more intense. |
| **Play Space** | 
Specifies the coordinate space the shake should play in.

-   **Camera Local** will cause the shake to be relative to the camera's position, making it an additive shake.
-   **World** will cause the shake coordinates to be relative to the Level's coordinates.
-   **User Defined** will cause the shake rotational coordinates to be relative to the coordinates specified in **User Defined Play Space**.



 |
| **User Defined Play Space** | When **Play Space** is set to **User Defined**, you can input rotation coordinates here, which are relative to the **World Rotation** coordinates, but with a specified offset. |

### Playing from Blueprints

You can also play shakes from Blueprints using the **Start Camera Shake** node. The node contains parameters for specifying the **Shake**, **Scale**, and **Play Space**.

![start camera shake blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78846e41-72fc-4fbb-a395-4ec60974fe96/shakebp1.png)

The Start Camera Shake function requires a **Player Controller** or a **Camera Shake Source Component** as the target.

## Camera Shake Source

The **Camera Shake Source** triggers camera shakes based on the camera's proximity to a location. It also contains controls for the size and radius of the shake influence. You can add it as an **Actor** in your Level, or as a **Component** in Blueprints.

To add a **Camera Shake Source Actor** to your Level, drag it from the **[Place Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine)** panel into your Level.

![camera shake source actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acc1c11b-8ca1-4e7c-9860-21de194e31da/addsourceactor.png)

Selecting the Actor or Component will reveal the following details:

![camera shake source actor details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0410aa9b-35fd-422b-adb5-4d40627baee6/sourcedetails.png)

| Name | Description |
| --- | --- |
| **Attenuation** | The falloff curve type as the camera gets closer or further away from the source. This can either be **Quadratic**, which provides an ease in and out blend, or **Linear**, which provides a linear blend. |
| **Inner Attenuation Radius** | The radius from the source in which the shake will play at its full intensity. |
| **Outer Attenuation Radius** | The radius from the source in which the shake will no longer be visible. The shake will blend its intensity between the outer and inner radius as the camera moves between them. |
| **Camera Shake** | The shake Blueprint class to use. |
| **Auto Start** | Enabling this will cause the shake to automatically start when playing the game. |

### Looping Shake Example

You can quickly create a source shake effect by doing the following:

1.  In the **Camera Shake Blueprint**, set all **Timing** properties to 0. This will make the shake loop indefinitely with no blending. Also ensure you have set an appropriate amplitude and frequency on your axes so that the shake is visible.
2.  Assign the Blueprint to the camera shake source **Camera Shake** property, and enable **Auto Start**.

![source shake setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3d0ad63-1d66-4b35-9479-e67f24b8f698/sourceshakesetup.png)

Now when you play the game and approach the source point, you should see the shake blend on and off as the camera enters the influence of the camera shake source.

![distance shake example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47f923b4-95aa-45a3-b071-c87fabe21fb7/sourceshakeexample.gif)

### Camera Shake Previewer

The Camera Shake Previewer can be used to preview [**Camera Shake Sources**](/documentation/en-us/unreal-engine/camera-shakes-in-unreal-engine#camerashakesource) in the editor without needing to start the game or simulation.

To open the previewer, navigate to Unreal Editor's main menu and select **Window > Camera Shake Previewer**.

![camera shake previewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33c0c3d1-c2f4-4224-bf50-b7bc3b77cf80/openpreviewer.png)

In order for camera shakes to play in the editor, you will need to enable **Allow Camera Shakes** in the viewport options menu.

![allow camera shakes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61aff6d6-1e61-4df3-95f2-f70c43d3ec60/allowcamerashakes.png)

Next, select the shake source entry you want to preview and click **Play/Stop Selected** to enable the shake preview. You can also click **Play/Stop All** if you want to preview multiple sources at once. Once it is playing, you can move the editor's camera towards the source and see the shake effect.

![camera shake previewer example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d856d03f-b9ce-43e0-9c1f-799a151614b9/shakepreviewexample.gif)