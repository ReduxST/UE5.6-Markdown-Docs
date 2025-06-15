# Curve Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:01

---

When you want more control over the way your objects are animated, the Curve Editor can be used to modify and fine-tune your keyframes. Using the Curve Editor's graph, you can create new keyframes, edit tangents, and use various built-in tools to adjust your animation curves.

The Curve Editor is used in other tools across the Unreal Editor, such as [Niagara](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine), Curve Assets, and [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine). This guide provides an overview of how to use the Curve Editor within Sequencer, however, many of the features and functions shown will still be compatible within other areas of the editor as well.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).
-   You have an understanding of [Keyframing in Sequencer](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine).

## Curve Editor Overview

The Curve Editor can be opened from Sequencer by clicking the **Curve Editor** button in the [Sequencer Toolbar](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine).

![open curve editor sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/626a97a0-44f3-430d-9f77-0cd9e819f0ba/opence.png)

Once the Curve Editor is opened, you will see the following view:

![curve editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e559b3cc-c08c-49a3-8609-cfdfe0c70fab/ceoverview.png)

1.  [Toolbar](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#toolbar)
2.  [Outliner](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#outliner)
3.  [Graph](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#graph)

### Toolbar

The Curve Editor Toolbar contains various commands, tools, and options. These can be found listed in the table below.

![curve editor toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73cb4e90-c230-4c96-bb70-ba80d9876d1e/toolbar.png)

| Name | Icon | Description |
| --- | --- | --- |
| **Save** | ![save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b62436a-19ee-4691-b2c4-f8646a4407e9/toolbarsave.png) | Saves the current sequence and any subscenes or shots. |
| **View Modes** | ![view mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c70c411-05f5-47cd-affc-78c4acfd0be7/toolbarviewmode.png) | Opens a dropdown menu for the Curve Editor [View Modes](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#viewmodes). |
| **Zoom to Fit** | ![zoom to fit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70f5720e-e653-4297-a573-746b43022a4a/toolbarzoomfit.png) | Frames and zooms in on the selected keyframes. If no keyframes are selected, then all viewable keyframes within the Graph view will be framed. You can also use the **F** hotkey for this command. |
| **Focus Playhead** | ![focus playhead](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23ed911d-88fe-428d-9913-e0392b143cea/toolbarzoomplayhead.png) | Focuses the graph view on the [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead) without changing zoom level. You can also use the **A** hotkey for this command. |
| **Zoom to Playback Range** | ![zoom to playback range](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78583c6b-f8cf-41d7-94dd-2f91c22fa160/toolbarzoomplayback.png) | Focuses the graph view so that all keyframes are visible, including the start and end frames of the sequence. |
| **Curve Options** | ![curve options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/556d0c07-6ee2-409c-921d-174edc6bb69b/toolbarcurveoptions.png) | 
Opens a menu where you can set the following commands:

-   **Tangent Visibility**, which controls how [Tangents](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#editing%20tangents) are drawn in the graph. You can choose from:
    
    -   **All Tangents**, which causes all keyframes to display their tangents, regardless of whether they are selected or not.
    -   **Selected Keys**, which only displays tangents on selected keyframes.
    -   **No Tangents**, which disables all drawing of tangents.
    
-   **Auto Frame Curves**, which causes automatic framing and zooming of all visible keyframes on a curve when it is selected from the [Outliner](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#outliner).
-   **Snap Time to Selection**, which moves the Playhead to the selected keyframe's time. If multiple keyframes are selected, the Playhead moves to the left-most keyframe.
-   **Buffered Curves**, which enables or disables drawing [buffered curves](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#buffercurves) in the graph.
-   **Curve Tooltips**, which shows a tooltip for a curve's name, time, and value when hovering your cursor over it in the graph.
    
    ![curve tooltips](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db6a2c99-ce8c-4ab0-a19d-32a6a6eb062b/curvetooltip.png)
    



 |
| **Time and Value Fields** | ![time and value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44df9902-bdde-4ebf-a11d-b56024051f9f/toolbarvalues.png) | These property fields display the **Time** and **Value** of the selected keyframe. You can edit these properties directly by typing in new values. |
| **Selection Mode** | ![select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a15a9263-fbc3-4ca7-a838-c67950200153/toolbarselect.png) | Enables normal keyframe and tangent selection and editing. You can also use the **Q** hotkey for this command. |
| **Transform Mode** | ![transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f11178ef-1d22-4e88-93be-ad4bc377ed96/toolbartransform.png) | Enables the [Transform Tool](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#transformtool) for editing keyframes. You can also use the **Ctrl + T** hotkey for this command. |
| **Retime Mode** | ![retime](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9d553a5-f211-4451-af21-6795812e6608/toolbarretime.png) | Enables the [Retime Tool](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#retimetool), which activates a lattice manipulation mode for adjusting keyframe times. You can also use the **Ctrl + E** hotkey to enable this command. |
| **Multi Select Mode** | ![multi select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10e1a34b-a2db-43d4-ac51-a37d22307b61/toolbarmultiselect.png) | Enables the [Multi Select Tool](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#multiselecttool), which activates a scaling mode for selected groups of keyframes based on an adjustable pivot. You can also use the **Ctrl + M** hotkey to enable this command. |
| **Time Snapping** | ![time snap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdc680b5-c7d5-4eeb-8114-69b6a1fffbe3/toolbartimesnap.png) | 

Enables keyframe [snapping](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#snapping) on horizontal (time) increments in the graph.

The snap increments are based on Sequencer's [Frames Per Second](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#framespersecond) if you are using the Curve Editor from Sequencer. Otherwise, you can click the nearby dropdown menu to select a custom time-based snapping increment.

![curve editor time snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72b6ba4a-7efc-46d3-9e05-1d9c3ce6bae9/timesnapping.png)

 |
| **Value Snapping** | ![value snap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c87deca-08af-45d4-9aca-44d1b5cb69e4/toolbarvaluesnap.png) | 

Enables keyframe [snapping](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#snapping) on vertical (value) increments in the graph. You can select the nearby dropdown menu to select a custom value-based snapping increment, as well as adjust the display of the graph lines.

![curve editor value snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48650b2b-d3fc-4e88-8552-fe1f0c40ed32/valuesnapping.png)

 |
| **Lock Axis** | ![lock axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e83c4a6-b116-4255-8021-c5b672b720b1/toolbaraxis.png) | 

Opens a dropdown menu for selecting which axis to lock keyframe movements to.

-   **Both** is the default value and allows keyframe movement in all directions in the graph.
-   **X Only** restricts keyframe movement along the horizontal (time) axis only.
-   **Y Only** restricts keyframe movement along the vertical (value) axis only.



 |
| **Cubic (Auto) Tangent** | ![auto tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e12b6d3f-67e8-4226-b3ac-1368d10ee93a/toolbarcubicauto.png) | 

Sets the selected keyframes to interpolate automatically, causing the curve's tangents to adjust based on the location of neighboring keyframes in the graph.

![curve editor cubic auto tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0022570-c278-4f7f-827e-e521dcca75b3/tangentauto.gif)

 |
| **Cubic (User) Tangent** | ![custom tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d43be26c-66c9-4ac5-b0a9-68763a1d1c69/toolbarcubicuser.png) | 

Sets the selected keyframes to use user-defined tangent angles. Whenever you adjust a tangent angle, the keyframe will automatically switch to this mode.

![curve editor cubic user tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/971b9ee8-b315-4390-b785-c1fc3a7aa642/tangentuser.png)

 |
| **Cubic (Break) Tangent** | ![broken tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9eec26d8-b980-4bcd-b0bf-a472d97e39bb/toolbarcubicbroken.png) | 

Sets the selected keyframes tangents to use broken tangent angles, allowing for keyframes that have different incoming and outgoing tangent angles.

![curve editor broken tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17b8ebb4-e704-4d1f-9fe3-50554659e65b/tangentbroken.png)

 |
| **Linear Tangent** | ![linear tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4a5f6f7-612b-4f94-a115-3d466d231bcb/toolbarlinear.png) | 

Sets the selected keyframes to use linear tangent angles. This causes the incoming and outgoing tangents to always face their respective neighbors, resulting in abrupt changes when reaching each keyframe.

![curve editor linear tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/374165ac-95e2-4bfa-bf6c-cee16d4ff75e/tangentlinear.png)

 |
| **Constant Tangent** | ![stepped tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/183abc8e-2a64-4792-932b-53273d74d3c6/toolbarconstant.png) | 

Sets the selected keyframe to use stepped tangent angles, causing keyframes to maintain their value until reaching the next keyframe.

![curve editor constant tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c837433-a616-4c66-b0d7-122080b943be/tangentconstant.png)

 |
| **Weighted Tangents** | ![weighted tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94251a57-380d-452f-a8fc-9e4c1dc02cd1/toolbarweighted.png) | 

Sets the selected keyframe to use weighted tangent angles, causing tangents to use user-defined lengths which determines the influence that tangent angle exerts over its neighboring keyframe tangents.

![curve editor weighted tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ab0af36-cda6-4298-a609-d69dfa79012e/tangentweight.png)

 |
| **Pre Infinity Settings** | ![pre infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b455076-2ebb-4a83-8e5f-2fe11687a2b0/toolbarpreinfinity.png) | Opens a dropdown menu for selecting the [Pre-Infinity](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#preandpostinfinity) behavior of the selected keyframe or curve. |
| **Post Infinity Settings** | ![post infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61d441c9-8529-433e-a19d-bcb25342cf9d/toolbarpostinfinity.png) | Opens a dropdown menu for selecting the [Post-Infinity](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#preandpostinfinity) behavior of the selected keyframe or curve. |
| **Flatten Tangent** | ![flatten tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb3aab3c-1795-42fa-bf12-8f78122b831c/toolbarflatten.png) | 

Flattens the tangents of the selected keyframes horizontally.

![curve editor flatten tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/574016b2-1bbc-4c2a-ba1f-7f4951a8b51c/tangentflat.png)

 |
| **Straighten Tangent** | ![straighten tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/184df6bd-34dc-4c42-952a-bec0d54e87be/toolbarstraighten.png) | When using **Broken Tangents** on a keyframe, selecting this will straighten the tangent angles, but not unbreak them. The angles will straighten along an average angle between the two broken tangents. |
| **Filter Tool** | ![filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/505837f9-329e-4740-9702-64ff7d75f0cf/toolbarfilter.png) | Opens the [Filter Tool](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#filtertool) window, where you can **bake**, **simplify**, and perform other curve functions. |

### Outliner

The Curve Editor Outliner contains header information for all animatable tracks added to your sequence, as well as a track filter and playback controls.

![curve editor outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8eec432-df76-47a0-8e35-415f409a4151/outliner.png)

Selecting entries from the list automatically filters and frames the [Graph View](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#graph) to only display curves from that selection and any children. You can disable the auto-framing behavior by disabling **Auto Frame Curves** from the **Curve Options** toolbar menu.

![outliner filter selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d1b1dd4-e6c5-4c75-a492-071deb861165/outlinerselectfilter.gif)

You can also use the search bar to search for entries to narrow down the list. Any returned results will also include children tracks.

![outliner search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8cd029d-b6ae-4879-8320-9b87dfd17a28/searchfilter.png)

Contents displayed in the outliner are determined by what tracks you have selected from Sequencer. Selecting tracks in the Sequencer window will cause only the selected tracks to appear in the Curve Editor Outliner. Deselecting all tracks in Sequencer will cause all contents to appear in the Curve Editor.

![outliner sequencer select filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de6a7e70-29d5-408f-86ab-8e57dbacf310/outlinerselectfilter2.gif)

You can disable this selection matching and filtering behavior by disabling **Synchronize Curve Editor Selection** and **Isolate Curve Editor to Selection** in the [Sequencer Editor Preferences](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine) window.

### Graph

The Curve Editor Graph contains a two-dimensional display of your keyframes, and the interpolated curves generated. The graph plots both **Time** and **Value** on the **Horizontal** and **Vertical** axes, respectively, and keyframes are positioned in the graph according to those properties.

![curve editor graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c86c112-2174-4af3-9ba6-ec211dce5415/graph.png)

## Graph Navigation

There are several ways to navigate within the graph, as well as different [View Modes](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#viewmodes) you can use for representing curve data.

### Panning

Use **RMB** to pan the graph view freely.

![graph pan](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffc8317f-cfae-4407-b3e0-008b1ab14071/pan1.gif)

Holding **Shift + RMB** will pan along either the horizontal or vertical axis, depending on the initial direction of your cursor.

![graph pan single axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d239d9cf-b90e-4282-9827-1b66fcc22447/pan2.gif)

Holding **Alt + MMB** will pan only along the horizontal axis.

![graph pan horizontal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6036bf67-2314-4fef-85bf-960a07f34c7e/pan3.gif)

### Zooming

Scrolling the mouse wheel will zoom the graph relative to the [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead).

![graph zoom scroll](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4674546-13c5-4bae-95f7-d4f380582ed4/zoom1.gif)

Holding **Alt + RMB** will smoothly zoom the graph according to your cursor movement. The zoom pivot is relative to your cursor position upon pressing **RMB**.

![graph zoom cursor smooth](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4893227-ca19-4a85-822e-0d4fca7777d2/zoom2.gif)

Holding **Alt + Shift + RMB** will freely zoom the graph according to your cursor movement, which enables scaling time and value axes separately. Moving your cursor up and down will scale the value axis, and moving it left and right will scale the time axis.

![graph zoom free](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98e2bc8c-240a-4825-84b3-5c377d8fdc14/zoom3.gif)

### View Modes

The **View Modes** menu contains different options to visualize your curves.

![curve editor view mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7d5ab10-b664-4175-8706-42c16c4325d3/viewmodes1.png)

**Absolute View Mode** is the default view mode, in which all curves and keyframes are displayed at their exact values in the graph. This mode functions similarly to most animation curve editors.

![absolute view mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83391be3-2a33-41f5-b0a1-b7de4d2bfa2f/viewmodes2.png)

**Stacked View Mode** will separate each curve into its own group, and stack them in the graph. Each group's value range is normalized between **\-1** and **1**.

![stacked view mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4987482-de9f-4675-92c6-3e8126f0e8d2/viewmodes3.gif)

**Normalized View Mode** will display all curve and keyframe values overlapping along a normalized value range of **\-1** and **1**. This view can be useful if you are wanting to universally scale curve amounts proportionally.

![normalized view mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3416d91-1978-4f78-865a-cbaeb8405b8a/viewmodes4.png)

## Curve Editing

The Curve Editor is primarily used for editing your **keyframes** and **tangents**. You can add, remove, or change keyframe locations which affect the curve. You can also edit a keyframe's tangent, and control the incoming and outgoing curve vectors of a keyframe, which also affects the curve. There are also a variety of features and behaviors to help with your editing.

### Editing Keyframes

Keyframes can be moved by using **LMB** and dragging them around the graph. Depending on your **Snap** settings, it should be possible to move a keyframe anywhere along the time and value axes. You can also use **MMB** to move selected keyframes relative to your cursor position. This provides an easier way for manipulating keyframes without needing selection accuracy.

![curve editor move keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3661d48-9536-4bb1-aed5-ab40744e3e30/movekey1.gif)

Holding **Shift** and dragging a keyframe will cause it to lock on either the horizontal or vertical axes as it moves, depending on the initial direction of your cursor.

![move key axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e60feb3c-a16b-4f44-a296-0c4db7220294/movekey2.gif)

Clicking a curve segment will select all keyframes for that curve. With these selected, you can move entire curves by dragging a keyframe or by using **MMB** to move the curve relative to your cursor.

![curve editor move entire curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33d96ae7-349e-4bda-b47d-9617f3320880/movekey3.gif)

### Creating New keyframes

Keyframes can be added along a curve by clicking **MMB** when your cursor is hovered over a curve segment.

![add key to curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3378e5f0-db66-4816-b65d-08fc69139ae9/addkey.gif)

You can also create keyframes without disturbing the curve structure by holding **Ctrl** and clicking **MMB** on any curve segment.

![add key to curve without disruption](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91fec6ae-150d-4241-bd98-1960d3ef768b/create2.gif)

### Copy and Paste

Keyframes can be **cut** (Ctrl + X), **copied** (Ctrl + C), and **pasted** (Ctrl + V) on the same curve and across different curves. There are also certain rules and contexts that determine the paste behavior.

When copying and pasting keys, they will paste at their original value and relative to the [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead). Pasting multiple keys will cause the starting (left-most) keyframe to be placed at the **playhead**, and all other keys relative to that point.

![copy paste curve keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/734f6d56-5686-414b-bd56-d00e1c034204/copypaste1.gif)

Depending on which curve you have selected and filtered in the [Outliner](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#outliner), the paste operation will occur on all curves within the current view.

![copy paste all curves](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdbd9fc8-432d-4337-985d-d2b25c629d7c/copypaste2.gif)

If multiple curves are within the current view and you want to paste on only one of them, you can click the curve segment, which will select all keyframes for that curve, and press **Ctrl + V**.

![copy paste single curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e7315c8-1a75-4ede-aab0-24ae324eac31/copypaste3.gif)

### Editing Tangents

When selecting your keyframes, they will display their **tangent** information. Tangents are lines that control the incoming and outgoing direction of the curve as it reaches the keyframe. You can select either side of the tangent handle and edit them to control the curve trajectory from that keyframe.

![tangents](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e65287a9-44ad-4875-ac9a-de33ebdbf3c8/tangents.png)

Depending on your **Tangent Visibility** settings in the **Curve Options** menu, your tangents may be displayed differently. Ensure this is set to **Selected Keys** for the default behavior.

![tangent visibility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfab5d17-9af8-4ec1-a6be-6a78800a02e6/tangentsettings.png)

To edit a Tangent, first select a keyframe, then select the tangent handle and drag it around in the graph. Similar to moving keyframes, you can also use the **MMB** to move the tangent relative to your cursor position.

![edit tangent curve editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de30026c-f215-40f7-9d31-1fe3948a2976/edittangent1.gif)

Multiple tangents can be adjusted at the same time by multi-selecting them and using **MMB** to edit them.

![edit multiple tangents](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97fecaa5-13e0-43fd-8ff7-29861542ec8f/edittangent2.gif)

If multiple keyframes are selected, clicking a single tangent will select all tangent handles of the same side.

![select all tangent handles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0945323f-d33a-4491-988c-61772904952c/edittangent5.gif)

Holding the **Shift** key while moving your tangents will snap them to the nearest 45 degree increment.

![snap tangent angle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2ef4373-2a30-49e7-a587-8fbc472e3f13/edittangent3.gif)

Various tangent modes are located in the **toolbar**, and can be used to change the tangent angle of the selected keyframe. Reference the [Toolbar](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#toolbar) section in this document to view their behaviors.

![tangent mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95323132-15b5-40fe-ab6a-e5b18f95b2c3/tangentmodes.png)

### Weighted Tangents

With a keyframe selected, clicking the **Weighted Tangents** toolbar button will enable weighted tangent angles. This causes tangents to have user-defined lengths which determines the influence that tangent angle exerts over its neighboring keyframe tangents.

Once **Weighted Tangents** is enabled, you can stretch the tangent to increase its influence on the curve, or shrink it to decrease its influence.

![weighted tangent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80ebf08e-ebb4-4c30-84cc-b3f3001da0fd/edittangent4.gif)

### Buffer Curves

Curves can be temporarily saved and stored (known as buffering), which is useful when making experimental changes to your curves as these curves can be reverted to their stored state. While a curve is buffered, it will display an after-image on the graph for your reference.

To store a curve, right-click a part of the curve segment and select **Buffer Curves**.

![store curves](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c113ebc-524a-4f79-96ed-dad6bd21e09e/storecurve2.png)

After a curve is stored, you can make any edits you want to the curve. Keyframes and tangents can be added, edited, or removed. To revert your curve back to the original stored version, right-click the curve segment and select **Apply 1 Buffered Curves**. Buffered curve data is locked to the curve it is stored on, so you cannot buffer for one curve and then apply that buffered data to a different curve.

![apply stored curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b846fb20-45f7-4635-8de5-83934e34847f/storecurve3.gif)

You can also **Swap** your curves, which restores the curve but also stores the changes you just made. To do this, right-click the curve and select **Swap Buffered Curves onto Selected Curves**.

![swap buffered curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/205ec306-acf4-459b-8e8a-a3ad836004a9/storecurve6.gif)

Stored curves are lost whenever you close the Sequencer window.

### Pre and Post Infinity

Curves also contain rules for how they should behave in the timeframes before and after their keyframe segments. This is known as **Pre** and **Post Infinity**, and can be useful in order to extend the animation on a curve without needing to create additional keyframes. **Pre-Infinity** affects the curve region before the first keyframe, and **Post-Infinity** affects the curve region after the last keyframe.

![pre post infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4fdf7ed-0a64-4219-b389-0c8dac51f516/infinity1.png)

You can access the Pre and Post Infinity settings for your curves by clicking the **Pre** or **Post Infinity** buttons in the [**Toolbar**](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#toolbar), or by right-clicking a curve segment and selecting **Pre-Infinity** and **Post-Infinity**. Both methods require you have a keyframe selected from the curve you want to adjust .

![pre post infinity menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f9847d7-4422-4685-baf5-cd47af2b5461/infinity2.png)

You can choose from the following infinity types:

| Name | Description |
| --- | --- |
| **Constant** | 
This is the default value for all new curves, and will cause the curve to retain its value leading up to the first key, and after the final key.

![constant infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa311470-c7d4-4e04-8ba2-42bffb1e21dc/constant.png)

 |
| **Cycle** | 

The curve will repeat, using the absolute values of the keyframes for each loop segment.

![cycle infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e8baa2d-226c-4822-9c82-78b52da860c2/cycle.png)

 |
| **Cycle with Offset** | 

Similar to **Cycle**, the curve will repeat, however each loop segment's value will be set relative to the previous, causing the curve to compound for each loop.

![cycle with offset infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce1d3201-89a8-4a58-935f-72bcb618e557/cycleoffset.png)

 |
| **Linear** | 

The curve will project the first and last keyframe's tangent angle outward.

![linear infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50fc1aa1-167b-4261-a68e-2f0404e0d3b7/linear.gif)

 |
| **Oscillate (Ping Pong)** | 

Similar to **Cycle**, the curve will repeat, however each loop segment will mirror the previous, going backward and forward for each loop.

![oscillate ping pong infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a97bc02c-a728-47fd-b048-bad4646c293a/oscillate.png)

 |

For looping-based infinity modes, such as Cycle and Oscillate, the loop length is defined by the number of keyframes used. Therefore, it will adjust as you add or adjust the length of your keyframe segments.

![cycle length infinity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c455824-fd0d-452a-b436-781ad51eaeb2/infinity3.gif)

### Custom Curve Colors

If you want to alter the displayed color of a curve, which can be useful when you want to visually differentiate property curves, you can use the following commands from the **Curve Options** toolbar menu:

-   **Set Random Curve Colors**, which applies a random color to all visible curves.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15449949-6328-4ddf-990e-3db56ae6bee5/curvecolor1.gif)
    
-   **Set Curve Color For Selected**, which opens a Color Picker where you can apply a specific color to a curve. Select a color and click **OK** to apply the color to the curve.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b73855b9-6a91-48a0-8714-dfb1f65c8e92/curvecolor2.gif)
    

Custom curve colors are saved on the specific property or channel curve, enabling them to be re-used throughout your project. To view or change curve color data, open **Editor Preferences** by clicking **Edit > Preferences** in the main Unreal Engine menu. Navigate to the **Content Editors > Curve Editor** section and locate the **Custom Colors** property array. Here you can add, edit, or remove custom color data. Deleting entries will restore the default color for that curve.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0e36a6c-2534-49eb-a0f0-4b17aa18c03f/curvecolor3.png)

## Curve Tools

When editing curves, **Selection Mode** is the default behavior for interacting with keyframes. There are also a variety of other tools you can enable to assist in scaling, transforming, and warping your keyframes.

![curve editor select mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1ee3bf0-d54e-418a-8929-a13c17063b50/selectmode.png)

### Transform Tool

The Transform Tool enables a lattice interface when you select your keyframes. You can use the various controls on this lattice to adjust your keyframes' times and values.

To activate the Transform Tool, click the **Transform Tool** button in the toolbar, then select multiple keyframes.

![curve editor transform tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17f3fb9d-c849-450c-90e2-43744e1cd172/transformtool1.png)

Various points on the lattice can be manipulated, which scales the entire selection relative to the center point. You can drag the **Corners**, **Edges**, and **Central** areas to adjust the curve.

![transform tool controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76e0e0ae-0e15-43fa-83f2-6b22a031831b/transformtool2.gif)

The pivot point of the transform can also be dragged and changed. It will snap to the edges, corners, and center of the lattice, when moving close to those points.

![transform tool pivot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bc082d0-3010-4468-92dc-b00bb7cc5dd9/transformtool3.gif)

When the Transform Tool is active, you can also use the **Tool Options** properties to set explicit values for the lattice. These properties affect specific areas of the lattice and display in absolute **Seconds**.

| Name | Description |
| --- | --- |
| **Upper / Lower Bound** | 
These properties control the locations of the upper and lower bounds of the lattice.

![upper bound lower bound](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6844d806-fa8f-47ea-ae8b-22e93a425ab0/transformtoolupperlower.png)

 |
| **Left / Right Bound** | 

These properties control the locations of the left and right bounds of the lattice.

![left bound right bound](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/470ae110-06c2-4c7f-a167-8b1e2d531bc3/transformtoolleftright.png)

 |
| **Scale Center X / Y** | 

These properties control the location of the scale pivot point.

![transform tool pivot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4635d86-961b-4920-b347-c90fc56c4422/transformtoolcenter.png)

 |

### Retime Tool

The Retime Tool enables a one-dimensional lattice tool, with which you can specify arbitrary anchor points along the time graph in order to retime your keyframes relative to those points.

To enable the Retime Tool, click the **Retime Tool** button in the toolbar. This will cause two vertical green lines to appear, which are **Retime Anchors**.

![retime tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ba87cb5-b37e-42a7-b296-ea9cca5623da/retimetool1.png)

Drag either of the Retime Anchors to retime your keys. When you select one, it will show its influence between its adjacent anchors, which is a linear falloff.

![retime tool edit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/deb31d11-ac87-4b79-9843-66859aef15df/retimetool2.gif)

Double-click in the graph to add new anchor points, and click the **Delete (X)** button below the anchor lines to remove anchors.

![retime tool add delete](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d6246c3-4caf-4a7c-9c16-20aa4be3a9aa/retimetool3.gif)

### Multi Select Tool

The Multi Select Tool enables a pivot-based scaling tool, with which you can scale your curve along either the value or time axes relative to a set pivot point.

To enable the Multi Select Tool, click the **Multi Select Tool** button in the toolbar, then select multiple keyframes.

![multi select tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5adcbaf-fa96-4c8f-8ddc-01f557798189/multiselecttool1.png)

Dragging either the vertical or horizontal handles will stretch the selected keyframes along the time or value axes. The horizontal handle corresponds to the **XScale** property, and the vertical handle corresponds to **YScale**.

![multi select tool edit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b85e3105-2335-4e0f-95b9-e6d2acf58ee5/multiselecttool2.gif)

The **Pivot Type** property controls the placement of the scale pivot point, which is denoted with a crosshair overlay on the graph. You can select the following options from it:

-   **Average**, which will place the pivot at the average location between all selected keyframe points and values.
-   **Bound Center**, which will place the pivot at the center point of the bounding box of all selected keyframes.
-   **First Key**, which will place the pivot at the location of the left-most selected keyframe.
-   **Last Key**, which will place the pivot at the location of the right-most selected keyframe.

![multi select tool pivot type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e08083c-f82a-4482-898e-eb1d1e3a84ec/multiselecttool3.gif)

### Filter Tool

The Filter Tool contains various filters and commands with which you can **Bake**, **Smooth**, and perform other operations to your curves. To open the Filter Tool window, click the **Filter Tool** button in the toolbar.

![curve editor filter tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ffa6baf-0a16-4f79-a985-9a8ff63416f6/filtertool.png)

When performing filter commands, the commands will only apply to the keyframes and curves you have selected in the graph.

#### Bake

Baking causes new linear keyframes to be created along your curve selection at a specified interval when clicking **Apply**.

![curve editor bake keyframes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13287799-365e-4de8-b1c5-ee5b3bc0d615/bake1.gif)

When baking a curve section, only the section between your keyframe selections will be baked. In the above example you can see curve sections outside of the selection are not being baked.

Bake has the following properties:

| Name | Description |
| --- | --- |
| **Use Frame Bake** | If this is enabled, then keyframes will be baked according to the [Frames Per Second](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#framespersecond) value of the sequence. |
| **Bake Interval in Frames** | The interval to bake keyframes relative to the framerate of the sequence. A value of **1** will bake every frame, and higher number values will skip that number of frames. |
| **Bake Interval in Seconds** | If **Use Frame Bake** is disabled, then this will be the seconds-based interval to bake keyframes. |

#### Euler

The Euler filter is used to correct rotational frame jumps. Typically these can occur when working with imported raw motion capture data.

![curve editor fix rotation 360 180 euler filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac2d8245-7752-4c4c-b53b-87e889d7bf05/euler1.png)

#### Fourier Transform (FFT)

The Fourier Transform filter is used to smooth keyframes with a lot of divergences or noise between them. The smoothing effect is achieved without deleting keyframes, and is based on intelligent low or high pass smoothing with frequency parameters. Typically you would use this if you are cleaning up raw imported motion capture animation, or smoothing a noisy curve with many keyframes.

![curve editor fourier transform fft filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18a45ae5-9974-4676-8952-e56a60b5b39b/fourier1.png)

Select **Fourier Transform (FFT)** in the filters window to view its properties.

![fourier filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b62b6f9-2c87-4136-b04e-ec06c8496ee1/fourier2.png)

| Name | Description |
| --- | --- |
| **Cutoff Frequency** | This property controls the strength of the filtering effect. If **Type** is set to **Lowpass**, then you will need to set this value lower in order to produce a smoother result. If **Type** is set to **Highpass**, then you will need to set this value higher. |
| **Type** | Which types of frequencies are to be allowed through. If **Lowpass** is specified, then low frequency noise will be ignored and filtering will only occur on high frequency noise. |
| **Response** | 
The type of Fourier filter to use.

-   **Butterworth** filter removes noise from data without affecting the curve's minimum or maximum values.
-   **Chebyshev** filter removes noise from the data and can affect the curve's minimum or maximum values, but it will have a sharper cutoff at the specified frequency, and will improve accuracy in some cases.



 |
| **Order** | The number of samples to use when filtering in the time domain, which affects how steep the roll-off is for the filter. |

In this example, a **Butterworth** filter type is being used to remove high frequency noise along a curve when clicking **Apply**.

![fourier butterworth filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40f181ba-11f8-4833-82a6-5de3f951d0ea/fourier3.gif)

#### Simplify

The Simplify filter removes redundant keyframes based on a tolerance amount, while still maintaining the overall curve. You can also set the following properties to customize the Simplify operation:

| Name | Description |
| --- | --- |
| **Tolerance** | The higher the **Tolerance** value, the more the filtered curve is allowed to deviate from the original, which causes more keyframes to be removed. |
| **Try Remove User Set Tangent Keys** | Enables using **Sample Rate** as the method to sample between evaluated keyframes, which includes keyframes with user tangents to be possibly removed during simplification. |
| **Sample Rate** | The frame rate at which the curve should be sampled to compare against **Tolerance**. |

Click **Apply** to execute the Simplify command on all selected keyframes.

![curve editor simplify curve filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8d15ec5-b4ff-40da-8e6f-027a5ea637f3/simplify.gif)