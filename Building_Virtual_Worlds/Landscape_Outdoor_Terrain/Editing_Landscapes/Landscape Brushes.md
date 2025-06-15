# Landscape Brushes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-brushes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-brushes-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:03

---

The **Landscape** tool's Brush defines the size and shape of the area of the Landscape that will be affected by either sculpting or painting. Brushes can have different shapes, sizes, and falloffs. Brushes should be a familiar concept to anyone who has experience using Photoshop or a similar image-editing application.

You can set the brush type and falloff in either the **Sculpt** or **Paint** tab of the Landscape toolbar. Settings can also be adjusted in the Landscape panel.

![Brush Settings Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0ecd4a7-1e74-46fd-94d1-8540d7e6fe0f/01-brush-settings-toolbar.png "Brush Settings Toolbar") ![Brush Settingsin the Landscape Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee3e118f-5fc5-40ec-bb5b-1bb48f422980/02-brush-settingsin-the-landscape-panel.png "Brush Settingsin the Landscape Panel")

| Property | Description |
| --- | --- |
| **Brush Size** | Determines the size of the brush in Unreal Units including the falloff. Within this area, the brush will have at least some effect. |
| **Brush Falloff** | Determines the percentage from the brush's extents where the falloff should begin. Essentially, this determines how hard the brush's edges are. A falloff of 0.0 means the brush will have full effect throughout with hard edges. A falloff of 1.0 means the brush will only have full effect at its center, and the effect will be reduced throughout its entire area to the edge. |
| **Use Clay Brush** | Clay Brush allows for an organic, additive approach to sculpting your Landscape. Similar to working with digital clay. If selected, uses a Clay Brush. |

The size and falloff of the current brush is displayed in the viewport as a pair of concentric circles.

|   |   |   |
| --- | --- | --- |
| ![Falloff of 0.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c665c0e-7b77-4f88-bf47-0e37983816ea/03-falloff-0-0.png "Falloff of 0.0") | ![Falloff of 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e133769-a6b6-4488-82a9-377615f1754c/04-falloff-0-5.png "Falloff of 0.5") | ![Falloff of 1.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b6e5450-c25a-49fe-a4c0-a9d93302b972/05-falloff-1-0.png "Falloff of 1.0") |
| Falloff: 0.0 | Falloff: 0.5 | Falloff: 1.0 |

## Circle

![Circle Brush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc05d9fb-8ca5-4c32-b87e-1b6283287a26/06-circle-brush.png "Circle Brush")

The **Circle** brush applies the current tool in a circular area, with a falloff defined both numerically and by type.

![Circle Brush in use](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d914ace-78a3-4492-a56f-561603c51c0c/07-circle-brush-in-use.png "Circle Brush in use")

### Circle Brush Falloff Type

| Icon | Type | Description |
| --- | --- | --- |
| ![Smooth Falloff](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bec6ec5d-f774-407a-a936-db59b60a7bc2/08-smooth-falloff.png "Smooth Falloff") | **Smooth** | A linear falloff that has been smoothed to round off the sharp edges where the falloff begins and ends. |
| ![Linear Falloff](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17722a10-f9d9-4f40-b411-9d1c843d560f/09-linear-falloff.png "Linear Falloff") | **Linear** | A sharp linear falloff, without rounded edges. |
| ![Spherical Falloff](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de3aea32-d030-4f50-b184-6d7abe22eb44/10-spherical-falloff.png "Spherical Falloff") | **Sphere** | A half-ellipsoid-shaped falloff that begins smoothly and ends sharply. |
| ![Tip Falloff](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aafef3f1-e90a-4084-977a-022881ef2432/11-tip-falloff.png "Tip Falloff") | **Tip** | A falloff with an abrupt start and a smooth ellipsoidal end. The opposite of the **Sphere** falloff. |

Below is an example of each of these falloff types when operating on the heightmap, with the same radius and falloff:

|   |   |   |   |
| --- | --- | --- | --- |
| ![Smooth Falloff example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b905bc2a-9bf0-4477-890b-049314622a48/12-smooth-falloff-example.png "Smooth Falloff example") | ![Linear Falloff example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c04eac35-608e-41f0-8027-d46d77587e5a/13-linear-falloff-example.png "Linear Falloff example") | ![Spherical Falloff example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e14db9c-6b01-4ec5-9288-bd211e206314/14-spherical-falloff-example.png "Spherical Falloff example") | ![Tip Falloff example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f407d169-c17e-40da-9f5a-109789cb5b34/15-tip-falloff-example.png "Tip Falloff example") |
| **Smooth** | **Linear** | **Spherical** | **Tip** |

## Alpha

![Alpha Brush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac2b0ce4-86f9-4823-bdf4-45dee91509e9/16-alpha-brush.png "Alpha Brush")

The **Alpha** brush is similar to the Pattern brush, but instead of tiling the texture across the Landscape as you paint, it orients the brush texture in the direction of your painting and drags the shape as you move the cursor.

![Dragging a Brush Alpha](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e32d88eb-b4bf-46e7-ac22-751ff7a3c6ab/17-brush-alpha-drag.png "Dragging a Brush Alpha")

### Alpha Brush Settings

![Alpha Brush Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7a08687-b441-4189-af20-9baadaa6a626/18-alpha-brush-settings.png "Alpha Brush Settings")

| **Setting** | **Description** |
| --- | --- |
| **Texture** | Sets the Texture to be used, assigned from the **Content Browser**. |
| **Texture Channel** | Sets the Alpha brush's contents to the data from the corresponding channel of the Texture that is currently assigned. |
| **Brush Size** | Sets the size of the brush. |
| **Use Clay Brush** | If selected, uses a clay brush. |

## Pattern

![Pattern Brush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c4213c7-06f2-492a-8a31-a3fa3bf483c3/19-pattern-brush.png "Pattern Brush")

The **Pattern** brush allows you to use an arbitrary shape for the brush by sampling a single color channel from a texture to use as the alpha for the brush. The texture pattern is tiled as the brush is painted.

For example, the textures below could be used as the alpha:

![Alpha Tex](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d4fdf2e-c6da-4b5b-8114-aeca9a0730bf/20-alpha-tex.png "Alpha Tex") ![Alpha Tex Checker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24266e27-7854-41a8-964e-d0bf06d9076f/21-alpha-tex-checker.png "Alpha Tex Checker")

Those would result in the following brushes:

![Alpha Pattern](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f8c6697-1f43-4a3a-ab2d-50209b06d572/22-alpha-pattern.png "Alpha Pattern") ![Alpha Applied](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c379670c-7871-4dbc-b116-df5139c53569/23-alpha-applied.png "Alpha Applied")

![Alpha Pattern Checker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4be6c20-d851-4152-b6ae-e0a72bab5d3d/24-alpha-pattern-checker.png "Alpha Pattern Checker") ![Alpha Default Checker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d884f23-f2f6-4198-a068-af8e2e4d637d/25-alpha-default-checker.png "Alpha Default Checker")

### Pattern Brush Settings

![Pattern Brush Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f6abbaf-20dc-4725-ab14-3f608446dca5/26-pattern-brush-settings.png "Pattern Brush Settings")

| **Setting** | **Description** |
| --- | --- |
| **Texture** | Sets the Texture to be used, assigned from the **Content Browser**. |
| **Texture Channel** | Sets the Pattern brush's contents to the data from the corresponding channel of the Texture that is currently assigned. |
| **Brush Size** | Sets the size of the brush. |
| **Brush Falloff** | Sets the brush falloff. |
| **Use Clay Brush** | Enables you to use a clay brush. |
| **Texture Scale** | Sets the size of the sampled Texture in relation to the surface of the Landscape. ![Alpha Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f31589c1-922d-44e8-9d8e-4abc30fe186d/27-alpha-default.png "Alpha Default") ![Alpha Texscale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f24db43-6737-4d19-a210-0abe1570e771/28-alpha-texscale.png "Alpha Texscale") |
| **Texture Rotation** | Sets the rotation of the sampled texture in relation to the surface of the Landscape. ![Alpha Texrot Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d16b3988-9b9e-48a4-9073-38a3ba4744e1/29-alpha-texrot-default.png "Alpha Texrot Default") ![Alpha Texrotation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53ecdee2-c427-42b5-9ec5-2fc7671a68ba/30-alpha-texrotation.png "Alpha Texrotation") |
| **Texture Pan \[U/V\]** | Sets the offset of the sampled texture on the surface of the Landscape. ![Alpha Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7fbeed7-af1f-47eb-aec7-1dd2a34bcafd/31-alpha-default.png "Alpha Default") ![Alpha Texpan](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b7ab313-78f5-4f44-8d6c-d2dd5767fe7d/32-alpha-texpan.png "Alpha Texpan") |

## Component

![Component Brush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa911b34-aa9c-4044-8c2d-c58aec97a21a/33-component-brush.png)

The **Component** brush is used for operating on individual components. The cursor becomes limited to a single component at a time:

![Component Brush selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b52f6588-e104-4a7b-bbce-73a91505e0d5/34-component-brush-selection.png)

The Component brush is the only brush available when you are using tools that operate on the individual component level.

## Gizmo

![Gizmo Brush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31c88b26-0789-4e84-9560-a1395309d2b4/35-gizmo-brush.png)

The **Gizmo** brush is used for modifying your Landscape with Landscape Gizmos, which are tools that you use to perform actions to a specific localized area of the Landscape.

The Gizmo brush is available only when you are using the Copy/Paste tool in Sculpt mode.

For more information about Gizmos, see [Landscape Copy Tool](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine).