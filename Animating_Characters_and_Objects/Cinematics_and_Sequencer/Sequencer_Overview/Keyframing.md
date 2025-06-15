# Keyframing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:14

---

Tracks and content in Sequencer are animated by creating **Keyframes** (also referred to as **Keys**) with defined properties at specific points along the timeline. When the playhead reaches a key in the timeline, the properties are updated to the values defined at those points. Properties can either gradually change (interpolate) between keyframes, or change immediately to the specified value upon reaching the keyframe (no interpolation).

Keyframes and track states reside within grouped containers, called **Sections**. Sections are time ranges in which the track is being evaluated by Sequencer. They can either have an infinite or finite length, and also can be moved, trimmed, or blended.

This guide provides an overview of animation keyframing in Sequencer, and how sections enhance the animation feature set.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).

## Keyframes

Similar to most animation software, objects are animated in Sequencer by creating keyframes within the timeline. Keyframes enable the animation of an object's position, color and other attributes. Most Actor properties can be animated in Sequencer, and therefore also be keyframed.

![keyframe example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ac60f20-6668-4716-b85f-0ddf266cd5e8/keyframes.png)

### Creation

There are a variety of ways to create keyframes in Sequencer. In most cases when a keyframe is created, it will be created at the location of the [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead). If the playhead is at the same location as an existing keyframe when placing a new keyframe, it will be overwritten with the new keyframe.

| Keyframe Creation Method | Image |
| --- | --- |
| Clicking the **Add Key** button on a track. | ![add key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43859ba8-f942-4208-aeea-3ab1c830a7b2/createkey1.png) |
| 
Clicking the **Add Key** button next to a property in the selected Actor's Details panel.

The Actor or track does not need to be added to Sequencer for this to work. If it isn't added, it will automatically be added to Sequencer and keyframed.



 | ![add key details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41c0832d-94bf-4af7-9d9b-0e6dbc1773e5/createkey2.png) |
| 

Pressing **Enter** on your keyboard will place keys on the selected tracks.

If you have an Actor track selected, pressing **Enter** will create keyframes on all keyable child tracks.



 | ![add key enter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97f8d1ef-f332-4ab1-ba7a-630322c959a6/createkey3.gif) |
| Adjusting the property value displayed along the property track will add a new keyframe if the track already contains keyframes. You can either drag the property left and right to scrub its value, or click it and manually type a new value. | ![add key value change](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ba5de76-343b-4657-a7ec-9d01565a7d04/createkey4.gif) |
| Clicking the **middle mouse button** along the track's timeline will create a keyframe at the playhead's position. The keyframe value will match the value at the playhead's position. | ![add key mmb middle mouse](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83f66427-c4d8-4f83-a5d2-dd6d998acb8c/mmbkeyframe.gif) |
| 

Pressing **S** with an Actor selected creates a **[Transform Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine)** (if one does not already exist) and creates a keyframe with its current **Location**, **Rotation** and **Scale** properties.

This command also works if your window focus is on the viewport, mirroring Maya's keyframing hotkeys. It also will automatically add any Actor to Sequencer, if they currently are not being referenced inside your sequence.



 | ![add key s](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5e64d9d-0af8-4b9f-b9c5-635810809b8d/createkey5.gif) |
| Pressing **Shift + W** with an Actor selected creates a Transform track (if one does not already exist) and keyframes the **Location** property only. | ![keyframe location only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fc5153b-dc76-466d-ba2b-83c697db897e/location.png) |
| Pressing **Shift + E** with an Actor selected creates a Transform track (if one does not already exist) and keyframes the **Rotation** property only. | ![keyframe rotation only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b61fcc5-11e1-467d-8c10-3e703f9254d9/rotation.png) |
| Pressing **Shift + R** with an Actor selected creates a Transform track (if one does not already exist) and keyframes the **Scale** property only. | ![keyframe rotation only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/951397b7-98c4-4862-9c48-438bf6d1f88f/scale.png) |

#### Auto Key

Keyframes can also be set up to create automatically whenever you change an Actor's properties, which is known as **Auto Keying**. To use Auto Key, you must enable the [Auto Key](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#autokey) button in the [Sequencer Toolbar](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine).

Once enabled, modifying Actor properties will cause new keyframes to be created.

![sequencer auto option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc012162-eb80-4955-ac86-8befc4fbf5f9/autokey.gif)

The track you are auto keying must already have keyframes present in order to automatically create new keyframes. An empty track will not be auto keyed.

You can also open the [Keyframe Options Menu](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#keyframeoptions) to change the number of keyframes that are automatically created when channel keyframes are being auto keyed. Channel keyframes are property types made up of several properties, such as [Vectors](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#vectors) or [Transform](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#transformtrack).

![auto key settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47b50a74-0835-48f7-bdd5-f8fabc804b25/autokeyoptions.png)

| Auto Key Option | Description |
| --- | --- |
| **Key All** | All channels and groups will be keyframed when a value is changed. For example, in transform, if you only edit the X-Location property of an Actor, then keyframes will be set on the full XYZ **Location** channels as well as all channels in **Scale** and **Rotation**. |
| **Key Group** | All axes within a channel will be keyframed when a value is changed. For example, in transform, if you only edit just the X-Location property of an Actor, then keyframes will be set on the full XYZ **Location** channels. |
| **Key Changed** | Only the axis that changes will be keyed. For example, in transform, if you only edit the X-Location property of an Actor, then only the X-Location channel will be keyframed. |

#### Duplication and Copy Paste

Keyframes can be created by duplication and copy / paste methods. You can duplicate a keyframe by right-clicking it and selecting **Duplicate** or by pressing **Ctrl+D**. Doing this will create a duplicate keyframe at the same location as the original.

You can also duplicate a keyframe by holding **Alt** and dragging a key, or group of selected keys along the timeline.

![keyframe alt copy duplicate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c34c4ab-af76-4590-ae1a-3f4b3721ac6a/altduplicate.gif)

Keyframes can be copied and pasted using standard **Cut** / **Copy** / **Paste** commands. You can either right-click a keyframe and select one of these commands, or use the **Ctrl + X**, **Ctrl + C,** **Ctrl + V** hotkeys on a selected keyframe or group of keyframes. When keyframes are pasted, the left-most keyframe will paste at the same location as the playhead, and the keyframe group (if multiple keys were copied) will be placed relative to that location.

![keyframe copy paste](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2d29279-05de-4382-b92c-51ddd4c00cd7/copypastekeys.gif)

### Selection and Movement

Keyframes are selected by clicking them individually or by dragging a marquee selection around a group of keyframes. Keyframes from other tracks can be included in your selection when using marquee selection, and are highlighted when included within the marquee selection box.

![keyframe selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06b341a7-00ce-4347-a2c3-218a1c33dd51/selectingkeys.gif)

You can change the time of a keyframe by dragging it left and right. Multiple selected keys can also be moved relative to each other.

![move keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fac29fe-8d87-439f-9653-dd1de02b2d5c/movekeys.gif)

By default, the timeline [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead) will automatically snap to a selected keyframe, and will continuously snap to the keyframe while dragging it along the timeline. You can change this behavior by disabling both the **Snap to the Pressed Key** and **Snap to the Dragged Key** settings in the [Snapping](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#snapping) toolbar menu.

Use **Ctrl + \]** and **Ctrl + \[** to select all keyframes to the left or right of the playhead's location.

![select keyframe forward backward](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9671be0-dded-4a73-aabc-361123302df2/selectforwardback.gif)

### Layer Bars

To assist with movement and scaling of multiple keyframes at the same time, you can utilize **Layer Bars** to manipulate your keyframes. When multiple keyframes or sections exist on your Actor or Component, this bar will appear along the header track of the object which you can move and trim.

![sequencer layer bars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef2f772c-fa59-4938-97b3-bb291f815cce/layerbar1.png)

Dragging the center portion of the bar moves all child keyframes and sections in a grouped manner. Dragging the edges will scale the keyframes and sections relative to that edge.

![manipulate layer bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a793ea0c-b3d9-44fd-8f3a-349a77f4668b/layerbar2.gif)

Layer Bars are hierarchical and will appear on lower Component Tracks, and also [Folder Tracks](/documentation/en-us/unreal-engine/organize-cinematic-tracks-in-unreal-engine). Manipulating them at any of these points will appropriately manipulate keys, sections, and other Layer Bars of all Actors within. This makes it easier to manipulate keyframes on your Actors without needing to expand to the tracks to do so.

![layer bar hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca4a0923-f001-4bad-a4c6-2f89ecb3f870/layerbar4.gif)

You can enable or disable this feature by navigating to the **View Options** menu in Sequencer and selecting **Layer Bars**.

![enable or disable layer bars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84a15efb-105d-4671-9b4b-9fa13c6a358e/layerbar3.png)

### Key Bars

If you want to retime neighboring pairs of keyframes, you can select and drag the line drawn between two keyframes. This will move both keyframes relative to each other. This method of manipulating keyframes can be useful to save time from multi-selecting each key individually, and preserving custom curves between these keys.

![maniplate key bars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf18105d-c83a-434b-b5f4-a121579b133f/keybars1.gif)

You can enable or disable this feature by navigating to the **View Options** menu in Sequencer and selecting **Key Bars**.

![enable or disable key bars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dabd06d-65e6-48cc-a7db-c70b1e80296c/keybars2.png)

### Interpolation

Keyframes can either **Interpolate** or **not Interpolate**. Keys that interpolate will gradually change the values of the property they are animating over time, while keyframes that don't interpolate will retain their value until the next keyframe is reached. An example of non-interpolating keyframes would be when keyframes created on an [Event Track](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine), [Boolean Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#boolean), or [Enum Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#enum)

![keyframe interpolation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20e20112-a477-4167-8a3f-dc8ac6a56252/interpolatecompare.png)

1.  **Non-Interpolating Keyframes**: These keyframes are displayed using a **white diamond** shape.
2.  **Interpolating Keyframes**: These keyframes are displayed using a **red circle**, or other colored shape if using different tangents.

Keyframes that interpolate can have their **tangents** adjusted. Tangents are properties on the keyframe that control the speed and easing angle of the interpolation between keyframes. Depending on the tangent type chosen, the keyframe icon will display differently to denote its tangent property

![keyframe tangent type display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f959ec12-b7d1-4408-bd43-4e9f774f0804/tangentkeys.png)

There are five main types of tangents you can select:

| Tangent Name | Keyframe Icon | Description |
| --- | --- | --- |
| **Cubic (Auto)** | ![cubic auto](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c254b553-f6ed-4c6a-9cdc-98fff25d1b2e/cubicauto.png) | The Cubic (Auto) tangent type is the default tangent type. It attempts to maintain a smooth curve between keyframes and eases both the start and end keyframes. It will automatically adjust whenever keyframes are added or moved. |
| **Cubic (User)** | ![cubic user](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2944adbd-e755-44eb-a52f-1fd77765dda0/cubicuser.png) | Cubic (User) is similar to Cubic (Auto), but it will lock the tangent from any further automatic edits when keyframes are added or moved. Cubic (Auto) keyframes will convert to Cubic (User) when manual tangent edits occur within the [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine). |
| **Cubic (Break)** | ![cubic break](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fcace42-5840-47bc-a954-b78ed57e8ef4/cubicbreak.png) | Cubic (User) is similar to Cubic (Auto), but its tangents are **broken**, allowing for different incoming and outgoing angles to be specified from the Curve Editor. |
| **Linear** | ![linear](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3dd70ef-a802-4bc7-a75a-14dec9facecc/linear.png) | Linear tangents cause keyframes to have no smoothing or easing between them, causing abrupt starts and stops when reaching each keyframe. |
| **Constant** | ![constant](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ac74606-b9db-4a5c-b68d-6849f0846245/constant.png) | Constant tangents function similarly to non-interpolating keyframes by maintaining their current value until the next keyframe is reached. |

You can convert an existing keyframe's tangent type by right-clicking it and selecting a tangent type from the **Key Interpolation** menu category.

![change tangent menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d223814e-326d-4c78-be06-ff6bc16f728e/tangenttype.png)

Hotkeys can also be used to change a selected keyframe's tangent. Pressing **1**, **2**, **3**, **4**, or **5** on your keyboard will change the tangent to **Cubic (Auto)**, **Cubic (User)**, **Cubic (Break)**, **Linear**, or **Constant**, respectively.

The default tangent for newly created keyframes can be changed by clicking the [Keyframe Options](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#keyframeoptions) button in the Sequencer toolbar and selecting a tangent type from the **Default Key Interpolation** menu category.

![default tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/962ae093-aca6-4b60-bbde-c2bf22a99906/defaulttangent.png)

### Properties

Right-clicking a keyframe and navigating to the **Properties** menu will display the keyframe's current **Property Values** and **Time**. Depending on the [Property Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine) being animated, the **Properties** menu display will vary according to the property.

![keyframe properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8424ca2d-dd7c-4155-83f3-484ec1f35811/keyframeproperties.png)

There are also keyframe-specific commands you can use to edit your keyframe time.

| Name | Description |
| --- | --- |
| **Set Key Time** | 
Selecting this will cause a new window to appear from which you can specify a new time for the keyframe.

![set key time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b82e344-b5f0-4ca9-8666-53081f61fd7c/setkeytime.png)

 |
| **Rekey** | 

Snaps the keyframe to the [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead).

![rekey](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c0d0573-e0cd-4929-81d8-c935bfd46028/rekey.gif)

 |
| **Snap to Frame** | 

Snaps all selected keyframes to their nearest frame, as defined in the [Frames Per Second](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#framespersecond) toolbar menu.

![snap to frame](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfdba704-b945-4665-b1eb-33d4da930614/snaptoframe.gif)

 |
| **Delete** | Deletes the selected keyframe. |

## Sections

In the context of keyframes and keyframing actor properties, Sections are the groups that contain keyframes. They function similar to animation layers found in other animation tools, but with some differences. While layers usually do not consider time ranges for their keyframes, Sections do, which enable features such as offsetting whole chunks of keyframe data easily, without needing to select and move every keyframe individually. All keyframes reside within sections, either infinite or finite in length.

![sections example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d22d88a-7944-4eef-af79-754180409dd9/sections.png)

Additionally, while keyframes occupy only single frames within the timeline, sections occupy a range of time. As such, any animatable track that produces its content from ranges of time is using Sections. This includes tracks such as the [Animation Track](/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine), [Subsequence Track](/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine), or [Audio Track](/documentation/en-us/unreal-engine/cinematic-audio-track-in-unreal-engine).

![sections example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de7030da-7ac6-486d-9dc1-06c6eb43b324/sections2.png)

### Creation

A section with infinite length is created automatically whenever a keyframable track is created. You can more clearly see this section by right-clicking an empty space of the section, navigating to the **Properties** menu and unlocking the **Section Range Start** and **Section Range End** properties. This will convert the section to a finite length, in order to view and manipulate it.

![create section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d75e4a10-f1b0-45ee-be9d-3cbce9ca5a13/sectioncreation.gif)

Additional sections can be added by clicking the **Section (+)** button on the track. You can choose which [Blend Type](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#blendtypes) to use for this new section. Additional sections created after the initial one will be created with finite range.

![add new section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cef84026-0e18-472d-a67c-769693cdf425/newsection.png)

### Interaction and Display

Finite sections can be moved and resized by dragging them or their edges. You can move them between tracks as well by dragging them up and down in the timeline.

![edit section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c837881-a921-4631-a1fb-f2b4fdcf9d46/sectionmove.gif)

Use **Alt + \]** and **Alt +\[** to trim or loop sections to the current playhead time. If you select the main header track beforehand, then all child sections will trim or loop to the playhead.

![trim section hotkey](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a681f85-2226-411a-a7f9-dde8401e5e8b/trimhotkey.gif)

You can also time scale sections, which will scale the keyframes proportionally to the scale amount. Hold **Ctrl** and drag the edge of a section to timescale a section. Time scaling is denoted by a **clock icon** beside your cursor when holding **Ctrl** and hovering over the left or right edge of a section.

![time scale section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64aeae72-2a84-4a51-9612-9af64c13f7e5/sectiontimescale.gif)

When multiple sections exist on a property, only one of them can receive keyframes (when keyframing by pressing **S** or **Enter**). This section is displayed with a **green outline** around its border to denote that it is the section designated to receive new keyframes. Typically, the most recently created section will be the one receiving keyframes.

![section green outline](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b6313d6-5cd5-46a8-86e0-438646b65a5d/keythissection.png)

You can change which section will receive keyframes by right-clicking a section and selecting **Key This Section**.

![key this section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2b2bd96-36b4-4d77-a097-5100ae7add32/keythissection2.png)

Custom colors can be applied to sections if you want to differentiate them from their default color scheme. To change the color of a section, select the vertical color bar on the track header edge adjacent to the specific section you want to color code. This will open the **Color Picker** where you can select a different color. Click **OK** to apply the new color to the section.

![change section color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da38456a-bb30-4e2d-bc2b-798f358ac052/sectioncolor.png)

### Show Curves

To assist with visualizing your animation data, you can also enable your curves to be displayed in-line on the section. To do this, right-click on a section and select **Curve Channels > Display**, then enable **Show Curve**.

![show curves](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/237cb622-751d-45d3-88a4-c501d6879a9b/showcurves1.png)

You can modify the curve display using the following options in the **Display** menu:

| Name | Description |
| --- | --- |
| **Show Curve** | Enables or disables showing curves in this section. |
| **Key Area Curve Normalized** | If enabled, this adjusts the curves range to display normalized, relative to the height of the track defined by **Key Area Height**. If disabled, curves will show in absolute terms. |
| **Key Area Curve Range** | The range of the curve if **Key Area Curve Normalized** is disabled. |
| **Key Area Height** | The height of the track if **Show Curve** is enabled. You must restart Sequencer for this to update. |

### Data and Evaluation Range

Even without keyframes, Sequencer sections provide a static evaluation of an Actor's properties. This can be useful if you want to set properties on Actors and have Sequencer store them, without needing to set keyframes. This can be done by ensuring your playhead is on the section range for that property (if it is finite), then change the property. You should see the property change between its default level value and the sequencer section when playing or scrubbing over the section boundaries.

![section evaluation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f597268-e706-454d-9efe-a4ae1d458fed/sectioneval1.gif)

You can also blend sections by dragging the top corner edge of a section, which enables the ability to blend any property from its current value to that section's value.

![section evaluation blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84a77a12-b1bf-4108-b886-2bd2f1e6781a/sectioneval2.gif)

### Blending

You can adjust the **start** and **end** blend curves of a section by selecting and moving the blend curve handle located on the upper portion of a section's edge. A curve symbol will appear above the cursor to aid your selection accuracy.

![section blend icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44d98a71-c292-43c2-8d92-8b46a253d56e/blendhandle.png)

Right-clicking a blend curve will reveal the additional context menu commands.

![easing curve blend curve menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1070220d-4958-459d-86ef-73dfd624e1a1/easingcontext.png)

| Name | Description |
| --- | --- |
| **Easing Length** | 
The length of the blend curve. Enabling **Auto** causes the blend curve to return to the default behavior and support automatic length calculation when sections are intersecting.

![blend curve length](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93263b7a-7b2e-4b5e-90fd-9629e9956c2f/easinglength.gif)

 |
| **Method** | **Method** controls the type of curves to apply to the blend, and enables custom external blends based on functions. |
| **Options** | 

The Options menu will display a list of curve shapes that you can apply to your blend curve. Selecting one of these will replace your current curve shape with the selected curve.

![blend curve shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f0f6871-d321-4b80-8335-a332b885309b/curveshapes.png)

 |

Sections can also blend between other sections by dragging them on top of each other. Doing this will blend the resulting keyframe values for the duration of the overlapping region.

![blend sections together](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20c1b078-ecf8-4fbb-832d-8a80f736ebc3/blendsections1.gif)

Sections that overlap show keyframes from only a single section. You can adjust which section's keys are showing by using the **Order** context menu commands to re-order section displays forward or backward.

![section order display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58cb679b-ef3e-4eed-a517-6c16d342cdd1/order.png)

### Blend Types

When creating sections or viewing the **Blend Type** menu, there are different blending modes to apply to your sections. These modes affect how your sections interact with each other, or the value that results from animating a property.

![section blend type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90e82f20-fe5c-43ba-9bcc-d58f17345ca4/blendtype.png)

The following blend types can be chosen:

| Name | Description |
| --- | --- |
| **Absolute** | Sets the property to the absolute value defined by the section or keyframe. If multiple absolute sections are set up to animate the same value, then the value will blend equally between them. |
| **Additive** | Adds the amount defined by the section or keyframe to the current properties. These values stack additively with other sections. |
| **Relative** | Applies this value as a sum total of all other additives and the initial value before animation. |
| **Additive from Base** | The first keyframe of this section will be equal to the current value of the property it is animating at that time. Subsequent keyframes will animate the property relative to that initial point. |

When hovering your cursor over a section with a blend type other than **Absolute**, it will display the blend type name on the section bar.

![section blend type name display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26f00d34-80d1-43b3-b30c-3d414f67fc81/blendtype2.png)

### Properties

Right-clicking a section and navigating to the **Properties** menu will show the section properties.

![section properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9839978-f82f-464f-9531-f17bd7a30560/sectionproperties1.png)

| Name | Description |
| --- | --- |
| **Section Range Start** | The start time of the section. If this region is Locked, then the start time is infinite, and no value is shown. |
| **Section Range End** | The end time of the section. If this region is Locked, then the end time is infinite, and no value is shown. |
| **When Finished** | 
Determines what the property should do when the section finishes.

-   **Keep State** will keep the property in the last animated value, and it will not snap back to its previous value.
-   **Restore State** will return the property back to its state before the section animated it.
-   **Project Default** is the default behavior, and will use the settings defined in your **DefaultEngine.ini** project file. Adding the following lines to the .ini file will set the project default. By default, it is set to Restore State.
    
    `[/Script/LevelSequence.LevelSequence]`
    
    `DefaultCompletionMode=KeepState`
    



 |
| **Timecode Source** | The timecode information for the section, if timecode is being used. You can also specify delta frames here to control offset information. |
| **Is Active** | Activates the selected section. This is similar to [Muting Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#mute), but is used for sections instead of tracks. |
| **Is Locked** | Locks the selected section. This is similar to [Locking Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#mute), but for sections instead of tracks. |

Right-clicking a section and navigating to the **Sections** category reveals section-specific properties and commands.

![sections context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/801304f4-5333-48d7-9d3d-4ca737bb0d45/sectionproperties2.png)

| Name | Description |
| --- | --- |
| **Pre/Post-Infinity** | 
If the section contains keyframes, this menu will display options for selecting what the animation should be doing before the first keyframe (Pre-Infinity), or after the last keyframe (Post-Infinity). These settings affect the animation for the entirety of the section.

-   **Cycle** will repeat the keyframe animation.
-   **Cycle with Offset** will repeat the keyframe animation, but will make each repeating starting keyframe be relative to the starting or ending keyframe value.
-   **Oscillate** will repeat the keyframe animation by mirroring the animation backward and forward with each loop.
-   **Linear** will cause the initial or final keyframe to determine a continuous motion. This may require setting the keyframe tangent type to **Linear**, or setting a custom tangent angle in the [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine).
-   **Constant** is the default behavior and causes the section to maintain the initial or final keyframe value.



 |
| **Order** | When sections with keyframes overlap, keyframes from only one section will display on the timeline. The **Order** menu contains the following controls for sorting which sections are in front or behind. |
| **Blend Type** | Sets the [Blend Type](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#blendtypes) for the selected section. |
| **Active** | Activates the selected section. This is similar to [Muting Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#mute), but is used for sections instead of tracks. |
| **Locked** | Locks the selected section. This is similar to [Locking Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#mute), but for sections instead of tracks. |
| **Group** | 

Links two or more sections together so that when one of the sections moves, they all move together.

![group section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1aa862b1-5e0c-41fb-aea2-04b46074099b/groupsection.gif)

 |
| **Ungroup** | Ungroups the selected section. |
| **Delete** | Deletes the selected section. |
| **Key This Section** | Specifies this section to receive keyframes when keyframing. |
| **Trim Section Left/Right** | Trims the selected section's start or end time to the playhead position. You can also use the **Ctrl + ,** and **Ctrl + .** hotkeys. This command only trims sections and does not add section time like the **Alt + \]** and **\[** commands. |
| **Split Section** | 

Divides the selected section into two parts at the playhead position. If the section contains keyframes, then bracketing keyframes will be created at the split point in order to maintain continuous animation up to the split. You can also use the **Ctrl + /** hotkey.

![split section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a24816c-2553-4b4d-8a5f-abca99350f27/splitsection.gif)

 |
| **Delete Keys** | Deletes keyframes when they fall outside the section range when using the **Trim Section Left/Right** commands. |
| **Auto Size** | Sets the section's start and end times to match to the starting and ending keyframes. This command is not clickable if the section range is infinite, or if there are no keyframes in the section. |
| **Synchronize using Source Timecode** | Synchronizes multiple selected sections using the source timecode. The **first selected section** will be used as the source timecode, and subsequent selected sections will be adjusted according to their source timecode as relative to the first section. |
| **Key Interpolation** | Sets all keyframes in this section to use a specific [Tangent Type](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#interpolation). |
| **Reduce Keys** | Automatically reduces keyframes in the selected section based on the **Tolerance** value. |
| **Tolerance** | Sets how aggressive the automatic removal of keyframes should be when reducing keyframes. Higher values will cause more keyframes to be removed. |