# Layers Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:54

---

The **Layers** panel allows you to organize Actors in your Level.

Click image for full size.

Layers provide the ability to quickly select as well as control visibility of groups of related Actors. You can use your layers to quickly un-clutter a scene leaving only the geometry and Actors that you are working with. For example, you might be working on a building that has multiple levels but is comprised of many modular parts. By assigning each floor to a layer, you can hide each of the floors you are not working on making the top view much more manageable.

An Actor can be in as many layers as you want. This might be useful if you have different sets of Actors that fall under overlapping layers. For instance, you could organize your layers by assigning everything within a particular *zone* to one layer and have another layer comprised of all the doors in your level.

When creating large levels, the more extensively you use layers, the easier your job will be. And remember, it is always easier to start using layers from the beginning rather than trying to incorporate them after you are already deep into the creation of your level.

## Layer Creation

Layers are created in the **Layers** panel either as empty or using the current selection.

**To create an empty layer:**

1.  **Right-click** in the **Layers** panel and choose *Create Empty Layer*.
    
    ![Create Empty Layer menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fca95cbb-9c13-4ef0-bf40-93849550dfe7/02-create-empty-layer-menu-option.png "Create Empty Layer menu option")
2.  The new layer is displayed in the list.
    
    ![Layer1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef4ad5ed-7026-474d-9e61-abb5678ecc39/03-layer-layer-1.png "Layer1")

**To create a layer from a selection:**

1.  Select the objects to add to the layer in the viewport.
    
    ![Selected Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05f33734-92dc-4a71-850a-313c3d4918af/04-selected-actors.png "Selected Actors")
2.  **Right-click** in the **Layers** panel and choose *Add Selected Actors to New Layer*.
    
    ![New Layer from Selection menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d782c88-854f-4d18-ba56-0e192577fbe8/05-new-layer-from-selection-menu-option.png "New Layer from Selection menu option")
3.  The new layer containing the Actors is displayed in the list.
    
    ![Layer 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e0ed0b9-63af-405b-90b0-84f252235c84/06-layer-layer-1.png "Layer 1")

**To create a layer by drag and drop:**

1.  Select the Actor(s) to add to the layer.
    
2.  Drag the Actor(s) from the **World Outliner** on to the empty area in the **Layers** panel.
    
    ![Layer drag drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3847ddca-78a6-41a0-b763-fc92402ca0cf/07-layer-drag-drop.png "Layer drag drop")
3.  The new layer containing the Actors is displayed in the list.
    
    ![Layer 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bee6945e-c6d8-4a99-b6f8-3bb9a3abe74a/08-layerlayer-1.png "Layer 1")

## Layer Naming

By default, new layers are given a name using a *Layer\[number\]* naming scheme. The number is incremented for each new layer. It is best to make sure you name your layers with descriptive names, and never leave the default naming. For instance, a layer that contains small items scattered on the floor might be named *Ground Clutter*. This not only makes it easy to quickly see what each layer contains, but also makes it possible to filter the layers using the [search](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine#searchinglayers) feature.

Layer names can contain any alphanumeric characters and can also include spaces, hyphens, and underscores.

**To rename a layer:**

1.  **Right-click** on the layer and choose **Rename** from the context menu.
    
    ![Rename layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d58e851-a985-4f3f-80d9-4656868e3d1a/09-rename-layer.png "Rename layer")
2.  Enter a name in the text box containing the current name.
    
    ![Layer new name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/428c6ea7-7067-4e90-b5fb-647bc7d591f3/10-layer-new-name.png "Layer new name")
3.  The layer is displayed with the new name.
    
    ![Layer new name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b9be02b-c419-4a45-b5c7-152fac887430/11-layer-new-name-2.png "Layer new name")

## Searching Layers

Layers can be filtered using the search box at the top of the **Layers** panel. Filtering occurs based on matches between the text entered in the search box and the names of the layers. As you type in the box, the list of layers is filtered in real-time; only displaying those layers whose names match the text.

|   |   |
| --- | --- |
| ![Unfiltered Layer List](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3af686a-a7b7-42b2-9594-210062a796be/12-layer-new-name-2.png "Unfiltered Layer List") | ![Filtered Layer List](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9142ef3c-d9d3-4e47-af86-573631ffbe3f/13-layers-filter.png "Filtered Layer List") |
| Unfiltered Layer List | Filtered Layer List |

Press the 'X' button to clear the current search terms.

## Layer Contents

The contents of a layer can be viewed directly in the **Layers** panel. The layer contents view displays the name of the layer, a list of all Actors contained in the layer, and information about the layer's contents. To enter the layer contents view, press the **See Contents** button at the bottom of the **Layers** panel with the layer you want to view selected.

Click image for full size.

The name of the layer is displayed at the top along with a collection of buttons showing the various types and numbers of Actors contained within the layer.

Click image for full size.

The various buttons to the right of the layer's name show how many of each individual type of Actor are contained within the layer. For instance, the button in the bottom right of the Layers panel informs the user that there are 139 StaticMeshActors contained within the layer.

These buttons can also be used to perform [type-specific selections](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine#type-specificselection).

To return to the layer list, press the ![Back button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3fd98f4-5d32-4666-8b90-f9ce99d15d82/17-back-button.png "Back button") button.

### Adding Actors

Actors can be added to one or more layers as a selection or by dragging and dropping from the **World Outliner**.

**To add a selection of Actors:**

1.  Select the Actor(s) to add to the layer.
    
    ![Select Actors to add](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee3f946c-168d-4dab-8541-db16a4ec3fe3/18-select-actors-to-add.png "Select Actors to add")
2.  **Right-click** on the layer you want to add the Actors to and choose *Add Selected Actors to Selected Layers*.
    
    ![Add Selected Actors to Selected Layers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ecdfab3-f0d7-46da-ac1c-d548337b9f6e/19-add-selected-actors-to-selected-layers.png "Add Selected Actors to Selected Layers")

**To add by drag and drop:**

1.  Select the Actor(s) to add to the layer.
    
2.  Drag the Actor(s) from the **World Outliner** on to a layer in the **Layers** panel.
    
    You can also drag to the contents bar at the bottom of the **Layers** panel to assign the Actors to the selected layer.
    
    ![Layers drag and drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6241784e-8ab7-4d36-b704-5bc4caebe89c/20-layers-drag-and-drop.png "Layers drag and drop")The layers the Actors are already assigned to are grayed out when dragging and dropping. Additionally, if the Actors being dragged are already assigned to the target layer, a message will inform you of this: ![All Actors already Assigned to Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c75bd8e8-1b5e-450d-ba2b-2052fec430fa/21-all-actors-already-assigned-to-layer.png "All Actors already Assigned to Layer") 
3.  The Actors are added to the layer.
    

### Removing Actors

Actors can be removed from the layer individually or as a group of selected Actors.

**To remove individual Actors:**

1.  Press the 'X' button next to the Actor in the layer contents view.
    
    ![Remove Actor button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c165032e-abd1-4c0e-adbf-3fad468e0fcd/22-remove-actor-button.png "Remove Actor button")
2.  The Actor is removed from the layer and the list is updated.
    
    ![Remove Actor button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e64252fa-6b43-4ddd-b8ba-56abfcffb009/23-remove-actor-button.png "Remove Actor button")

**To remove a selection of Actors:**

1.  Select the Actors to be removed from the layer.
    
    ![Select Actors to remove](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7863ea6-164f-4c66-9443-134dc265c933/24-select-actors-to-remove.png "Select Actors to remove")
2.  **Right-click** on the layer and choose *Remove Selected Actors from Layers*.
    
    ![Remove Selected Actors menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39ede4db-488a-4f33-a5ad-4c39a0029321/25-remove-selected-actors-menu-option.png "Remove Selected Actors menu option")
3.  The Actors are removed from the layer.
    

### Searching Layer Contents

The Actors within a layer can be filtered in the layer contents view using the search box at the top. Filtering occurs based on matches between the text entered in the search box and the names of the Actors. As you type in the box, the list of Actors is filtered in real-time; only displaying those Actors whose names match the text.

|   |   |
| --- | --- |
| ![Unfiltered Layer Contents](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/520cfc24-ba8e-4190-b769-55cc438893d8/26-layers-contents-unfiltered.png "Unfiltered Layer Contents") | ![Filtered Layer Contents](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88ad2a34-1484-4d7e-a467-a6fef9f0263c/27-layers-contents-filtered.png "Filtered Layer Contents") |
| Unfiltered Layer Contents | Filtered Layer Contents |

Press the 'X' button to clear the current search terms.

## Visibility

The contents of any layer can be shown or hidden by toggling the Visibility (eye) button for the layer in the layer list.

|   |   |
| --- | --- |
| ![Layer Visible](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd958363-8b62-416a-9556-8c0a75a5579a/28-layer-visible.png "Layer Visible") | ![Layer Hidden](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfa01831-fd34-46ea-b5d6-b437cbb56d6c/29-layer-hidden.png "Layer Hidden") |
| Visible ![Visibility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b24cce79-22b0-4d6d-8b25-b548a6001e8c/30-visible-visibility.png "Visible") | Hidden ![Visibility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/798b1169-eb7e-457a-bbf8-55c67d7ccf7e/31-hidden-visibility.png "Hidden") |

## Selection Methods

Actors within a layer can be selected as a group, individually, or based on type. The Actors within a layer can also be added to or removed from the current selection.

**To select all Actors within a layer:**

1.  **Double-click** the layer in the layer list or **right-click** on the layer and choose *Select Actors*.
    
    ![Select Actors menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25a44c2f-ee86-4ba3-b9c4-9d1cf68151da/32-select-actors-menu-option.png "Select Actors menu option")
2.  All Actors in the layer are selected, replacing the current selection set.
    
    ![Actors Selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3af0f0f1-9ec7-4f58-be72-d11724019086/33-actors-selected.png "Actors Selected")

**To append layer Actors to the selection:**

1.  **Right-click** on the layer and choose *Append Actors to Selection*.
    
    ![Select Actors menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/013dc238-9d9f-4593-be51-48a598f96324/34-select-actors-menu-option.png "Select Actors menu option")
2.  All Actors in the layer are selected, appending them to the current selection set.
    
    |   |   |
    | --- | --- |
    | ![Initial Actors Selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7d5ea27-b580-4fc9-b109-670ef4afc96b/35-initial-actors-selected.png "Initial Selection") | ![Layer Actors Appended](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fd12a96-c85b-4385-b889-23015e230b24/36-layer-actors-appended.png "Layer Actors Appended") |
    | Initial Selection | Layer Actors Appended |
    

**To remove layer Actors from the selection:**

1.  **Right-click** on the layer and choose *Deselect Actors*.
    
    ![Select Actors menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca1783fb-770e-4354-a190-e13338a5ccb4/37-select-actors-menu-option.png "Select Actors menu option]")
2.  All Actors in the layer are removed from deselected, removing them from the current selection set.
    
    |   |   |
    | --- | --- |
    | ![Initial Actors Selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e33d0563-4402-4d04-b253-6d231a204e34/38-initial-actors-selected.png "Initial Selection") | ![Layer Actors Removed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b91f9bf-f99f-404f-888f-e2fbda036e72/39-layer-actors-removed.png "Layer Actors Removed") |
    | Initial Selection | Layer Actors Removed |
    

### Type-Specific Selection

Type-specific selection allows you to quickly select all of one type of Actor contained within a layer. This can be performed using the buttons in the contents bar of the main layer list or the title bar of the layer contents view.

|   |   |
| --- | --- |
| ![Contents Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b8c43e8-f3f7-4574-b4e0-b7d56c608903/40-contents-bar.png "Layer List Contents Bar") | ![Title Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46a58b02-9876-42b0-81db-df8725f30b1b/41-title-bar.png "Layer Contents View Title Bar") |
| Layer List Contents Bar | Layer Contents View Title Bar |

Pressing the instances button selects all of the StaticMeshActors in the layer.

![Selected StaticMeshActors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3db5a728-a525-4744-ab7f-6921677b3fe9/42-selected-static-mesh-actors.png)

## Details Layers Section

The **Layers** category displays which layers the selected Actor(s) belong to using a tag cloud style layout.

![Layer cloud](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f42b8bfe-78d9-4d6d-84a3-cc7c28118b39/43-layer-cloud.png "Layer cloud")

Only the layers common to all selected Actors will be displayed.

Clicking the ![Remove](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f85d9196-8c2a-4963-a52e-445f0cb5b6e1/44-remove.png "Remove") button for a particular layer will remove all selected Actors from that layer.