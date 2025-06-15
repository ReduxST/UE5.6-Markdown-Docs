# 3D Text Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/3d-text-actor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/3d-text-actor-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:04

---

Add high-resolution **3D Text** to your Level using the geometry-based **Text 3D** Actor. Use 3D Text objects in any project where you need to show clean, high-quality text in the virtual world, such as live broadcasts and virtual sets.

You can use the [Sequencer Editor](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) to animate your 3D text objects, creating motion graphics directly inside the Unreal Editor.

## Enabling the 3D Text Plugin

To use 3D Text, you must first enable the **Text 3D** Plugin.

1.  In the Main Menu Bar, select **Edit > Plugins**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a55ba363-53e2-4673-8d01-6b92e31a2eda/3dtext_editplugins.png)
2.  From the **Text** tab, enable **Text 3D**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/affcc581-d952-41e2-9646-2cf4edc9d200/3dtext_plugin.png) You'll be warned that the Plugin is in an experimental state. Click **Yes**.
    
3.  Click **Restart Now** to use the plugin in your project.
4.  If you have made changes to your project, a window opens where you can save your work before restarting.

## Placing 3D Text in Your Level

1.  In the **Place Actors** panel, select **All Classes**, then **Text 3D**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1267d3a6-c859-4a6c-ab16-8b03f50b8fa9/3dtext_modespanel.png)
2.  Drag and drop the Text 3D Actor into the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71e20332-283d-44b4-9b8a-e65c5ec22459/3dtext_actor.png)
3.  In the viewport, select the Text 3D Actor to view its parameters in the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82f4772b-1378-4573-a03c-a71810082920/3dtext_details.png)

## Text 3D Actor Settings

The following options are available in the **3D Text** section of the **Details** Panel to control the way your 3D text appears.

| Property | Description |
| --- | --- |
| **Text** | 
Enter the text used to create the 3D Text geometry.

Press **Shift+Enter** to create a line break.



 |
| **Extrude** | Set the depth of the geometry: how thick the letters are from front to back. |
| **Bevel** | Set the size of the bevel along the edges of the characters. |
| **Bevel Type** | Set the type of edge bevel: Linear for a sharp, flat bevel, or Half Circle for a rounded edge. |
| **Half Circle Segments** | Set the number of segments used to create the curve for the Half Circle bevel. |
| **Front Material** | Select the Material to use for shading the front surface of the letters. |
| **Bevel Material** | Select the Material to use for shading the surface of the bevel. |
| **Extrude Material** | Select the Material to use for shading the sides of the letters. |
| **Back Material** | Select the Material to use for shading the back of the letters. |
| **Font** | 

Select the True Type (TTF) or Open Type (OTF) font Asset you want to use for the letters.

For more information about getting fonts into your Unreal Engine project, see [Importing Fonts](/documentation/en-us/unreal-engine/importing-fonts-in-unreal-engine).



 |
| **Horizontal Alignment** | Align horizontal text to the Left, Center or Right with respect to the position of the Actor in 3D space. |
| **Vertical Alignment** | Align the text vertically to put the Top Line, Top, Bottom or Center of the letters at the position of the Actor in 3D space. |
| **Kerning** | Set additional space between each character. |
| **Line Spacing** | Set additional space between each line. |
| **Word Spacing** | Set additional space between each word. |
| **Max Width** | Set the maximum width of the text. |
| **Max Height** | Set the maximum height of the text. |
| **Scale Proportionally** | Locks the height and width of the letters to their current ratio. When enabled, any change to either the height or width of the letters applies to both. |

## Animating Letter-by-Letter

You can interpolate the 3D translation, rotation, and scaling of the letters in a Text 3D Actor between configurable starting and ending values. You can set the order in which the animations progress across the letters in the text (left-to-right, right-to-left, from the middle letters out, or from the outer letters in), and how much each letter's animation overlaps with its neighbors. In combination with the [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) tool, this allows you to design dynamic motion graphics that apply animations letter-by-letter.

For example, the following video shows how to apply transforms to the location, scale, and rotation of the letters in a Text 3D Actor, then the effect of using a Level Sequence to animate the transforms over time.

Letter-by-letter animation in a Text 3D Actor is controlled by a **Text3DCharacterTransform** Component. You'll need to add one of these Components to your Actor, and set up its values.

To set up letter-by-letter animation:

1.  Select your Text 3D Actor in the Viewport or the **World Outliner**.
    
2.  In the **Details** panel, click **Add Component** and select **Text3DCharacterTransform**.
    
    ![Add the Text3DCharacterTransform Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5f9d289-8812-4081-82a2-099170ea13e6/text3d-add-transform-component.png "Add the Text3DCharacterTransform Component")
3.  Select the new **Text3DCharacterTransform** at the top of the **Details** panel to access its settings.
    
    ![Select the Text3DCharacterTransform Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d9e45ff-3c5b-40bd-8e06-7493c7c2b615/text3d-select-component.png "Select the Text3DCharacterTransform Component")
4.  Enable the location, rotation, and/or scale transforms, and adjust their settings to produce the animation effect you want. See the table below for a description of each setting.
    
    As you adjust the settings for the location, rotation, or scale transforms, you can drag the **Progress** value back and forth between 0 and 100 to preview the effect.
    
5.  Typically, you will want to use a **Level Sequence** to play back the animation effect you've designed over time. This will usually involve adding your Text 3D Actor to a Level Sequence, creating new tracks for the **Progress** setting, then creating keyframes on those tracks that make the values change between 0 and 100 over time. For example:
    
    ![Animating Progress settings in a Level Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3750ca3c-c094-414d-a6f6-45431d9d5446/text3d-sequence.png "Animating Progress settings in a Level Sequence")
    
    For details on creating a Level Sequence and working in the Sequencer Editor, see the [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) documentation.
    

### Text 3D Character Transform Settings

The **Text3DCharacterTransform** Component exposes the following settings for the 3D location, rotation, and scale of your text. You can control the three types of transform separately.

| Setting | Description |
| --- | --- |
| **Enabled** | 
Determines whether the **Text3DCharacterTransform** Component updates the location, rotation, or scale of the letters based on the values in this section.

Enabling this option adds some extra calculations for the CPU to carry out. Typically, you should only enable this setting for types of transforms that you actually need to animate.



 |
| **Progress** | 

Determines the overall progression of the text animation between the **Begin** and **End** states. At `0`, the location, rotation, or scale of the text is at its **Begin** state. At `100`, the location, rotation, or scale of the text is at its **End** state. Values in between interpolate the location, rotation, or scale proporationately in between the **Begin** and **End** states.

If you create a Level Sequence to animate the letter-by-letter transforms over time, this is typically the setting that you will want to animate in your Level Sequence.



 |
| **Order** | 

Determines the direction in which the animation progresses across the letters in your text.

-   **Normal -** The animation begins with the leftmost letter and progresses to the right.
-   **From Center -** The animation begins with the letters in the center of the text and progresses outward in both directions.
-   **To Center -** The animation begins with the outermost letters of the text and progresses inward toward the letters in the middle.
-   **Opposite -** The animation begins with the rightmost letter and progresses to the left.



 |
| **Range** | Determines how much overlap there is between adjacent letters. At `0`, each letter completes its transformation from the **Begin** state to the **End** state before the next letter begins to transform. At `100`, all letters begin and end their transformations at the same time. Values in between create a partial overlap between each successive pair of letters. |
| **Begin** | 

Sets the desired initial state for the rotation or scale of the letters. All axis values are expressed in the local space of the Text 3D Actor.

For the location, the **Begin** position of each letter is always determined by the position of the Text 3D Actor in the Level.



 |
| **End** or **Distance** | Sets the desired end state for the location, rotation, or scale of the letters. |