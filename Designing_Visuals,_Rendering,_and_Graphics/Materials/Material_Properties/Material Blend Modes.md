# Material Blend Modes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:08

---

Blend Modes describe how the output of the current Material will blend over what is already being drawn in the background. Put more technically, it allows you to control how the engine will combine this Material (**Source color**) with what is already in the frame buffer (**Destination color**) when this Material is rendered in front of other pixels.

Blend Mode options are found in the Details panel with the rest of the base [Material Properties](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-properties):

[![Blend Modes dropdown menu](https://dev.epicgames.com/community/api/documentation/image/80c04109-dfc7-492d-a02b-83cf587b1dd9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/80c04109-dfc7-492d-a02b-83cf587b1dd9?resizing_type=fit)

This document uses a sphere placed between the camera and a wall to demonstrate the various Blend Modes. By changing the Blend Mode on the sphere Material you can see how the object blends with the pixels behind it.

[![Blend Modes demo setup](https://dev.epicgames.com/community/api/documentation/image/464a22e9-9dab-4d3f-8107-e68d7c7b7b06?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/464a22e9-9dab-4d3f-8107-e68d7c7b7b06?resizing_type=fit)

## Opaque

The Opaque Blend Mode is the most straightforward, and probably the one you will use most often. It defines a surface through which light neither passes nor penetrates. This is perfect for most plastics, metals, stone, and the larger percentage of other surface types. From the perspective of the camera, the golden sphere completely occludes the wall behind it.

[![Opaque Blend Mode](https://dev.epicgames.com/community/api/documentation/image/5c85b439-6e1e-4d1e-8558-86c5216307e3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5c85b439-6e1e-4d1e-8558-86c5216307e3?resizing_type=fit)

|   |   |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/4085402d-b79d-41a6-b646-2dd10bda729a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4085402d-b79d-41a6-b646-2dd10bda729a?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/1d3d6309-2e9c-43d1-a5bd-e2b6b8bbfc89?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1d3d6309-2e9c-43d1-a5bd-e2b6b8bbfc89?resizing_type=fit)



 |
| 

Scene Setup

 | 

Camera's View

 |

## Masked

The Masked Blend Mode is used when you need to selectively control visibility in a binary (on/off) fashion. For example, consider a Material that simulates a chain link fence or grate. You will have some areas that look solid while others are invisible. Such Materials are perfect for the Masked Blend Mode.

A Masked Material graph is shown below, with a black and white striped texture plugged into the **Opacity Mask** input. White parts of the mask are rendered, while black parts are invisible. There are no intermediate levels of opacity when using a Masked Material.

[![Masked Material Graph](https://dev.epicgames.com/community/api/documentation/image/7b69179a-3e32-4f01-9849-2563a1c1fd77?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b69179a-3e32-4f01-9849-2563a1c1fd77?resizing_type=fit)

Here is that Material from the camera's perspective:

[![Masked Material](https://dev.epicgames.com/community/api/documentation/image/44a1ee3b-ed0a-48d8-b997-63f6477ac6cd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/44a1ee3b-ed0a-48d8-b997-63f6477ac6cd?resizing_type=fit)

It is important to keep in mind the difference between **transparent** and **not rendered**. A transparent surface, such as glass, still interacts with light in the form of reflections (specularity). Pixels that are culled in Masked mode simply do not draw; you will not see any reflections in those areas. If you want to retain reflections or specular aspects, you would do well to use the Translucent Blend Mode, or consider making a [Layered Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/layering-materials-in-unreal-engine).

Further, since these features don't render in the masked area, they aren't calculated at all, leading to performance savings on the GPU.

### Opacity Clip Mask

When using Masked Blend Mode, you need to pay special attention to the **Opacity Mask Clip Value** property. This property holds a 0-1 scalar value which controls what value of the opacity mask texture will be used as a cutoff point, beyond which all **darker** pixels will not render.

![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/846604ab-7682-472f-b009-b42c1a7abce0?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/3d8ffc6c-bfc3-415b-95e1-9445b0d744f9?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/a8aada1e-5546-4eca-8136-2bd6aac1c4da?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/7dd3acfe-394f-48fa-8fd6-059df22fdb74?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/c57058f5-9dd0-431c-9959-920caea7fa5b?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/5ba7513c-dcf1-486b-af61-64c6d5817795?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/2221784e-eb85-4cd1-aebc-6ae4608a2756?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/f5e53311-4ab1-4e5f-b7fa-cdef8e1af037?resizing_type=fit&width=1920&height=1080)![Opacity Mask Clip Value (Drag the slider to preview.)](https://dev.epicgames.com/community/api/documentation/image/4fa85369-54a4-4cdf-a095-ea7289411de9?resizing_type=fit&width=1920&height=1080)

**Opacity Mask Clip Value (Drag the slider to preview.)**

In the example above, the Material has its **Two Sided** property set to **True** (checked), which is why you can see the inside of the box.

Also, despite the interactive example shown here, the **Opacity Mask Clip Value** property is not designed to be changed at runtime.

## Translucent

The Translucent Blend Mode is used for objects that require some form of transparency. This differs from the Masked Blend Mode in that it allows varying levels of translucency.

[![Translucent Material Graph](https://dev.epicgames.com/community/api/documentation/image/d1c99238-fe13-4b65-a256-f49db8ab4da0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d1c99238-fe13-4b65-a256-f49db8ab4da0?resizing_type=fit)

This Blend Mode works by taking in an **Opacity** value or texture and applying it to the surface such that black areas are completely transparent, white areas are completely opaque, and the varying shades of gradation between result in corresponding transparency levels. In the example, a black to white gradient is plugged into the Opacity input, resulting in a sphere that is fully transparent at the top of the mesh and gradually reaches full opacity at the bottom.

[![Translucent gradient on a sphere](https://dev.epicgames.com/community/api/documentation/image/ca50ec87-48d6-4187-916f-0bd30d040c24?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ca50ec87-48d6-4187-916f-0bd30d040c24?resizing_type=fit)

An important consideration when using Translucent Materials is that they do not currently support specularity. This means that you will see no reflections along the surface. However, such reflections can be faked using a Cubemap in a node network similar to this. The Cubemap texture is simply added on top of the Base Color.

[![Fake specularity on sphere](https://dev.epicgames.com/community/api/documentation/image/8c75d900-c0c0-4623-a953-1fc543d2f0c4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c75d900-c0c0-4623-a953-1fc543d2f0c4?resizing_type=fit)

## Additive

The Additive Blend Mode simply takes the pixels of the Material and adds them to the pixels of the background. This is very similar to the *Linear Dodge (Add)* Blend Mode in Photoshop. This means that there is no darkening; since all pixel values are added together, blacks will just render as transparent. This Blend Mode is useful for various special effects such as fire, steam, or holograms.

[![Additive Material Graph](https://dev.epicgames.com/community/api/documentation/image/2bfbb274-4b31-498e-9b19-4933bce0e1a3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bfbb274-4b31-498e-9b19-4933bce0e1a3?resizing_type=fit)

As with the Translucent Blend Mode, this Blend Mode does not respect specularity (i.e. reflections). The additive nature of the blending probably means you will not use it anyway, but it is possible to simulate a reflection-like effect using the Cubemap method shown above in the Translucent section.

In the image below a second sphere was added to the scene. Note that where the two spheres overlap, the pixels are added together and therefore brightened.

[![Additive Material Example](https://dev.epicgames.com/community/api/documentation/image/9a0a4454-ab5b-4acc-8a7b-4044bb5f4aea?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a0a4454-ab5b-4acc-8a7b-4044bb5f4aea?resizing_type=fit)

One drawback of Additive Materials is that they are often difficult to see against light colored backgrounds. A side view of the spheres demonstrates this.

[![Additive Material side view](https://dev.epicgames.com/community/api/documentation/image/d04441ac-8ceb-4f58-ae13-803e224394b8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d04441ac-8ceb-4f58-ae13-803e224394b8?resizing_type=fit)

A solution is to use the [AlphaComposite](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine) Blend Mode instead, which can improve saturation and visibility in bright scenes.

## Modulate

The Modulate Blend Mode multiplies the value of the Material against the pixels of the background. The behavior is very similar to the Multiply Blend Mode in Photoshop, and produces a darkening effect.

[![Modulate Material Graph](https://dev.epicgames.com/community/api/documentation/image/0a787355-a006-455f-a2ac-4c79b6f3747c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0a787355-a006-455f-a2ac-4c79b6f3747c?resizing_type=fit)

In the graph above, the Material Shading Model is set to **Unlit** and the Blend Mode to **Modulate**. A Constant3 Vector is plugged into the Emissive input to define the surface color.

[![Modulate Material Example](https://dev.epicgames.com/community/api/documentation/image/ed8f0e03-3224-4a98-88cd-00eb417716ee?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ed8f0e03-3224-4a98-88cd-00eb417716ee?resizing_type=fit)

Notice again that with multiple spheres, the pixels that overlap are multiplied together and become darker.

The Modulate blend mode is best suited for certain particle effects, but care must be taken as it does not support lighting or Separate Translucency.

## Alpha Composite

The **AlphaComposite** blend mode enables you to control how parts of the material are blended. With some material setup and logic, you can control what parts are blended additively and what parts are blended translucently using the opacity input of the material. AlphaComposite works by multiplying the underlying scene color by the inverse of the material’s opacity so that when the material is added to the scene color, areas of high opacity appear more saturated and full than those that are more opaque.

[![Alpha Composite graph](https://dev.epicgames.com/community/api/documentation/image/8bacb524-4d1a-4348-8463-dc5a6fdc41f6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8bacb524-4d1a-4348-8463-dc5a6fdc41f6?resizing_type=fit)

Example of a material set up to use AlphaComposite with a partical effect.

## Alpha Holdout

The **AlphaHoldout** blend mode lets you "hold out" the alpha of a Material, punching a hole through the objects directly behind it in view space. The following image shows the camera and scene layout for an AlphaHoldout implementation.

[![](https://dev.epicgames.com/community/api/documentation/image/cd4cfe14-b443-4080-a7a1-a9edc77f3298?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cd4cfe14-b443-4080-a7a1-a9edc77f3298?resizing_type=fit)

1.  The camera.
    
2.  A Static Mesh in the foreground acts as the "hole-punching" object. The **AlphaHoldout Material** is applied to this mesh. This Material must use the **Unlit** Shading Model.
    
3.  A receiving surface (which you intend to punch a hole through) is placed behind the AlphaHoldout object; in this case, a brick wall. The Material on the receiving surface **MUST** use either the Translucent, Additive, Modulate, or AlphaComposite Blend Modes. An AlphaHoldout Material cannot act upon an Opaque Material.
    
4.  The background of the scene, which will be visible through the hole.
    

From the camera's perspective, you will see a transparent hole through the receiving surface, making the objects behind it visible.

[![AlphaHoldout Example](https://dev.epicgames.com/community/api/documentation/image/ae849d98-8bbe-4741-b762-8ea9eef5c73f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ae849d98-8bbe-4741-b762-8ea9eef5c73f?resizing_type=fit)

Because the AlphaHoldOut material is on a separate Static Mesh Asset, you can easily move it around in-editor or animate it in game.

## Blend Mode Formulas

| Mode | Description |
| --- | --- |
| 
**Opaque**

 | 

Final color = Source color. This means that the Material will draw on top of the background. This blend mode is compatible with lighting.

 |
| 

**Masked**

 | 

Final color = Source color if OpacityMask > OpacityMaskClipValue, otherwise the pixel is discarded. This blend mode is compatible with lighting.

 |
| 

**Translucent**

 | 

Final color = Source color \* Opacity + Dest color \* (1 - Opacity). This blend mode is **NOT** compatible with dynamic lighting.

 |
| 

**Additive**

 | 

Final color = Source color + Dest color. This blend mode is **NOT** compatible with dynamic lighting.

 |
| 

**Modulate**

 | 

Final color = Source color x Dest color. This blend mode is **NOT** compatible with dynamic lighting, or fog, unless this is a decal material.

 |
| 

**AlphaComposite (Premultiplied Alpha)**

 | 

Final Color = Source Color + Dest Color \* (1 - Source Opacity).

 |
| 

**AlphaHoldout**

 | 

Final Color = Dest Color \* (1 - Source Opacity). This blend mode is **NOT** compatible with dynamic lighting.

 |