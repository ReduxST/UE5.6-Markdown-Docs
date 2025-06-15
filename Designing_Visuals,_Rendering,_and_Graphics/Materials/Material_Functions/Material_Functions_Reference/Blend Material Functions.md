# Blend Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:09

---

A **Blend** is a type of function that performs mathematical calculations in the color information of a texture so that one texture can blend into another in a particular manner.

Blends will always have a Base and a Blend input, both of which are Vector3. These will each take in a texture and the two will be blended in some way. The manner in which the blend takes place depends on the type of blend function used.

## Blend Functions

Below is a list of all of the blend material functions.

### Blend\_ColorBurn

**Blend\_ColorBurn** blends the textures in such a way that the darker the Blend color the more of that color will be used in the final result. If the Blend color is white, no change takes place.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Color Burn](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3531572-733b-4d6b-9b9f-aa25da4cc83e/colorburn.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95fde1df-1725-4412-bd67-f545fd92d01f/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87bf118c-9542-413d-b1fd-f3cfeb0c43e3/blend.png) | ![Color Burn Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65ca2fb1-0065-4d1c-bb61-40330c7d0226/colorburn2.png) |
|   | Base | Blend | Result |

### Blend\_ColorDodge

**Blend\_ColorDodge** lightens the result by inverting the Base color and dividing it by the Blend color.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Color Dodge](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b71571b3-406f-4997-835f-d1162116c52f/colordodge.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0094dd01-eb0d-4c8f-82bf-9eb6bc7f12ed/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c0ae3d6-781e-4bb9-aa95-74519855621c/blend.png) | ![Color Dodge Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/060aabc0-4d21-45c1-b664-5a57ce5a9dc5/colordodge2.png) |
|   | Base | Blend | Result |

### Blend\_Darken

**Blend\_Darken** works by choosing the darker value for each pixel of the Base and Blend colors. A white Blend color does not produce a change.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Darken](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a18da62f-17bf-4e23-8c55-0822a9496bb6/darken.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b17d0ee-c64c-4d6d-9efb-00a10eee4394/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65cdcf65-9cbb-4718-949f-b6808a49211a/blend.png) | ![Darken Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ca79ccf-ca87-478f-8782-47d46bddd266/darken2.png) |
|   | Base | Blend | Result |

### Blend\_Difference

**Blend\_Difference** creates a sort of inversion-style effect by subtracting the Base from the Blend and then taking the absolute value of the result.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Difference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8441e338-15b0-407c-a594-499c925e26d5/difference.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b08c3356-8e00-4557-ab69-d90f93499c29/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/490ad713-c9c3-4372-8d92-08e981ba1889/blend.png) | ![Difference Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66d32993-0db0-4f04-a3c0-49e48abd66ab/difference2.png) |
|   | Base | Blend | Result |

### Blend\_Exclusion

**Blend\_Exclusion** halves both the Base and Blend textures, combines them, and then does a partial inversion on the result.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Exclusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4393b1df-eacc-4773-a0f2-580aee09437f/exclusion.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00b99659-bed8-48b7-a431-81e524dfc442/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc4bd52e-2efd-4325-8058-87c527912a82/blend.png) | ![Exclusion Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ac52a48-cf52-49b7-aaca-f066a1f0c314/exclusion2.png) |
|   | Base | Blend | Result |

### Blend\_HardLight

Like a harsher version of Blend\_Overlay, **Blend\_HardLight** will either screen or multiply the Base and Blend together. The function does a comparison on the Blend color such that wherever the Blend is brighter than 50% gray, the Base and Blend will be combined via a Screen operation. If the Blend is darker than 50% gray, the Base will be multiplied by the Blend as in the Multiply function. The contrast of the final result is then boosted for a harsh output.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Hard Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70afc8e9-6deb-49a4-8061-6d7ef467fff5/hardlight.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb1886f8-0299-403d-81c7-95d980fc5476/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b77ef0b0-505d-4b9c-9f4a-ac0d605964b5/blend.png) | ![Hard Light Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae8fdf83-8a70-4e8f-bab2-fa3685771d9c/hardlight2.png) |
|   | Base | Blend | Result |

### Blend\_Lighten

**Blend\_Lighten** compares each pixel of the Base and Blend colors and returns the brighter result.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Lighten](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15ad0ab6-8977-4e43-b28d-ba07f4a36511/lighten.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8d776c1-a4cc-4b16-8839-8706f93401ae/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b47e96e-2746-475a-bb8a-d22130dd537e/blend.png) | ![Lighten Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26ee97d0-2231-4e90-b128-7ada8edf810b/lighten2.png) |
|   | Base | Blend | Result |

### Blend\_LinearBurn

**Blend\_LinearBurn** adds Base color to the Blend color and then subtracts 1 from the result.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Linear Burn](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a082f7c-53a9-40a0-bcd7-823eb2ddae58/linearburn.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d4ccd46-d538-426f-bdf5-e8f437d705f4/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab85587d-3e4c-427c-a82e-f85089f74592/blend.png) | ![Linear Burn Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ac30230-c4a2-482f-a6da-a57dfce58d70/linearburn2.png) |
|   | Base | Blend | Result |

### Blend\_LinearDodge

**Blend\_LinearDodge** adds the Base color to the Blend color.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Linear Dodge](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/827e22d5-c3e8-4747-848c-db35b6741411/lineardodge.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70d5f5c1-ffb2-4662-89a3-ece88e145ee0/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfe8f889-3291-4d65-857e-31cdf41d22ac/blend.png) | ![Linear Dodge Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dd23e55-c3b6-4a82-95cb-1e2ad07ad323/lineardodge2.png) |
|   | Base | Blend | Result |

### Blend\_LinearLight

**Blend\_LinearLight** is a linear version of Blend\_Overlay, providing harsher results. The function does a comparison on the Blend color such that wherever the Blend is brighter than 50% gray, the Base and Blend will be combined via a Screen operation. If the Blend is darker than 50% gray, the Base will be multiplied by the Blend as in the Multiply function.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Linear Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/690570e4-f15d-4361-9846-c1db89403711/linearlight.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6b1cba8-96bf-4b7a-a5d0-78b32fecf888/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa756e50-f1d7-425f-8a4d-da5beb665dbe/blend.png) | ![Linear Light Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/391e36a0-09f5-4064-8ddb-f828154e8663/linearlight2.png) |
|   | Base | Blend | Result |

### Blend\_Overlay

**Blend\_Overlay** will either screen or multiply the Base and Blend together. The function does a comparison on the Blend color such that wherever the Blend is brighter than 50% gray, the Base and Blend will be combined via a Screen operation. If the Blend is darker than 50% gray, the Base will be multiplied by the Blend as in the Multiply function.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Overlay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3179dc78-265a-4667-b2e8-3da645a5c5d6/overlay.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b7ea369-2f96-4733-9186-d17b99d72947/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0eaa901-3f9a-4192-b975-b4056cd5a146/blend.png) | ![Overlay Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db4c37cc-f5f1-41ca-8ae2-0b63f87e49c8/overlay2.png) |
|   | Base | Blend | Result |

### Blend\_PinLight

Like Blend\_Overlay, **Blend\_PinLight** will either lighten or darken the Base and Blend together. The function does a comparison on the Blend color such that wherever the Blend is brighter than 50% gray, the Base and Blend will be combined via a Screen operation. If the Blend is darker than 50% gray, the Base will be multiplied by the Blend as in the Multiply function. The contrast is softened, making this a less harsh version of Overlay.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Pin Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b1b0271-f33e-4baf-9177-17fde3a42069/pinlight.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34b6551a-7060-4f23-8fe5-51615bfbeed8/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bc8b3f9-8033-40e4-acb2-634710ea5fe2/blend.png) | ![Pin Light Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a43445c9-7bc2-4ead-becf-af011cd01064/pinlight2.png) |
|   | Base | Blend | Result |

### Blend\_Screen

**Blend\_Screen** lightens the Base by the Blend color. It does this by doing a "one minus" on both colors, multiplying them together, and taking a one-minus of the result.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Screen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c2d9dd2-1899-4be6-a0c9-1a7526e45f08/screen.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61c9e1d8-650f-4f2d-9a03-b06e8ce2884c/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d0acbd5-2f59-46b7-91d2-5759b632cfbe/blend.png) | ![Screen Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e8e0599-5df3-48b6-ace8-254354df09cf/screen2.png) |
|   | Base | Blend | Result |

### Blend\_SoftLight

**Blend\_SoftLight** is a softer version of Overlay. The function does a comparison on the Blend color such that wherever the Blend is brighter than 50% gray, the Base and Blend will be combined via a Screen operation. If the Blend is darker than 50% gray, the Base will be multiplied by the Blend as in the Multiply function. The contrast is softened, making this a less harsh version of Overlay.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Base (Vector3)** | The base, or original texture that will be blended with the Blend texture in some way. |
| **Blend (Vector3)** | The blend texture, which is combined with the base in some way based on the type of blend operation taking place. |

![Soft Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8ac455-e7c6-417e-86d6-3b35206c7fd8/softlight.png)

|   |   |   |   |
| --- | --- | --- | --- |
|   | ![Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91c04ccc-dd6f-4a24-ad12-77749cf3e668/base.png) | ![Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a885871-3efc-401b-93d1-9ae44be9f094/blend.png) | ![Soft Light Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bc2197b-043a-4e1a-acf0-fec6f75a6451/softlight2.png) |
|   | Base | Blend | Result |