# Slate Clipping System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-slate-clipping-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-slate-clipping-system-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:53

---

**Unreal Engine (UE)** uses Slate's clipping system to restrict graphics or text to a region of your screen. This is done by creating a clipping rectangle (or clipping rect) around the objects and panels that are created. This system is used throughout the Editor and the UMG UI Designer tools. Slate enables users to move panels and resize them as needed in the Editor, and the clipping system enables the text and graphics to be confined to their clipping rect. With UMG, this enables better render transforms that clip appropriately for your UI.

## Clipping Overhaul

Unreal Engine 4.17 overhauled the clipping system to be much more flexible than it has in previous versions. This created a potential to add more rendering effects for tool systems like [UMG](/documentation/en-us/unreal-engine/specialized-blueprint-visual-scripting-node-groups-in-unreal-engine) to use for your project's UI. The clipping system used in prior versions was limited and only axis-aligned for layout-space which lead to noticeable difficulties with render transforms, generally around edges, like in the example below:

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/453ea40f-7c21-4fe7-9378-5c2dae295eb7/oldclippingissue1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc06b11b-a99e-4979-a8b3-a8b00e8f3957/oldclippingissue2.png) |

This example shows that while the Widget is rotated the clipping rect (white dots) is not, which causes the graphic not to render even though it is within the Canvas panel bounds.

Below is comprised list of differences between version 1.0 and 2.0 of the Clipping System:

| Clipping 1.0 (4.16 and earlier) | Clipping 2.0 (4.17 and later) |
| --- | --- |
| 
-   Axis-aligned clipping - Only functions in layout space
-   Every Widget gets clipped
-   All clipping is done in the pixel shader (requires six floats per vertex)
-   Allowed batching across clipping rects, since the rects are part of the batch data
-   Render Transforms are "special" in that they allow rendering outside the clipping rect provided by the parent, with side effects when the layout rect is clipped



 | 

-   A clipping that is an arbitrary quad
    
    -   Axis-aligned clipping zone using Scissor Rects to clip - which avoids unnecessary pixel shader operations
    -   Complex clipping zones use the stencil buffer to compose an arbitrary stack of clipping zones into the stencil buffer that is then used to clip draw calls
-   Very few widgets clip now (by default), consisting mostly of scroll panels and editable text fields
    
    -   Render Transforms are no longer "special," so any transform can allow you to render outside of another widget, provided it doesn't clip.
-   Slate can no longer batch across clipping zones. This frees up six floats in the Slate vertex format, and no longer need to clip in the pixel shader
    



 |

Because the new system supports clipping in the render space of the widgets instead of requiring axis-alignment, the system no longer needs to be concerned with clipping issues (left), and instead clips the outermost widget. Now, any transform that is applied to the inner widgets will be correctly clipped at the edges (right).

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ed95c9c-b95f-4d3c-8112-ebcf77361c5d/clippingold.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8499433-f92a-40a7-937e-8937f22deaff/clippingnew.png) |
| 4.16 and earlier clipping and transforms. | 4.17 and later, clipping applied at edges, along with transforms to the children. |

For the most part, you shouldn't need to worry about changing the clipping state of a widget. If you were to consider game UI as an example, you wouldn't really need to adjust the widget in UMG and mostly would change this for something like a scroll panel, or in cases, like the Editor, where you can't control the length of the text and need to clip it for resizing the windows or parts of the panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eb37950-7494-4a58-afa8-fd60b32ccf41/clippingexamples.png)

Here are a few examples of what you might see with various clipping setups:

-   Left - No clipping is enabled on the button or the text.
-   Center - Clipping is enabled on the text
-   Right - Clipping is enabled on the button.

Take note of the difference it makes when clipping is assigned to different objects. Since the system clips to bounds, things like padding do not factor in here, so if the button is set to clip (right), the contents will run all the way to the edge before it is cut off, whereas if the text is responsible for handling the clipping (center), then the text clips based on things like the button content padding that reduces the space the text has to fit into.

In addition to the simple axis-aligned examples of clipping, the system also supports arbitrary clipping quads that are stacked on top of each other.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c854834b-4da7-4541-a13a-d3de20868072/transformclipping.png)

While this example is extreme, being able to combine multiple arbitrary clipping zones is a prerequisite to being able to introduce 3D transforms and projections, since any widget being clipped with a projection would need to perform clipping in projected space.

## Conversion Guide from 4.16 and Earlier to 4.17 and Later

The changes to the Slate clipping system in 4.17 will break compatibility with previous versions, so you'll want to use the sections below to update your project to avoid any conversion issues and to learn about the new methods you can use to debug Widgets in your project.

### Enabling Clipping of Widgets

For all your UMG Widgets, you can adjust the **Clipping** property located in the **Details** panel of the selected Widget.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f37161ab-bbd7-4e70-8851-70866ea719c6/umgclippingproperty.png)

You can learn more about [Clipping with UMG UI Designer](/documentation/en-us/unreal-engine/clipping-for-umg-widgets-in-unreal-engine) here.

To enable clipping in your code, you'll set the clipping property for `EWidgetClipping` to one of the following states:

-   Inherit
-   ClipToBounds
-   ClipToBoundsWithoutIntersecting
-   ClipToBoundsAlways
-   OnDemand

Here's a code example:

```
	`SNew( SBorder ) 	.Clipping(EWidgetClipping::ClipToBounds) 	[ 		... 	]`
Copy full snippet
```
SNew( SBorder ) .Clipping(EWidgetClipping::ClipToBounds) \[ ... \]

### Deprecated APIs

The following APIs have been deprecated as of 4.16. If your project was using these, consider if you would even need to use them now. Not every Widget clips, so you may no longer need any code that was possibly tricking the clipping system to allow you to move the clipping zone.

-   `FSlateDrawElement::Make___(...)` - there is no longer need to pass a clipping rect into every draw call, so you only need to remove the function call, and you'll automatically be using the new version.
-   `SScissorRectBox` - This is no longer necessary since every axis-aligned clipping rect is now a scissor rect. Make sure to delete these and replace the job it was doing by making its most direct child widget have clipping enabled.

### Custom Clipping

There are cases where you may need to clip internally in your widget. For example, a `SProgressBar` may need to clip the progress bar drawing at arbitrary locations based on its progress. To add your clipping, you would do the following in `OnPaint`:

```
	`OutDrawElements.PushClip(FSlateClippingZone(AllottedGeometry));  	//TODO Do your drawing here, or child widget paint calls.  	OutDrawElements.PopClip();`
Copy full snippet
```
OutDrawElements.PushClip(FSlateClippingZone(AllottedGeometry)); //TODO Do your drawing here, or child widget paint calls. OutDrawElements.PopClip();

The `FSlateClippingZone` is the arbitrary clipping area in window space that can be initialized using several methods that should allow for a straightforward conversion of your existing code.

If you also need your custom clipping to affect Hit Testing, you will need to push your clipping zone onto the Hit Test Grid by setting up the following:

```
	`OutDrawElements.PushClip(FSlateClippingZone(AllottedGeometry)); 	Args.GetGrid().PushClip(FSlateClippingZone(GetCachedGeometry()));  	//TODO Do your drawing here, or child widget paint calls.  	OutDrawElements.PopClip(); 	Args.GetGrid().PopClip();`
Copy full snippet
```
OutDrawElements.PushClip(FSlateClippingZone(AllottedGeometry)); Args.GetGrid().PushClip(FSlateClippingZone(GetCachedGeometry())); //TODO Do your drawing here, or child widget paint calls. OutDrawElements.PopClip(); Args.GetGrid().PopClip();

The clipping rect for the Hit Test Grid is using cached geometry, instead of the AllotedGeometry. In `OnPaint`, `AllotedGeometry` is in window space, while the Hit Test Grid is in desktop space, so you have to use geometry that you'd get in Tick.

### Wrapped Clipping States

In some instances, a widget that has a clipping state isn't going to be responsible for clipping. For example, the `SScrollBox` lets you publically change the clipping state like any other widget, however, when the `SScrollBox` was constructed, it set `bClippingProxy` to `true`. This makes it so that when Slate goes to render that widget, it will ignore its clipping state.

Internally, the `SScrollBox` informs another nested widget that it needs to clip or perform whatever clipping state it was told to do. Additionally, when users change the clipping state, the `SScrollBox` overrides the `SWidget` function called `OnClippingChanged` so that it knows when to mirror the new clipping state to the nested private widgets.

### Culling Changes

Although clipping is performed in render space, the engine still performs culling using a simple bounding box. However, that box is based on the bounding box of the render-transformed clipping zone. Additionally, clipping and culling might become more nuanced over time, so if you have a custom panel and were doing `MyClippingRect.IntersectionWith` to identify and cull widgets that can't possibly be drawn, you should now use the `SWidget` function `IsChildWidgetCulled`. The following is an example of this:

```
	`for (int32 ChildIndex = 0; ChildIndex < ArrangedChildren.Num(); ++ChildIndex) 	{ 		FArrangedWidget& CurWidget = ArrangedChildren[ChildIndex];  		if (!IsChildWidgetCulled(MyCullingRect, CurWidget)) 		{ 			// Paint this widget. 		} 	}`
Copy full snippet
```
for (int32 ChildIndex = 0; ChildIndex < ArrangedChildren.Num(); ++ChildIndex) { FArrangedWidget& CurWidget = ArrangedChildren\[ChildIndex\]; if (!IsChildWidgetCulled(MyCullingRect, CurWidget)) { // Paint this widget. } }

Any place where you're taking in `MyClippingRect` in your OnPaint call should be renamed to `MyCullingRect`.

Even with the changes to the clipping system, Slate's culling approach hasn't changed. In the example below, you'll need to keep in mind that if the parent widget (blue) is culled when outside the clipping zone (green), the child widget (yellow) will also be culled, even if it has a transform that allows it to render entirely outside of the bounds of the parent. This is true even when the clipping property **Clip to Bounds - Without Intersecting** is enabled since the flag would only be checked by the direct parent widget.

![Widgets viewed outside | the clipping zone.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86748d18-484d-4935-9d26-1dd26578ca3b/slate_cullinged.png)

![Widgets culled outside | the clipping zone.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb57156c-62bb-4378-90b7-355ef8e7961d/slate_cullinged2.png)

## Debugging Clipping

The **Widget Reflector** indicates the clipping state for selected Widgets inside the Editor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/853bf869-1abf-44f1-b0d7-3ce793ffcb46/widgetreflector.png)

A text block has been selected using the Widget Reflector that indicates the Clipping state to be set to On Demand.

To open the **Widget Reflector**, navigate to the file menu and select **Window** > **Developer Tools** > **Widget Reflector**.

Below are the available console variables that can be used to debug clipping and culling states for any Widget in the Editor:

| Console Variable | Description |
| --- | --- |
| **Slate.ShowClipping** | 
When enabled, this shows yellow outlines for all axis-aligned clipping rects (Scissor Rects) and red outlines for all stencil clipping quads.

Click image for full size view.



 |
| **Slate.DebugCulling** | When enabled, this helps you to better understand how the culling in a panel is working or why it isn't working correctly. It disables clipping on the GPU, but everything continues as normal, so it enables you to see all the things rendering outside the bounds of clip zones and see if they are being culled when you expect them to be. |
| **Slate.EnableDrawEvents** | When enabled, draw events will be enabled so that when you're debugging with RenderDoc or something similar that it's easier to understand the batches or clipping state transitions. This is enabled by default when using a Debug build. |