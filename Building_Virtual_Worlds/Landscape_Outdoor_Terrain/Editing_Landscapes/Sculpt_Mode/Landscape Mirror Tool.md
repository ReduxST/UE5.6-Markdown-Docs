# Landscape Mirror Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-mirror-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-mirror-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:19

---

The **Mirror** tool enables you to mirror or rotate the existing Landscape heightmap geometry along the X or Y axis.

In this example, the Mirror tool is used to mirror the entire entire Landscape Actor along the Y axis.

## Using the Mirror Tool

1.  In the Landscape toolbar, in **Sculpt** tab, select the **Mirror** tool.
    
    ![Mirror Tool button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1380bfaf-ea92-420b-a0a4-fdac17474aee/01-mirror-tool-button.png "Mirror Tool button")
2.  Use the **Operation** drop-down selection to choose the axis and mirroring method you would like to use for your selected landscape. The directional arrow indicates which side of the landscape geometry will be mirrored on.
    
    ![Mirror Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbc968cb-390b-4a10-b580-0a5ec18a54d0/02-mirror-settings.png "Mirror Settings")
3.  If necessary, adjust the **Mirror Point** values for the mirror plane or Left-click and drag the directional arrow on mirror plane into the position you want to mirror.
    
    Only the currently selected **Operation** axis will be used for the **Mirror Point**. For example, if the Operation method is "-X to +X" the X axis is the only active Mirror Point that will be affected.
    
    ![Setting the Mirror Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85dda869-522c-4e7c-889f-3f200cbcad0e/03-setting-the-mirror-point.png "Setting the Mirror Point")
4.  Once you are satisfied with your edits, you can hit the **Apply** button to see the results.
    
    ![Applying Mirror](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/927ead4a-0234-499b-b9e3-415916811dba/04-applying-mirror.png "Applying Mirror")
    
    You now have a landscape with mirrored geometry.
    

### Mirror Smoothing Width

If the edge seams from mirroring your landscape look unnatural or too sharp in contrast after you apply your changes you can use **CTRL + Z** to undo your last action. Then you should adjust the **Smoothing Width** so that these edge vertices that are merged are softened.

![Smoothing Width Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff0a919d-28f1-4930-8d83-95365abb40f2/05-smoothing-width-before.png "Smoothing Width Before")

![Smoothing Width After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb64dc06-9539-4e6c-9d7b-b385087c067a/06-smoothing-width-after.png "Smoothing Width After")

In this example, the left image has no smoothing applied after the Landscape is mirrored, whereas the right is using a value of 10 to smooth the mirrored edges and reduce the harshness of the seam.

## Tool Settings

|   |   |
| --- | --- |
| ![Mirror Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85376936-372f-4128-b401-5d38d3ed7bc9/07-mirror-tool.png "Mirror Tool") | ![Mirror Tool properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31015f03-76f0-4434-9d3d-ca6027bee5ae/08-mirror-tool-properties.png "Mirror Tool properties") |

| **Property** | **Description** |
| --- | --- |
| **Mirror Point** | This sets the location of the mirror plane. This will default to the center of the selected Landscape and in most cases will not normally need to be changed. |
| **Operation** | The type of mirroring operation to perform. For example, -X to +X will copy and flip the -X half of the Landscape onto the +X half. |
| **Recenter** | This button places the mirror plane back at the center of the selected Landscape. |
| **Smoothing Width** | This will set the number of vertices on either side of the mirror plane to smooth over reducing sharp contrasting angles for mirrored sides. |