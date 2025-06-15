# UMG Rich Text Block

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-rich-text-blocks-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-rich-text-blocks-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:31

---

The Text Block, provided in Unreal Motion Graphics (UMG), offers a variety of style options and customization. However, you might need a more flexible text block option that supports markup for things like style changes, inline images, hyperlinks, and so on.

The UMG **RichTextBlock** provides a more flexible text block. It supports markup for things like style changes, inline images, hyperlinks, and so on. UMG RichTextBlock accepts decorator classes, which you can write to define the markup behavior you need in your project. Also, page shows the detailed information about properties, you can set to the RichTextBlock Widget and the Data Table Asset with the Rich Image Row and Rich Text Style Row data types.

The Rich Text Block uses a **Data Table Asset** to manage added styles and customization. With the help of the Data Table Asset, you will be able to create your own styles. Also, it allows you to write custom decorator classes, that define the markup behavior you need, in your project. The page shows an example of decorator class, **RichTextBlockImageDecorator**. You can use it as a starting point for experience in writing custom decorator classes.

Get familiar with the content of the page to learn more about the RichTextBlock in UMG, and how you can write custom decorator classes.

## Creating and Assigning a Data Table Asset

At first, you should create a Data Table Asset. With the help of the Data Table Asset, you will be able to create different types of data tags and use it with the RichTextBlock Widget in UMG. You can use the Data Table Asset for specifying text styles or images, that you can use inline with rich text via the RichTextBlock.

Create a Data Table Asset like any other asset: click **Add New** in the **Content Browser**, then select **Miscellaneous > Data Table**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8455bd25-beac-4080-aeec-b3ea43dda03b/01_addnewdta.png)

Select either **Rich Image Row** or **Rich Text Style Row** in **Pick Row Structure** window.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e0a4c7f-6224-4338-826c-d79fe1a6808d/02_createdta_pickstructure.png)

The Rich Image Row uses a custom decorator class, which you can find more details about in the Decorator Classes [Decorator Classes](/documentation/en-us/unreal-engine/umg-rich-text-blocks-in-unreal-engine#decoratorclasses) section.

### Rich Image Row Data Type

As an example, the page shows the Rich Image Row data type, which is a custom decorator class. Store images and set up it with different customization options, using the Data Table Asset with the Rich Image Row data type. Due to this, you can use this data as inline images in the text via the RichTextBlock.

Follow the steps below to create and use the Rich Image Row data type of the Data Table Asset.

1.  Create a Data Table Asset, select the **Rich Image Row** from the drop-down list of the **Pick Row Structure** window. Also, you can rename this Data Table Asset. For example, put the name "Image\_DataTable".
2.  Double-click the created Data Table Asset in the Content Browser to open it in the **Data Table Editor**.
3.  Click **Add** in the Data Table Asset panel to add a new row. Create rows in the Data Table Asset for each inline image, that will be used in your text via the RichTextBlock. There are other instruments for rows at the Data Table Asset panel, like: **Copy**, **Paste**, **Duplicate**, **Remove**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88200686-b560-409a-9355-ddf2a653eb75/04_addrows_dta_imagerowdt.png)
4.  You can change the row name via the text field of the **Row Name** section. It is allowed to use prefixes, camel case, and so on.
5.  Set the properties you need for these images under **Appearance**.
6.  When you have done adding rows, click **Save** and close the Data Table Asset.

See [Properties of the Data Table Asset with Rich Image Row Data Type](/documentation/en-us/unreal-engine/umg-rich-text-blocks-in-unreal-engine#propertiesofthedatatableassetwithrichimagerowdatatype) for more information about these settings.

### Rich Text Style Row Data Type

The Rich Text Style Row data type is the default decorator class. With the help of this, you can set text styles, that can be applied to the text via the RichTextBlock.

Follow the steps below to create and use the Rich Text Style Row data type of the Data Table Asset.

1.  Create a Data Table Asset, select the **Rich Text Style Row** from the drop-down list of the Pick Row Structure window. Also, you can rename this Data Table Asset. For example, put the name "TextStyle\_DataTable".
2.  Double-click the created Data Table Asset in the Content Browser to open it in the Data Table Editor.
3.  Click **Add** in the Data Table Asset panel to add a new row. Create rows in the Data Table Asset for each text style, that will be used in your text via the RichTextBlock. There are other Instruments for rows at the Data Table Asset panel, like: **Copy**, **Paste**, **Duplicate**, **Remove**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64e2b3ef-a2c7-42ce-b2ee-bc72ffe9eee2/06_addrows_dta_textstylerowdt.png)
4.  You can change the name of each row in the text field of the Row Name section. It is allowed to use prefixes, camel case, and so on.
    
    It is recommended to rename the first row of the Data Table Asset to "Default". Due to this, you have defined style of this row as the default style for text in the assigned RichTextBlock.
    
5.  Set the properties you need for these styles under Appearance.
6.  When you have done adding rows, click Save and close the Data Table Asset.

See [Properties of the Data Table Asset with Rich Text Style Row Data Type](/documentation/en-us/unreal-engine/umg-rich-text-blocks-in-unreal-engine#propertiesofthedatatableassetwithrichtextstylerowdatatype) for more information about these settings.

For correct display of the text, it is necessary to set the font in the Data Table Asset for each Rich Text Style Row. Open Data Table Editor. You should select the text row you want to customize, then go on **Appearance > Text Style > Font** section of the Row Editor. In new window you need click **Gear** and enable **Show Engine Content**. With the help of this you will be able to choose **Roboto** font or another one you want.

## Using Rich Text Block Widgets in UMG UI Designer

You should assign the RichTextBlock widget with the created Data Table Asset. Due to this, you will be able to use configured text styles and inline images from the Data Table Asset via the **Designer Viewport**.

### Add a Rich Text Block Widget

Create a Widget Blueprint: click **Add New** in the Content Browser, then select **User Interface > Widget Blueprint**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56dabddc-f4f7-4331-91fe-4cc998366414/08_createwidgetblueprint.png)

You should find a **Canvas Panel** in the **Palette** panel on the left side. Drag the Canvas Panel into the Designer Viewport. Find a **RichTextBlock** in the Palette panel, drag this widget into the Canvas Panel box of the Designer Viewport. You can scale or resize the RichTextBlock box for your needs.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6ef906f-fd66-4310-b2a1-c62286dde975/09_addrichtextblocktowb.png)

The text box does not scale automatically to fit the text size. If you do not resize the box to fit your text size, some of your text may be clipped and not display properly. Also, you can enable the checkbox of the section **Set to Content** in the Details panel for automatic resizing text box to content.

### Assign a Data Table Asset to a Rich Text Block

Select the added RichTextBlock widget. With the help of the **Details** panel on the right side, you will be able to assign your Data Table Asset to the RichTextBlock in the Appearance section.

Use the **Text Style Set** to assign your Data Table Asset with Rich Text Style Rows to the RichTextBlock.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e0fd09a-ed7e-47a9-bff9-d8ed6efd4232/10_assigndttortb.png)

### Apply Style to Text

You should assign the Data Table Asset to the RichTextBlock as described before. Follow the steps below to apply the styles from your Data Table Asset to the text.

1.  Select RichTextBlock.
2.  Find the **Content** section of the Details panel on the right side.
3.  Type your text into the text field of the **Text** section.

The display text has a style from the row of the Data Table Asset with name "Default". For example, if you typed to the text field "This is some rich text!", it would display with the style you customized in "Default" row of the Data Table Asset.

You can change default text style for the RichTextBlock you defined in the Data Table Asset. Enable the checkbox of the section **Override Default Style** in the Details panel. Due to this you will be able to customize new default text style in **Default Text Style Override** section.

In case you need another style from your Data Table Asset, type the name of the style row in enclosed brackets, using the markup `<TextStyleRowName>text</>` (where *"TextStyleRowName"* is the text style Row Name of the Data Table Asset you assigned, *"text"* – part of text you want to have style from specified row). For example: `This is some <RichText.Emphasis>rich</> text!` You can apply different styles for different parts of your text.

T I P: The row name tag in the RichTextBlock is case insensitive to the Data Table Asset rows name.

## Decorator Classes

You can include something other than style to your text by using the **Decorator Classes**. When you create a Decorator Class, you can set up your own markup tags. With the help of this, you will be able to use [Slate](/documentation/en-us/unreal-engine/slate-user-interface-programming-framework-for-unreal-engine). It allows you to render other elements seamlessly within your text.

### Using Decorators

As an example, the page shows how to include inline images into the text via **RichTextBlockImageRowDecorator** class. This example helps you to get start using custom decorator classes.

You need to have the created Data Table Asset with Rich Image Row data type (see [Creating and Assigning a Data Table Asset](/documentation/en-us/unreal-engine/umg-rich-text-blocks-in-unreal-engine#creatingandassigningadatatableasset) section above), and subclass **Blueprint Class** with RichTextBlockImageRowDecorator **Parent Class** as a blueprint to configure the instance. Follow the steps below to do this:

1.  Create a new Blueprint class: click **Add New** in the Content Browser, then select **Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee68f1dc-fd6f-4b14-901d-08f1e391e605/13_createblueprintclass.png)
2.  Choose **RichTextBlockImageRowDecorator** in the **Pick Parent Class** window and click **Select**.
    
3.  Double-click the created Blueprint Class in the Content Browser to open it in the **Blueprint Editor**.
4.  Assign this Blueprint Class to the Data Table Asset with Rich Image Row data type via the **Image Set** with the help of the Details panel on the right side.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d31e47cd-e52e-406b-a455-d6a39733e774/15_assigndtatobc.png)

Having done everything listed above, you are able to add the Decorator Class to your RichTextBlock Widget. Follow the steps below for using inline images from Data Table Asset in your text.

1.  Open your Widget Blueprint.
2.  Find **Decorator Classes** section under Appearance in the Details panel on the right side.
3.  Click **(+)** button for adding array element to the Decorator Classes.
4.  Choose the created Blueprint Class in drop-down list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7291231a-483e-4904-96cb-6febe9870544/16_adddecoratorclass_to_rtb.png)

For inserting inline images from the Data Table Asset, you should use the markup `<img id="ImageRowName"/>` (where *"ImageNameFromTable"* is the Row Name of Data Table Asset you assigned) in the Content section of Details panel. For example, if you typed to the text field `With <img id="RichText.Logo"/> inline images!` and click **Compile**, it would display text with inline images you customized in the Data Table Asset at the row with the name "RichText.Logo".

### Adding New Decorators

You can define custom decorator classes, that can leverage Slate to add anything you want inline the text. To do this, you should write two classes: `URichTextBlockDecorator` and `FRichTextDecorator`. You should set up these classes. Due to this, you will be able to add your Decorator to any RichTextBlock. Use the Decorator Classes array and your markup to parse text with your Decorator.

`URichTextBlockDecorator` defines a `UObject` to implement `CreateDecorator`, which should return a `SharedPtr` to the `FRichTextDecorator`. Due to this, you can implement any properties and utility functions. Also, you can subclass your Decorator as a Blueprint. It allows to add and use any data you need in RichTextBlock.

Remember, the `RichTextBlockImageDecorator` defines a Data Table property. Anything you want to modify in Blueprints should exist in the `UObject`.

## Setting of the UMG Rich Text Block

This reference section shows the detailed information about properties, you can set to the RichTextBlock Widget and the Data Table Asset with the Rich Image Row and Rich Text Style Row data types.

### Rich Text Block Properties

| Property | Description |
| --- | --- |
| Slot (Canvas Panel Slot) |   |
| **Anchors** | 
This sets the anchor location for the selected widget.

-   **Minimum** - Holds the minimum anchors, left and top.
-   **Maximum** - Holds the maximum anchors, right and bottom.



 |
| **Alignment** | Alignment is the pivot point of the widget. Starting in the upper left at (0,0) and ending in the lower right at (1,1). Moving the alignment point enables you to move the origin of the widget. |
| **Size To Content** | When AutoSize is true, it uses the widget's desired size. |
| **ZOrder** | This indicates the order priority for rendering selected widget. Higher values are rendered last, appearing on top. Lower values rendering first and appearing on the bottom. |
| Content |   |
| **Text** | This is the text to display in the widget. |
| Appearance |   |
| **Text Style Set** | This holds the Data Table Asset, which enables rich text decorators to be used for text and image styles. |
| **Decorator Classes** | This adds the Decorator can be used for selected widget. |
| **Override Default Style** | If sets true, it specifies the default text style for this rich text inline, overriding any default provided in the style set table. |
| **Default Text Style Override** | This sets the text style to apply by default. |
| **Min Desired Width** | This sets the minimum desired size for the text. |
| **Transform Policy** | 

The text transformation policy to apply to this text block.

-   **None** - No transform, just use the given text as-is.
-   **To Lower**\*\* - Convert the text to lowercase for display.
-   **To Upper** - Convert the text to uppercase for display.



 |
| **Justification** | This sets how the text is aligned with the margin. |
| **Margin** | This sets the amount of blank space, left around the edges of the text area. |
| **Line Height Percentage** | This sets the amount each line height is scaled by. |
| Clipping |   |
| **Clipping** | 

Controls how the clipping behavior of this widget works. Normally, content, that overflows the bounds of the widget, continues rendering. Enabling clipping prevents that overflowing content from being seen.

-   **Inherit** - Selected widget does not clip children, it and all children inherit the clipping area of the last clipped widget.
-   **Clip to Bounds** - Selected widget clips content the bounds of this widget. It intersects those bounds with any previous clipping area.

Elements in different clipping spaces can not be batched together, so there is performance costs when clipping is applied. Do not enable clipping, unless a panel actually needs to prevent content from showing up outside its bounds.



 |
| **Overflow Policy** | 

Sets what happens to text, that is clipped and does not fit within the clip rect for this widget.

-   **Clip** - Overflowing text will be clipped.
-   **Ellipsis**\*\* - Overflowing text will be replaced with an ellipsis.



 |
| Wrapping |   |
| **Auto Wrap Text** | If sets true, it wraps the text automatically, based on the computed horizontal space for this widget. |
| **Wrap Text At** | This determines whether text wraps onto a new line when its length exceeds this width. If this value is zero or negative, no wrapping occurs. |
| **Wrapping Policy** | 

The wrapping policy to use:

-   **Default Wrapping** - No fallback, just use the given line-break iterator.
-   **Allow Per Character Wrapping** - Fallback to per-character wrapping if a word is too long.



 |
| Behavior |   |
| **Tool Tip Text** | The tooltip text, that is displayed, when the user hovers the mouse cursor over the widget. |
| **Is Enabled** | This sets whether this widget can be modified interactively by the user. |
| **Visibility** | 

Sets the visibility of this widget.

-   **Visible** - The widget is visible and can interact with the cursor.
-   **Collapsed** - The widget is not visible and takes up no space in the layout. It can never be clicked on, because it takes up no space.
-   **Hidden** - The widget is not visible, but occupies layout space. It is not interactive, because it is hidden.
-   **Not Hit Testable (Self & All Children)** - The widget and its children are visible, but cannot interact with cursor.
-   **Not Hit Testable (Self Only)** - The widget and its children are visible, but cannot interact with cursor. (The same as Not Hit Testable (Self & All Children) but doesn't apply to child widgets.



 |
| **Render Opacity** | This sets the opacity of the widget. |
| **Tool Tip Widget** | The tooltip widget, that is displayed, when the user hovers the mouse cursor over the widget. |
| **Cursor** | 

The cursor to show when the mouse is over the widget.

-   **None** - Causes no mouse cursor to be visible.
-   **Default** - Default arrow cursor.
-   **Text Edit Beam** - Indicates text that can be edited.
-   **Resize Left Right** - Resize horizontal arrows cursor.
-   **Resize Up Down** - Resize vertical arrows cursor.
-   **Resize South East** - Bi-directional forward resize arrow cursor.
-   **Resize South West** - Bi-directional back resize arrow cursor.
-   **Cardinal Cross** - Indicates something is being moved.
-   **Crosshairs** - Indicates precision selection, usually by dragging a selection box around something.
-   **Hand** - Uses the hand cursor with pointing finger.
-   **Grab Hand** - Uses the open hand cursor indicating something can be grabbed.
-   **Grab Hand Closed** - Uses the closed hand cursor indicating something is grabbed.
-   **Slashed Circle** - Cursor indicates the action cannot be completed.
-   **Eye Dropper** - Indicates a color can be selected.



 |
| Render Transform |   |
| **Transform** | 

The render transform of the widget allows for arbitrary 2D transforms to be applied to the widget.

-   **Translation** - The amount to translate the widget in X and Y in Slate Units.
-   **Scale** - The amount of scale to apply to the widget in X and Y.
-   **Shear** - The amount of shear to apply to the widget in X and Y in Slate Units.
-   **Angle** - The degree angle to rotate the widget.



 |
| **Pivot** | The render transform pivot controls the location, about which transforms are applied. This value is a normalized coordinate, about which things, like rotations, will occur. |
| Performance |   |
| **Is Volatile** | If sets true, this prevents the widget, or its child's geometry, or layout information, from being cached. If this widget changes every frame, but you want it to still be in an invalidation panel, you should mark it volatile, instead of invalidating it every frame. It would prevent the invalidation panel from actually ever caching anything. |
| Navigation |   |
| **Left** | 

Defines navigation when using Left:

-   **Escape** - Navigation is allowed to escape the bounds of this widget.
-   **Stop** - Navigation stops at the bounds of this widget.
-   **Wrap** - Navigation wraps to the opposite bound of this object.
-   **Explicit** - Navigation goes to a specified widget.
-   **Custom** - Custom function can determine what widget is navigated to, when itself or its children are navigated away from. Applied when the itself or any children are navigated from.
-   **Custom Boundary** - Custom Function can determine what widget is navigated to. Applied when the boundary is hit.



 |
| **Right** | 

Defines navigation when using Right:

-   **Escape** - Navigation is allowed to escape the bounds of this widget.
-   **Stop** - Navigation stops at the bounds of this widget.
-   **Wrap** - Navigation wraps to the opposite bound of this object.
-   **Explicit** - Navigation goes to a specified widget.
-   **Custom** - Custom function can determine what widget is navigated to, when itself or its children are navigated away from. Applied when the itself or any children are navigated from.
-   **Custom Boundary** - Custom Function can determine what widget is navigated to. Applied when the boundary is hit.



 |
| **Up** | 

Defines navigation when using Up:

-   **Escape** - Navigation is allowed to escape the bounds of this widget.
-   **Stop** - Navigation stops at the bounds of this widget.
-   **Wrap** - Navigation wraps to the opposite bound of this object.
-   **Explicit** - Navigation goes to a specified widget.
-   **Custom** - Custom function can determine what widget is navigated to, when itself or its children are navigated away from. Applied when the itself or any children are navigated from.
-   **Custom Boundary** - Custom Function can determine what widget is navigated to. Applied when the boundary is hit.



 |
| **Down** | 

Defines navigation when using Down:

-   **Escape** - Navigation is allowed to escape the bounds of this widget.
-   **Stop** - Navigation stops at the bounds of this widget.
-   **Wrap** - Navigation wraps to the opposite bound of this object.
-   **Explicit** - Navigation goes to a specified widget.
-   **Custom** - Custom function can determine what widget is navigated to, when itself or its children are navigated away from. Applied when the itself or any children are navigated from.
-   **Custom Boundary** - Custom Function can determine what widget is navigated to. Applied when the boundary is hit.



 |
| **Next** | 

Defines navigation when using Next:

-   **Escape** - Navigation is allowed to escape the bounds of this widget.
-   **Stop** - Navigation stops at the bounds of this widget.
-   **Wrap** - Navigation wraps to the opposite bound of this object.
-   **Explicit** - Navigation goes to a specified widget.
-   **Custom** - Custom function can determine what widget is navigated to, when itself or its children are navigated away from. Applied when the itself or any children are navigated from.
-   **Custom Boundary** - Custom Function can determine what widget is navigated to. Applied when the boundary is hit.



 |
| **Previous** | 

Defines navigation when using Previous:

-   **Escape** - Navigation is allowed to escape the bounds of this widget.
-   **Stop** - Navigation stops at the bounds of this widget.
-   **Wrap** - Navigation wraps to the opposite bound of this object.
-   **Explicit** - Navigation goes to a specified widget.
-   **Custom** - Custom function can determine what widget is navigated to, when itself or its children are navigated away from. Applied when the itself or any children are navigated from.
-   **Custom Boundary** - Custom Function can determine what widget is navigated to. Applied when the boundary is hit.



 |
| Localization |   |
| **Force Direction Preference** | 

Use it for set up a new flow direction.

-   **Inherit** - Inherits the flow direction, that set by the parent widget.
-   **Culture** - Begins laying out widgets. It uses the current cultures layout direction preference, flipping the directionality of flows.
-   **Left to Right** - Forces a Left to Right layout flow.
-   **Right to Left** - Forces a Right to Left layout flow.



 |
| **Text Shaping Method** | 

It determines text shaping method, that used within selected widget. When unset, the default is used that is set by Get Default Text Shaping Method.

-   **Auto** - Automatically picks the fastest possible shaping method (either KerningOnly or FullShaping), based on the reading direction of the text. Left-to-right text uses the KerningOnly method. Right-to-left uses the FullShaping method.
-   **Kerning Only** - Provides fake shaping using only kerning data. This can be faster than full shaping, but won't render complex right-to-left or bi-directional glyphs (such as Arabic) correctly. It can be useful as an optimization, when you know your text block will only show simple glyphs (such as numbers).
-   **Full Shaping** - Provides full text shaping, allowing accurate rendering of complex right-to-left or bi-directional glyphs (such as Arabic). It will perform ligature replacement for all languages (such as the combined "fi" glyph in English).



 |
| **Text Flow Direction** | 

It determines flow direction, that used within selected widget. When unset, the default is used that is set by Get Default Text Flow Direction.

-   **Auto** - Automatically detect the flow direction for each paragraph from its text.
-   **Left to Right** - Force text to be flowed left-to-right.
-   **Right to Left** - Force text to be flowed right-to-left.



 |

### Properties of the Data Table Asset with Rich Image Row Data Type

Set the following properties in the Data Table Asset to control the style for images, that used with a RichTextBlock widget.

| Property | Description |
| --- | --- |
| **Image** | The image to render for this brush. The assigned Asset can be a UTexture, UMaterialInterface, or an object implementing the AtlasedTextureInterface. |
| **Image Size** | The size of the resource in Slate Units. |
| **Tint** | Tinting applied to the image. |
| **Draw As** | 
How to draw the image.

-   **None**\- Don't do anything.
-   **Box** - Draw a 3x3 box, where the sides and the middle stretch based on the Margin.
-   **Border** - Draw a 3x3 border, where the sides tile and the middle is empty.
-   **Image** - Draw an image; the margin is ignored.
-   **Rounded Box**\- Draw a solid rectangle wuth an outline and corner radius.



 |
| **Tiling** | 

How to tile the image in Image mode.

-   **No Tile** - Just stretch.
-   **Horizontal** - Tiles the image horizontally.
-   **Vertical** - Tiles the image vertically.
-   **Both** - Tiles the image in both directions.



 |
| **Preview** | 

Sets how the image should be displayed in the preview box.

**Horizontal Alignment:**

-   **Fill** - The image will fill the preview box horizontally.
-   **Left** - The image will be aligned to the left of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Right** - The image will be aligned to the right of the preview box.

**Vertical Alignment:**

-   **Fill** - The image will fill the preview box vertically.
-   **Top** - The image will be aligned to the top of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Bottom** - The image will be aligned to the bottom of the preview box.



 |

### Properties of the Data Table Asset with Rich Text Style Row Data Type

Set the following properties in the Data Table Asset to control the style for text, that used with a RichTextBlock widget.

| Property | Description |
| --- | --- |
| Font |   |
| **Font Family** | The font object (valid when used from UMG or a Slate widget style asset). |
| **Typeface** | The name of the font to use from the default typeface. If None is initially selected, the first entry (Bold) will be used. |
| **Size** | The font size is a measure in point values. The conversion of points to Slate Units is done at 96 dpi. So, if you are using a tool like Photoshop to prototype layouts and UI mock ups, be sure to change the default dpi measurements from 72 dpi to 96 dpi. |
| **Font Material** | The material to use when rendering this font. |
| **Outline Settings** | 
Settings for applying an outline to a font.

-   **Outline Size** - Size of the outline in Slate Units (at 1.0 font scale, this unit is a pixel).
-   **Separate Fill Alpha** - If sets true, the outline will be completely translucent where the filled area will be. It allows for a separate fill alpha value to be used. The trade off when enabling this is slightly worse quality for completely opaque fills, where the inner outline border meets the fill area.
-   **Apply Outline to Drop Shadows**\- If sets true, the outline will be applied to any drop shadow, that uses this font.
-   **Outline Material**\- Sets optional material to apply to the outline.
-   **Outline Color** - The color of the outline for any character in this font.



 |
| **Color** | The color and opacity of this text. |
| **Shadow Offset** | It sets how much should the shadow be offset. An offset of 0 implies no shadow. |
| **Shadow Color and Opacity** | The color and opacity of the shadow. |
| **Shadow Background Color** | The background color of selected text. |
| **Highlight Color** | The color of highlighted text. |
| **Transform Policy** | The Text Transform Policy (defaults to None). |
| **Overflow Policy** | Determines what happens to text that is clipped and does not fit within the clip rect of a text widget. |
| Highlight Shape |   |
| **Image** | The image to render for this brush. The assigned Asset can be a UTexture, UMaterialInterface, or an object implementing the AtlasedTextureInterface. |
| **Image Size** | The size of the resource in Slate Units. |
| **Tint** | Tinting applied to the image. |
| **Draw As** | 

How to draw the image.

-   **None**\- Don't do anything.
-   **Box** - Draw a 3x3 box, where the sides and the middle stretch based on the Margin.
-   **Border** - Draw a 3x3 border, where the sides tile and the middle is empty.
-   **Image** - Draw an image; the margin is ignored.
-   **Rounded Box**\- Draw a solid rectangle wuth an outline and corner radius.



 |
| **Tiling** | 

How to tile the image in Image mode.

-   **No Tile** - Just stretch.
-   **Horizontal** - Tiles the image horizontally.
-   **Vertical** - Tiles the image vertically.
-   **Both** - Tiles the image in both directions.



 |
| **Preview** | 

Sets how the image should be displayed in the preview box.

**Horizontal Alignment:**

-   **Fill** - The image will fill the preview box horizontally.
-   **Left** - The image will be aligned to the left of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Right** - The image will be aligned to the right of the preview box.

**Vertical Alignment:**

-   **Fill** - The image will fill the preview box vertically.
-   **Top** - The image will be aligned to the top of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Bottom** - The image will be aligned to the bottom of the preview box.



 |
| Strike Brush |   |
| **Image** | The image to render for this brush. The assigned Asset can be a UTexture, UMaterialInterface, or an object implementing the AtlasedTextureInterface. |
| **Image Size** | The size of the resource in Slate Units. |
| **Tint** | Tinting applied to the image. |
| **Draw As** | 

How to draw the image.

-   **None**\- Don't do anything.
-   **Box** - Draw a 3x3 box, where the sides and the middle stretch based on the Margin.
-   **Border** - Draw a 3x3 border, where the sides tile and the middle is empty.
-   **Image** - Draw an image; the margin is ignored.
-   **Rounded Box**\- Draw a solid rectangle wuth an outline and corner radius.



 |
| **Tiling** | 

How to tile the image in Image mode.

-   **No Tile** - Just stretch.
-   **Horizontal** - Tiles the image horizontally.
-   **Vertical** - Tiles the image vertically.
-   **Both** - Tiles the image in both directions.



 |
| **Preview** | 

Sets how the image should be displayed in the preview box.

**Horizontal Alignment:**

-   **Fill** - The image will fill the preview box horizontally.
-   **Left** - The image will be aligned to the left of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Right** - The image will be aligned to the right of the preview box.

**Vertical Alignment:**

-   **Fill** - The image will fill the preview box vertically.
-   **Top** - The image will be aligned to the top of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Bottom** - The image will be aligned to the bottom of the preview box.



 |
| Underline Brush |   |
| **Image** | The image to render for this brush. The assigned Asset can be a UTexture, UMaterialInterface, or an object implementing the AtlasedTextureInterface. |
| **Image Size** | The size of the resource in Slate Units. |
| **Tint** | Tinting applied to the image. |
| **Draw As** | 

How to draw the image.

-   **None**\- Don't do anything.
-   **Box** - Draw a 3x3 box, where the sides and the middle stretch based on the Margin.
-   **Border** - Draw a 3x3 border, where the sides tile and the middle is empty.
-   **Image** - Draw an image; the margin is ignored.
-   **Rounded Box**\- Draw a solid rectangle wuth an outline and corner radius.



 |
| **Tiling** | 

How to tile the image in Image mode.

-   **No Tile** - Just stretch.
-   **Horizontal** - Tiles the image horizontally.
-   **Vertical** - Tiles the image vertically.
-   **Both** - Tiles the image in both directions.



 |
| **Preview** | 

Sets how the image should be displayed in the preview box.

**Horizontal Alignment:**

-   **Fill** - The image will fill the preview box horizontally.
-   **Left** - The image will be aligned to the left of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Right** - The image will be aligned to the right of the preview box.

**Vertical Alignment:**

-   **Fill** - The image will fill the preview box vertically.
-   **Top** - The image will be aligned to the top of the preview box.
-   **Center** - The image will be positioned in the center of the preview box.
-   **Bottom** - The image will be aligned to the bottom of the preview box.



 |