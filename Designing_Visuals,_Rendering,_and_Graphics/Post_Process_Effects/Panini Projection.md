# Panini Projection

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/panini-projection-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/panini-projection-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:39

---

## Configuration

By default, Unreal Engine is using a perspective projection. However this projection model create distortions of the geometry when working with a wide field of view. It is very noticeable for instance here with sphere and a FOV = 120.

[![](https://dev.epicgames.com/community/api/documentation/image/987bc4dd-a24e-497b-b242-04c5d2720d34?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/987bc4dd-a24e-497b-b242-04c5d2720d34?resizing_type=fit)

Therefore Unreal Engine provides a optional post processing pass that attempt to fix this issue using a Panini Projection. The idea of this post processing is to displace the rendered pixel at the location where they should using the panini projection instead of the perspective projection. To set up, the only thing you need to do is setting up `r.LensDistortion.Panini.D > 0` . This post process effect is done in the Upscaling pass. It means this pass is then going to be used if `r.ScreenPercentage != 100` or `r.LensDistortion.Panini.D > 0` . For further understanding of this parameter, you can refer directly to the original research paper referenced at the bottom of this page.

[![](https://dev.epicgames.com/community/api/documentation/image/58d808dc-df00-4eab-9e5e-2c93c724f270?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/58d808dc-df00-4eab-9e5e-2c93c724f270?resizing_type=fit)

`r.LensDistortion.Panini.D > 0`  directly emphasizes the effect. However it is not the only parameter, `r.LensDistortion.Panini.S lerp` with the paper's hard compression. And if some sphere still looks eclipsed in the corners, then this parameter can also be tweaked as well. However, for `r.LensDistortion.Panini.S < 0`, it starts to show unrendered black looking pixels in the corners.

[![](https://dev.epicgames.com/community/api/documentation/image/091e067a-12c5-4dfe-bbb7-02987013ae6b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/091e067a-12c5-4dfe-bbb7-02987013ae6b?resizing_type=fit)

To have more understanding of how this effect works, `r.LensDistortion.ScreenFit` can be modified as well. One thing to have in mind is that some of the perspective projected pixels are at the end being not show at the screen near the top and bottom of the screen.

[![](https://dev.epicgames.com/community/api/documentation/image/6b262b0d-0f86-47b6-8598-e19b611745ae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b262b0d-0f86-47b6-8598-e19b611745ae?resizing_type=fit)

## Straight lines

The panini projection brings several guarantees on the lines. Firstly the vertical lines are guaranteed to stay straight for any `r.LensDistortion.Panini.D` and `r.LensDistortion.Panini.S`. Secondly, the lines going through the center of the screen is guaranteed to stay straight as well for any `r.LensDistortion.Panini.D`, but `r.LensDistortion.Panini.S = 0`. This mathematical property is therefore ideal in **First-Person-Shooter** games because the panini projection of a weapon directed towards the center of the screen is going to keep its straight lines going towards the center.

## Center Blurriness

One issue of this post processing effect is that a blur phenomena at the center of the screen kicks in as  `r.LensDistortion.Panini.D` increase. The panini projection has been implemented in the upscale pass especially to take advantage of the sharpening filter to fight against this phenomena. However it can quickly become not enough to fix this issue. Therefore you may need to increase `r.ScreenPercentage` to help fixing that issue but that is going to have a cost on all your rendering performance because increasing the number of pixels to draw. You may consider choosing a better trade of by then choosing a lower value of  `r.LensDistortion.Panini.D` on hardware that can't afford an higher screen percentage, and still have this effect by only relying on the upscale pass's sharpening filter.

[![](https://dev.epicgames.com/community/api/documentation/image/9b04da01-c3e5-4349-960a-e4c6e817d149?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b04da01-c3e5-4349-960a-e4c6e817d149?resizing_type=fit)

Another way to use the panini projection is through a Material function outputting a world position offset to be plugged into the material's world position offset input pin. This is actually what Unreal Tournament uses instead of rendering the weapon at a different FOV to fix the perspective projection distortions. You may want to have a look at it in the UT's github repository.

## References

-   [Original article's website](http://tksharpless.net/vedutismo/Pannini/).
    
-   [Original article's direct link](http://tksharpless.net/vedutismo/Pannini/panini.pdf).