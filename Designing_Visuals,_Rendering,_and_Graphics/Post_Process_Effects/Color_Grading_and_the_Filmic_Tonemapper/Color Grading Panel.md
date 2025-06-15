# Color Grading Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-panel-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-panel-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:09

---

The **Color Grading** panel is a dedicated interface for manipulating colors in your scenes. It uses actors that can perform [color grading operations](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine), such as Post Process Volumes and Color Correction Regions.

You can use this pane to configure color grading properties and settings directly, instead of through any individual actor’s Details panel. This should make the configuration more straightforward for artists.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e06cefd-7439-418d-bc37-06cb421684ca/cg-scene.png)

## Color Grading Panel Interface

You can open the **Color Grading** panel from the main menu of the editor by selecting **Window > Color Grading**. This panel opens at the bottom of the level viewport.

The Color Grading panel interface includes the following:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d1e004f-b8e3-4e3b-8a07-4310382224ec/cg-panelinterface.png)

1.  Toolbar
2.  Object Mixer Panel
3.  Color Grading Properties

### Toolbar

You can use the **Toolbar** to configure various different elements for your scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98452762-9373-464e-94b8-d637565045b4/cg-toolbar.png)

From the toolbar, you can perform the following actions:

-   Add color grading-capable actors to the scene.
-   Filter and search for color grading-capable actors by name.
-   Toggle sync selection between the Outliner and Object Mixer panel for actors.
-   Add folders to organize actors in the Object Mixer.
-   Add and Manage Collections for color grading-capable actors.

### Object Mixer Panel

The **Object Mixer** lists all types of actors within the scene and levels that have color grading controls. Actors within this list can be parented and grouped within folders.The folders mirror how the actors are displayed in the Outliner list.

The following types of actors are supported in the Object Mixer list:

-   [Post Process Volume](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)
-   [Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)
-   [Camera Actor](/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine)
-   [nDisplay Root Actor](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine)
-   [Color Correction Region](/documentation/en-us/unreal-engine/color-correct-regions-in-unreal-engine)
-   [Color Correction Window](/documentation/en-us/unreal-engine/color-correct-regions-in-unreal-engine)

Some actor types only become available when their plugin is enabled for the project. For example, the **nDisplay** plugin must be enabled for the nDisplay Root Actor type to show up in the list. You can enable plugins from the editor’s main menu by selecting **Edit > Plugins**.

From this panel, you can view information and perform the following actions:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c9aaa51-d41b-4038-af29-98d117c383b5/cg-objectmixer.png)

-   The sorting columns can be arranged in ascending or descending order.
-   Toggle actions for pinning, actor visibility, and isolating actors.
-   Identify objects that have changes that are yet to be saved.
-   Use the settings menu to show / hide list items.

### Color Grading Properties

The primary portion of the Color Grading panel displays the tonal color grading properties and their color wheels with channel values. These settings are often found in the Details panel of any actor that you can perform color grading on. The color grading properties are shown when you select a supported color grading actor type in the Object Mixer panel or the Outliner.

|   |   |
| --- | --- |
| 
 | 

 |
| Color Grading Panel and additional properties. | Color Grading properties of a Post Process Volume found in the Details panel. |

Click images to view full size.

The interface can be broken into two parts:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3149050f-382f-4bc9-8c2c-dfe51885a417/cg-propertiesinterface.png)

1.  The Color Grading panel with tonal ranges, color wheels, and value sliders.
2.  Color grading property overrides.

The color grading panel has the following properties:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bf45a16-a374-4245-b695-63553ead5c17/cg-colorwheelpropertiesinterface.png)

1.  Name of the currently selected actor that can be color graded.
2.  A selection of Tonal Ranges with their own color grading properties for Saturation, Contrast, Gamma, Gain, and Offset.
3.  Color model selection to display color values in RGB (Red, Green, Blue) or HSV (Hue, Saturation, Value).
4.  Color wheels and their value sliders.

Each Tonal Range (2) for **Global**, **Shadows**, **Midtones**, and **Highlights** has their own Color Wheels (4) for **Saturation**, **Contrast**, **Gamma**, **Gain**, and **Offset**. Each of these color wheels has their own value sliders and is specific to their tonal range.

When you select a color model (3), the value sliders change to match the selection. You can see an example of this in the table below.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5be5d5fd-6978-416c-bad5-a18834cbe1fd/cg-rgbmodel.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/226c5de4-9c63-4a32-8df8-525d28c2db4d/cg-hsvmodel.png) |
| RGB Color Model | HSV Color Model. |

To the right of the color wheel and sliders are the general property overrides panel that includes general color grading properties:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfe8b97a-00b7-4b76-8539-e5112f5ff1e1/cg-overrideproperties.png)

For more information on these settings and using color grading in your project, see [Color Grading Settings](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine).

## Managing Color Grading Actors

The Color Grading panel is where you can manage and edit all eligible actors in your scene.

### Filtering Color Grading Actors

Use the **Search Filter** at the top of the Object Mixer to filter actor types that support color grading.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4922810-8a26-473b-bfb4-d63559ed1895/cg-searchbar.png)

For large scenes with many color grading-capable actors, you might be able to speed up your workflow by filtering them with search

### Add Color Grading-Capable Actors

You can use the **Add (+)** button to add color grading-capable actors to the scene from this panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ccbfef0-bf2b-45a6-b4e9-f0199ab72259/cg-addactors.png)

### Sync Selection

The **Sync Selection** toggle synchronizes selected actors in the Object Mixer panel with the level [Outliner](/documentation/en-us/unreal-engine/outliner-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/756e4e4f-5f46-4c15-9c54-1e55fc3cfb49/cg-syncselection.png)

When **enabled**, the Color Grading panel and the Outliner act as one. This means that selected objects that have color grading properties are selected in both of these panels.

When **disabled**, each panel acts individually of the other by only selecting items within their own panel. Disabling sync selection is useful when you want to keep a color grading-capable actor selected in the Color Grading panel but also want to work within your scene to make other changes separately from color grading.

The Sync Selection toggle has accompanying functionality with the **Alt + Click** hotkey. When enabled, use this hotkey to only select items from the panel in which you are selecting an actor. When disabled, use this hotkey to sync selection in both panels.

### Organizing the Hierarchy

The Object Mixer’s list of actors can be organized with folders, actor parenting, or both.

The **Add Folder** icon in the toolbar creates a new folder for the selected actor in the Object Mixer. This icon will not add empty folders to the Object Mixer panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e78a3e1-ba84-4c29-a097-bcb583ed3f58/cg-addfolder.png)

You can parent actors in the list by dragging and dropping them onto one another. The Outliner mirrors any parent-child organization.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eb6841d-e33f-4424-a1a9-3fedb330124a/cg-folders.gif)

When a folder is left empty by moving or reparenting an actor, the folder is removed from the Object Mixer panel but not from the Outliner.

### Actor Visibility

You can toggle the **Visibility** of any color grading-capable actors by clicking the **Eye** icon next to their listed name in the Object Mixer. This sets whether this actor is visible in the scene or is muted. An icon of an open eye indicates that the actor is visible, and an icon of a closed eye indicates that it is muted in the scene. You can use this workflow to inspect particular parts of your scene, without making actual changes to it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01d212d4-6d92-47df-acae-b362a1d19796/cg-visibility.png)

### Actor Isolation

You can toggle the **Solo** option for any color grading-capable actors by clicking the **Headphones** icon next to their listed name in the Object Mixer.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7188336b-f4a9-4652-a40d-cc9e49245fb1/cg-isolation.png)

Toggling the Solo icon disables visibility of all other color grading actors in the Object Mixer, while leaving only the selected color grading actors visible. You can use this workflow to inspect particular actors on their own in your scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/383ac06d-693e-498f-a90f-84798f6e9c61/cg-isolationexample.gif)

### Settings Menu

The **Settings** menu contains configurable options for how actors are displayed in the Object Mixer panel. You can open this menu from the toolbar by clicking on the **Gear** icon.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8533be3-6f22-47b9-a4d8-7b7fc201019f/cg-settingsmenu.png)

The primary features of this menu are:

-   Settings to expand and collapse the Object Mixer hierarchy.
-   Show / Hide options for actors in the Object Mixer panel.
-   Whether to show folders in the Object Mixer panel.
-   Selection options for different worlds (levels) to display only actors from those levels when using World Partition.

## Working with Color Grading Collections

[Collections](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine) serve as a way to organize your assets into groups of user-defined sets. In the Object Mixer panel, you can add similar or frequently edited actors to groups for quicker access to their properties. For editing purposes, you can group Actors in the Object Mixer into individual or multiple collections.

All color actors that are eligible for color-grading listed in the Object Mixer belong to a default collection called **All**. This collection category doesn’t appear until a custom one is created, and it cannot be edited or removed.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3fdc1ee-ba92-437a-883a-45ef55ca2f0a/cg-collectionsbar.png)

### Creating a Color Grading Collection

To create a collection:

1.  Select one or more actors listed in the Object Mixer panel.
2.  Right-click the actors you want to create a collection for, and hover the mouse over **Select or Add Collection** in the context menu.
3.  In the text field, enter a name for this collection.
4.  Press **Enter** to create the collection.

Newly created collections appear below the search filter in the toolbar and just above the Object Mixer sorting columns. There is no limit to the number of collections you can create.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f2d30db-2f4f-40eb-952d-3324b5ce81be/cg-addcollection.gif)

### Viewing a Color Grading Collection

To view a collection, click on its name in the Collections area of the toolbar. When you select the collection, only the color grading-capable actors in the collection appear. The **All** collection restores all actors to the Object Mixer list.

### Adding and Removing Actors from a Color Grading Collection

You can add and remove eligible actors to a collection using the right-click Context Menu.

1.  Select one or more actors listed in the Object Mixer panel.
2.  Right-click the actors, and hover the mouse over **Select or Add Collection** in the context menu.
3.  In the list of collections, you can:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1f1a0b3-5cb8-4a87-871d-62838d920258/cg-addremovecollections.png)
    -   **Add** an actor to a collection by placing a checkmark in the box next to the named collection.
    -   **Remove** an actor from a collection by unchecking the box next to a named collection.

Actors are not exclusive to a single collection and can be added from any number of collections.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b270e4d-60d7-4ffe-8797-36d93774e7a7/cg-addremovecollections.gif)

### Deleting, Duplicating, and Renaming a Color Grading Collection

In the toolbar where all the Collections are listed, right-click on any collection to open its context menu. The options to **Delete**, **Duplicate**, or **Rename** the collection appear.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53cde47f-8364-4cfb-b403-fbd3e167b17a/cg-collectionactions.png)

The **All** collection is the only one that cannot be deleted, duplicated, or renamed. Right-clicking it does not show any options.

### Reordering Color Grading Collections

You can reorder any listed collection by left-clicking on it and dragging it to a new position within the collection row. The **All** collection cannot be moved.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14a0d438-2e65-49bf-bcfe-946b24742857/cg-collectionplacement.gif)

## nDisplay with Color Grading

There are additional color grading capabilities for [nDisplay](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine) content when used with the Color Grading panel.

These options only become available when the **nDisplay** plugin is enabled for the project. You can enable it in the **Plugins** browser. Open it from the editor main menu under **Edit > Plugins**.

Alternatively, if you want to see a project already set up using nDisplay and ICVFX with the Color Grading panel, you can create an **InCameraVFX** template project from the project browser under the **Film / Video & Live Events** tab.

### Per-Viewport and Per-Node Color Grading

You can apply color grading separately to both the Outer Viewports and the In-Camera VFX (ICVFX) Camera. Color grading is additively layered with per-viewport and per-node groupings with nDisplay.

When you select content that supports nDisplay in the Object Mixer, the color grading panel includes additional options in the top-left above the color wheels.

#### Per-Viewport Grouping

When you select the **Display Cluster Root Actor** (DCRA) in the Object Mixer panel, an additional option becomes available at the top of the color grading panel with the **Entire Cluster** button, checkbox, and dropdown viewport selection.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78d3139c-0178-4019-9c0e-1c72daef2e23/cg-ndisplayclusters.png)

You can use the **Add (+)** icon to create a new per-viewport grouping. A Per-Viewport Settings category becomes available on the right side of the color grading panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c438a42-3413-4874-a963-57a234948dc3/cg-viewportgrouping.png)

With the added per-viewport grouping, you can use the viewports dropdown to select from available viewports for this group to use. You can choose one or more viewports in the list by placing a check by their names.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/528cfaa8-f0a5-4500-9572-72913cedc940/cg-viewportselectionforgroup.png)

The properties panel on the right-side of the color grading panel now includes a **Per-Viewport Settings** category. You can opt in or out of including **All Nodes** properties from the Outer Viewports, since the ICVFX Camera displays on top of them at all times.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/423b5722-c67b-47a2-8ff9-d01a879785fd/cg-perviewportsettings.png)

#### Per-Node Grouping

When you select an **ICVFX Camera** component in the Object Mixer panel, an additional option becomes available at the top of the color grading panel with the **All Nodes Color Grading** button, checkbox, and dropdown node selection.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/598e8b48-6819-4c9b-bbd5-6ebf5a9f3daa/cg-icvfxnodes.png)

You can use the **Add (+)** icon to create a new per-node grouping and a Per-Node Settings category becomes available on the right side of the color grading panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ce853e1-1722-46e3-a377-24a9db6d8afb/cg-nodessettings.png)

With the added per-node grouping, you can use the nodes dropdown to select from available nodes for this group to use. You can choose one or more nodes in the list by placing a check by their names.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e1d8099-1d3a-4e45-bf00-415f9680adc9/cg-nodeselectiongroups.png)

The properties panel on the right-side of the color grading panel now includes a **Per-Node Settings** category. You can opt in or out of including **All Nodes** properties.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3530007-1cf9-4c9b-a097-25cee5125dd8/cg-pernodesettings.png)

### In-Camera VFX Editor

Since color grading is an integral part of the stage workflow for [In-Camera VFX](/documentation/en-us/unreal-engine/in-camera-vfx-in-unreal-engine) (ICVFX) virtual production, the color grading panel is present in the ICVFX Editor as a drawer that can be summoned and dismissed using the hotkey **CTRL + Spacebar** or by clicking the **Color Grading** tab at the bottom of the editor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9265956-0c83-443a-814a-3f54fa944377/cg-embeddedpanel.gif)

The color grading panel is a dockable panel in the ICVFX editor. You can click **Dock in Layout** in the top-right of the panel to have it automatically dock below the viewport.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d57aecaa-6d67-4ac5-a336-5b949ea2616e/cg-dockinlayoutbutton.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28e40f47-a1b2-4017-b906-6d16c60d855a/cg-dockinviewportaction.gif)