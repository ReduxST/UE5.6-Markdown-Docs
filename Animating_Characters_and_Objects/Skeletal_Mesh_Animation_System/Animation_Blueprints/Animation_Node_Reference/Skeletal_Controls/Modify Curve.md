# Modify Curve

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-modify-curve-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-modify-curve-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:31

---

With the **Modify Curve** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can blend, scale and remap [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) at runtime.

![modify animation curve animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d998d665-444e-44d2-bd79-c293989ea97f/modifycurve.png)

By **right-clicking** the Modify Curve node in the **AnimGraph**, you can select one of the character's [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) from the **Add Curve Pin** option in the context menu to add a pin that corresponds to the selected [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine).

![right click the modify curve node to create a new curve input pin add curve pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f318bbcd-e1b2-49fe-87d1-4a63c14d455c/addcurve.png)

Here, a **Hue Shift** curve has been added to the Modify Curve node to alter the hue of the characters material.

| Description | Graph | Restults |
| --- | --- | --- |
| Here the **Hue Shift** curve has been set to a static value of **1.0** on the Modify Curve Node in the **AnimGraph**. This returns a static value from the curve, resulting in the character displaying a single color material. | ![modify cuuve animaiton blueprint node disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27bc9314-5276-4d0f-8836-e269d75569ca/graphoff.gif) | ![modify curve animation blueprint node bot demo disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c42a6c9a-18df-4ff1-b2be-d2c68e237d90/botoff.gif) |
| Here a **sine wave** is set to drive the **Hue Shift** curve value on the Modify Curve node in the **AnimGraph**. This returns a dynamic value, resulting in the character displaying a rotating color material. | ![modify cuuve animaiton blueprint node disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e275e05-7a98-44bc-813d-a01fa80e02d8/graphon.gif) | ![modify curve animation blueprint node bot demo enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/390601e0-a7f0-4dfc-be75-9c3acf65335c/boton.gif) |

## Property Reference

![modify curve animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a32f499-0e16-45bc-ab4c-02a5dcdecd7a/details.png)

Here you can reference a list of the Modify Curve node's properties.

| Property | Description |
| --- | --- |
| **Curve Map** | Here you can set any curve maps. Curve maps are associative, unordered containers that associate a set of keys with a set of values. Each key in a map must be unique, but values can be duplicated. |
| **Curve Values** | Curve values are the values used to drive curve modifications. You can add a new curve by right-clicking the Modify Curve node in the **AnimGraph** and selecting one of the character's Animation Cures from the Add Curve Pin option in the context menu. These added curve pins can then drive their respective curves with a value. |
| **Alpha** | Set the alpha value to control the blend of the modified curve pose and the source animation pose. By default this property appears as a pin on the node in the **AnimGraph**. |
| **Apply Mode** | 
Set the method to apply the modification to the [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine). The application modification options include:

**Add**: Add new value to input curve value. **Scale**: Scale input value by new value. **Blend**: Blend input with new curve value, using alpha setting on the node. **Weighted Moving Average**: Bend the new curve value with the last curve value using Alpha to determine eht weighting. For example, .5 is a moving average, higher values react to new values faster lower slower. **Remap Curve**: Rempas the new curve values between the Curve Values entry and 1.0. For example, .5 in Curve Values makes 0.51 map to 0.02.



 |