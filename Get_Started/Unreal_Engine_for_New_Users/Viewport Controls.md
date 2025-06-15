# Viewport Controls

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-controls-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-controls-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:59

---

Unreal Engine uses **Viewports** to visually represent objects in your project. This can include objects in the world when using the Level Editor Viewport or individual tool editor viewports, like the ones found in the Material Editor, Animation Mode Editor, and Niagara Systems Editor. Each of these viewports share similar ways of navigating them in order to view objects with lighting and materials representative of what you'd see in your game or the Level Editor viewport.

The Level Editor is where most of your time will generally be spent when creating a game, making its viewport a great example for learning navigation.

A number of viewport settings and panels listed in this page assumes that you have read through a previous page in the onboarding series, [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface), describing the most common elements of Unreal Engine. If you haven’t yet, we recommend that you read through that page first to get an understanding of Unreal Editor’s interface.

## Abbreviations used on this page

For the purposes of this page, you should assume the following abbreviations, which we’ll refer to throughout the page:

| Control | Abbreviation |
| --- | --- |
| 
Left Mouse Button

 | 

LMB

 |
| 

Middle Mouse Button

 | 

MMB

 |
| 

Right Mouse Button

 | 

RMB

 |

The control schemes are split into their own lists with one covering **Perspective** view, and the other **Orthographic** view. Perspective view can be used to edit your level in a 3-dimensional (3D) space, while Orthographic view is used for editing in 2-dimensional (2D) space, like a top-down or side view perspective.

Some of the controls below are configurable in the **Keyboard Shortcuts**, located in **Edit -> Editor Preferences -> General -> Keyboard Shortcuts**. Each shortcut’s default state is listed in this page. If you have made changes to them, they may not match.

## Selecting objects in the level

When selecting objects in the Level Editor viewport, you can edit their properties using the **Details** panel, and move, rotate, and scale them within the viewport.

| Control | Action |
| --- | --- |
| Perspective view: |  |
| --- | --- |
| 
Press LMB

 | 

Selects the object under the cursor, replacing the currently selected object, if there is one.

 |
| 

Hold Ctrl / Hold Shift + Press LMB

 | 

Adds the object under the cursor to the current selection.

 |
| Orthographic view: |  |
| --- | --- |
| 

Press LMB

 | 

Selects the object under the cursor, replacing the current selection, if there is one.

 |
| 

Hold LMB + Drag the mouse

 | 

Creates a marquee selection box to select multiple objects, replacing the current selection, if there is one.

 |
| 

Hold Shift + Hold LMB + Drag the mouse

 | 

Adds the objects contained in the marquee selection box to the current selection.

 |
| 

Hold Ctrl + Hold RMB + Drag the mouse

 | 

Removes the objects contained in the marquee selection box from the current selection.

 |

## Navigating the level

There are multiple ways in which you can navigate the viewport. Some can be done entirely with the mouse, with the keyboard, and more often with a combination between the two.

#### Looking around your viewport

Using these controls, you can look around the viewport using only your mouse. There are additional sets of controls for Magic Mouse and Magic Trackpad users that you can reference below.

| Perspective | Orthographic |
| --- | --- |
|  |  |

##### Using a regular mouse

| Control | Action |
| --- | --- |
| Perspective |  |
| --- | --- |
| 
Hold LMB + Drag the mouse

 | 

Moves the camera forward and backward and rotates left and right.

 |
| 

Hold RMB + Drag the mouse

 | 

Rotates the camera to look around the level.

 |
| 

Hold LMB + Hold RMB + Drag the mouse

Hold MMB + Drag the mouse

 | 

Moves the camera up, down, left, and right without rotation.

 |
| 

Scroll up or down with MMB

 | 

Moves the camera forward and backward by increments.

 |
| Orthographic |  |
| --- | --- |
| 

Hold LMB + Drag the mouse

 | 

Creates a marquee selection box to select multiple objects.

 |
| 

Hold RMB + Drag the mouse

 | 

Pans the camera.

 |
| 

Hold LMB + Hold RMB + Drag the mouse

 | 

Moves the camera forward and backward.

 |
| 

Scroll up or down with MMB

 | 

Moves the camera forward and backward by increments.

 |

##### Using Magic Mouse and Magic Trackpad

| Magic Mouse Control | Magic Trackpad Control | Action |
| --- | --- | --- |
| Perspective |  |  |
| --- | --- | --- |
| 
Hold LMB + Drag the mouse

 | 

1 Finger Click + Drag

 | 

Moves the camera forward and backward and rotates left and right.

 |
| 

Hold RMB + Drag the mouse

 | 

2 Finger Click + Drag

 | 

Rotates the viewport camera.

 |
| 

Hold LMB + Hold RMB + Drag the mouse

Hold MMB + Drag the mouse

 | 

2 Finger Touch + Drag

 | 

Rotates the viewport camera.

 |
| 

Scroll up or down on the Multi-Touch Surface

 | 

Scroll up or down on the Multi-Touch Surface

 | 

Moves the camera forward and backward by increments.

 |
| Orthographic |  |  |
| --- | --- | --- |
| 

Hold LMB + Drag the mouse

 | 

1 Finger Click + Drag

 | 

Creates a marquee selection box.

 |
| 

Hold RMB + Drag the mouse

 | 

2 Finger Click + Drag

 | 

Pans the viewport camera.

 |
| 

Hold LMB + Hold RMB + Drag the mouse

Hold MMB + Drag the mouse

 | 

2 Finger Touch + Drag

 | 

Pans the viewport camera.

 |

#### Moving around in your level

You can use these controls to move the camera around in your viewport while in perspective view.

| Control | Action |
| --- | --- |
| 
Hold RMB + Scroll up or down with the mouse wheel

 | 

Increase / decrease the speed of the camera movement.

 |
| 

Hold RMB + W / Numpad8 / Up Arrow

 | 

Move the camera forward.

 |
| 

Hold RMB + S / Numpad2 / Down Arrow

 | 

Move the camera backward.

 |
| 

Hold RMB + A / Numpad4 / Left Arrow

 | 

Move the camera left.

 |
| 

Hold RMB + D / Numpad6 / Right Arrow

 | 

Move the camera right.

 |
| 

Hold RMB + E / Numpad9 / Page Up

 | 

Move the camera up.

 |
| 

Hold RMB + Q / Numpad7 / Page Down

 | 

Move the camera down.

 |
| 

Hold RMB + Z / Numpad1

 | 

Raises the Field of View of the camera.

 |
| 

Hold RMB + C / Numpad3

 | 

Lowers the Field of View of the camera.

 |

#### Orbiting the camera around an object or pivot

To pan, orbit, and zoom viewport controls, you can use these controls in Unreal Engine. These might be familiar to users of certain 3D tools like Maya and Unity.

| Control | Action |
| --- | --- |
| 
Press F

 | 

Focus the camera on a selected object in the level.

 |
| 

Alt + Hold LMB + Drag the mouse

 | 

Orbits the camera around a single pivot or point of interest. The point of interest can be an object you focus on using the F key.

 |
| 

Alt + Hold RMB + Drag the mouse

 | 

Dollies (zooms) the camera toward and away from a single pivot or point of interest.

 |
| 

Alt + Hold MMB + Drag the mouse

 | 

Tracks the camera left, right, up, and down in the direction of mouse movement.

 |

#### Moving, rotating, and scaling objects in the level

You can use the Transform tools to **move**, **rotate**, and **scale** selected objects using the viewport.

| Translate tool | Rotate tool | Scale tool |
| --- | --- | --- |
|  |  |  |

You can see which tool is active and switch to a different one using the options in the top-left corner of the viewport. You can also switch between the Transform tools by using their shortcuts. 

[![](https://dev.epicgames.com/community/api/documentation/image/9eb9feb1-62d4-4b36-8eaa-3b9f514a39db?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9eb9feb1-62d4-4b36-8eaa-3b9f514a39db?resizing_type=fit)

Each tool provides three axes you can use your mouse to pull on, the **X axis**, **Y axis**, and **Z axis**. Clicking and dragging any of these axes performs an operation in a specific direction.

You can use these controls to move, rotate, and scale objects in the level:

| Control | Action |
| --- | --- |
| 
Spacebar

 | 

Toggle between move, rotate and scale tools.

 |
| 

Q

 | 

Select the Selection Tool.

 |
| 

W

 | 

Select the Translate Tool.

 |
| 

E

 | 

Select the Rotate Tool.

 |
| 

R

 | 

Select the Scale Tool.

 |
| 

Hold LMB on a tool’s axis gizmo in the viewport + Drag the mouse

 | 

Move, rotate, or scale an object depending on the Transform tool selected. 

 |
| 

Hold V

 | 

Toggle vertex snapping to snap to the vertices of other geometry in the world. Vertex snapping is used only with the Translate Tool.

 |
| 

Hold MMB + Drag the mouse on the pivot point of the object

 | 

Translate the pivot of the selected object temporarily to offset transformations.

 |

With the transform tools you can also perform move and scale along multiple axes. You can identify which axes are being moved or scaled by how they are highlighted. For example, when using the Translate and Scale tools, you can use the pivot in the center of the tool gizmo in the viewport to move or scale uniformly. Or, you can hover your mouse over two axes and move or scale in only those directions.

When using one of the Orthographic views, you can only move or scale along two axes and do not have the option to move or scale in all directions.

#### Display controls

You can change how the level is displayed in the viewport with these controls.

| Control | Action |
| --- | --- |
| 
G

 | 

Toggle **Game Mode**, which causes the viewport to render only what would be seen in-game so that you don’t see editor-only gizmos and volume outlines by turning them invisible. 

 |
| 

Hold CTRL + Press R

 | 

Toggle real-time playback in the active viewport. Certain effects like the volumetric clouds of the sky will not dynamically move or update once real-time playback is toggled off. 

Toggling real-time viewport off can be useful for performance intensive scenes.  |
| 

F11

 | 

Toggle immersive mode, which puts the viewport into full-screen.

 |

#### Changing Viewport options with Editor Preferences

You can customize the navigation, controls, and overall look and feel of the viewport through the **Editor Preferences**. To access these options, go to **Edit > Editor Preferences > Level Editor > Viewports**.

In the **Controls** section, you can adjust settings related to viewport navigation, such as camera movement speed and mouse sensitivity. In the **Look and Feel** section, you can customize how the viewport appears and behaves to match your preferences. This includes options for enabling arcball rotation, enabling a combined translate/rotate widget, and adjusting the selection highlight intensity.