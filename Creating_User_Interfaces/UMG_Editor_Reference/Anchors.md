# Anchors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-anchors-in-unreal-engine-ui](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-anchors-in-unreal-engine-ui)  
**Processed:** 2025-06-14 16:55:25

---

Use **Anchors** to set location of the UI widgets on a **Canvas Panel**. The Anchors supports settings with different screen sizes and aspect ratios.

**Minimum (X,Y)** and **Maximum (X,Y)** Anchors parameters and offset parameters determine location of each widget.

You are able to select from a number of Anchors presets or set up it manually by the Minimum (X,Y) and Maximum (X,Y) parameters (where **Min (0,0)** and **Max (0,0)** determine the upper left corner of the Canvas Panel; **Min(1,1)** and **Max(1,1)** determine the bottom right corner of the Canvas Panel). Anchors presets differ in the set of offset parameters.

## How Anchors Work

**Anchor Medallion** shows the Anchor position in the Canvas Panel. It is marked by the yellow box in the image below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84597427-3e2c-4396-8146-f8b290a3c3b8/anchormedallion.png)

Image below shows you the **Image Widget** placed on the Canvas Panel. For this you should drag the **Image** from the **Palette panel** onto the **Canvas Panel**. Use default settings of Anchors (top left corner location).

The horizontal yellow line is X-axis Button offset. It determines distance in Slate Units from Anchor Medallion to the Image in the X-direction.

The vertical yellow line is Y-axis Button offset. It determines distance in Slate Units from Anchor Medallion to the Image in the Y-direction.

The offset parameters based on Canvas Panel size and adapt to size changes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/347c6d83-fb04-4f2c-b1d4-e644f2884e10/button1.png)

Click the **Screen Size** Button in the graph to change the currently used size. It is very useful to test the UI widget layout with different screen sizes or aspect ratios and adjust accordingly.

It is important to take into account differences in device screen sizes and aspect ratios, when you set Anchors and offset parameters of the widgets. You should avoid shifting widget out of the viewport. It could happen in case innapropriate Anchors settings for some screen sizes.

Image below shows what it looks like. Yellow box marks the location of Anchor point. Image is shifted off viewport.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0ee3bc1-6118-4fea-9b08-bddeab6233e4/ingamebutton1.png)

Set up the Anchor location to the lower right corner.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00f77fbf-c94c-4143-a4d2-add538482128/button2.png)

These settings allow you to avoid cropped off screen, and the Image is shifted inside viewport. Image below shows what it looks like. Yellow box marks the location of Anchor point.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85f22635-3ff3-4c77-b603-b7cca8dbf1ba/ingamebutton2.png)

This example shows the effect of the Anchors on widgets position in viewport, depending on aspect ratios. You can also split the Anchor Medallion into several components. With the help of this, you will be able to set more offset options to customize the display of widgets with different screen sizes and aspect ratios (see the [Manual Anchors](/documentation/en-us/unreal-engine/umg-anchors-in-unreal-engine-ui#manualanchors) section for more information).

## Preset Anchors

Preset Anchors is the most common method of Anchor point setting for widgets. With the help of this, you will be able to cover most of your needs in setting position of UI widget.

Select preset from **Anchors** drop-down window at the **Details** panel. Each preset determines the Anchor point location. The silver box marks this location.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32a72c61-2308-4feb-a620-9ed4f5d7065c/presetanchor.png)

For example, select the Center/Center preset Anchor option for widget you need.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70ef9720-50e4-454f-9d48-803bb190c6e8/centercenter.png)

There are also preset stretching methods of the Anchor Medallion, when it is splitted into several components.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c84ea001-e5b5-4926-90de-984fe579cb98/horizontalstretch.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4af3878-11e7-45a4-b3dd-3082ecb70eb0/verticalstretch.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1ea3c7f-3193-471a-a72a-952959ac2439/stretchboth.png) |
| Horizontal Stretch | Vertical Stretch | Stretch Both |

With the help of this, you will be able set up widget to stretch along with the viewport, based on screen size.

Image below shows the preset, which stretch Anchor of widget along bottom side of the Canvas Panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45e12c1f-ee11-4dfa-8a79-fcf59979cf02/progressbar3.png)

In this case, the stretching of the Anchor Medallion means splitting it into two pieces.

You can split the Anchor Medallion by draging one of the pins.

Progress Bar with Anchors settings, which is described before, in game process looks as following:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c2136c4-59cc-44a4-9809-29304d84eefd/progressbar4.png)

In case of using another aspect ratios of viewport, it looks as following:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2173801c-5bec-4e33-a33b-0e4a3d1dfcdc/progressbar5.png)

## Manual Anchors

In some cases, it is necessary to set Anchors manually. For example, this is useful, when you need to anchor widgets to each other.

Image below shows the Image Widget next to the Progress Bar Widget. Both of them are inside the Canvas Panel, which is placed on another Canvas Panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fb67129-1a96-4d13-9314-232d9f029ab1/manual1.png)

The Progress Bar Widget and the Image Widget has Anchors to the upper left corner of the Canvas Panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/659cb7d6-f3c3-4b5c-843e-4268981a011d/manual2.png)

The following shows adjustment process of the sizes proportional dependence between the Canvas Panel, widgets, and their positions.

Set the Progress Bar to stretch along longitudinal side of the Canvas Panel and fix distance from right side. You should do it by setting Anchors as following: move the Anchor Medallion of the Progress Bar to the center of the Progress Bar left side, then splitting apart the Anchor Medallion by dragging the left center pin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e8ceb2c-2c29-4cd8-85a2-0c2e96798b0e/manual3.png)

With the help of these settings, there is a proportional dependence between the Canvas Panel and the Progress Bar horizontally. Also, there is a fixed distance between right sides.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d2d9378-1630-46db-b7f7-e753ea48751f/manual4.png)

The next step is to fix the Image Widget position in the Canvas Panel and fix the distance between the Image Widget and the Progress Bar Widget.

Move the Anchor Medallion of the Image to the Progress Bar top left corner.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37d0eeff-d048-4261-b5c7-4fe0f18aa713/manual5.png)

With the help of these settings, Image moves with resizing of the Canvas Panel. Distance between the Image and the Progress Bar is fixed.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6583ed46-61db-4478-9b28-4f195fcd210b/manual6.png)

Set fixed distance between the Image and right side of the Canvas Panel. With the help of this, you avoid cropping the Image off with the Canvas Panel resizing.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82644074-e6ac-41ff-add3-ca5ee3d0a320/manual7.png)

Move and split the Anchor Medallion of the Image as shown below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59f5a951-b016-4ffb-a7bc-ff2fa0ebc3b4/manual8.png)

With the help of these settings, the Image location is fixed horizontally. Also, there is a proportional dependence between the Canvas Panel and the Image horizontally.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3d832b3-8670-4445-9708-2f101842cdd7/manual9.png)

The next step is to fix the Image Widget position in vertical direction. With the help of this, you avoid displacement of the Image relative to the Progress Bar.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f16a8fcd-67b0-4e40-8c82-0e1df33e78f0/manual9b.png)

Fix the Image position based on Progress Bar position in X and Y direction, by setting the Anchor Medallion as shown.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3a4b84f-922f-43e8-b675-8f850e5b0df1/manual10.png)

As a result, there is a proportional dependence of sizes in any direction between the Canvas Panel, the Progress Bar, and the Image. Also, there is fixed positions of each item.