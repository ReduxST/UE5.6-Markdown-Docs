# Creating and Using Material Instances

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:12

---

Creating and editing standard Materials in Unreal Engine can be a time consuming process. To help speed up and streamline the Material creation workflow, Unreal Engine offers a special type of Material called a **Material instance**. This tutorial demonstrates how to set up and use Material instances in your projects.

## Material Instancing

Material instancing is a way to create a parent Material that you can use as a base to make a wide variety of different looking children (Material instances).

To achieve this flexibility, [Material instancing](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) uses a concept called **inheritance:** the properties of the parent Material are passed to its children. Properties that are designated as **parameters** in the parent Material are exposed to artists in the **Material Instance Editor**.

![Material Instance Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6df1641-1570-471f-b61a-d3301b4aed09/instance-editor-ue5.png)

Using Material instances, you can create numerous variations from a single base Material:

![Three Material instances](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c27779ba-479d-4a43-b352-6c3b587713ab/three-instances-ue5-sm.png)

### Creating Material Instances is a Two Step Process

1.  First create a **parameterized** Material that you will use as the parent Material for your instances.
2.  Create a **Material Instance Constant** in the Content Browser. You can then customize the Material in the Material Instance Editor.

For additional background information about Material instancing, [read the overview here](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine).

## Creating a Parameterized Material

A Material instance inherits all the attributes of its parent Material, but not all of these attributes can be customized in the Material Instance Editor by default.

To make Material attributes editable in a Material instance, you must designate certain attributes as **parameters** by using parameter nodes instead of regular [Material Expressions](/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference).

There are two ways to add parameter nodes to your Material graph.

### Adding Parameter Nodes from the Material Palette

If you search for the word "parameter" in the **Material Palette**, or from the right-click menu in the Material Editor, you can find all of the parameter nodes that are available.

You can drag and drop these parameter nodes from the Palette or select them in the right-click menu to add them to your Material graph.

![Material Expression palette and context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac8bfbac-ecc1-4699-b631-523939b9f297/pallette-and-context-menu.png)

Parameters in the right-click menu (left) and the Materials Palette (right).

#### Parameter Shortcuts

Two of the most commonly used Material parameters have keyboard shortcuts in the Material Editor:

1.  **Scalar Parameter** - Hold the **s key** and **left-click** in the Material graph to place a Scalar Parameter. A Scalar Parameter is the parameterized version of a Constant, and contains a single numeric value.
2.  **Vector Parameter** - Hold the **v key** and **left-click** in the Material graph to place a Vector Parameter. A Vector Parameter is the parameterized version of a Constant 4 Vector and contains four floating-point values.

Use the shortcut or palette to place a Scalar parameter in your Material graph:

![Roughness scalar parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db11b88c-39ca-42e1-8fe8-2554c5143d5a/roughness-scalar-parameter.png)

Name the parameter **Roughness** and connect it to the corresponding [Material input](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine).

#### Default Value and Value Range

If you want to set a default value for the parameter or limit the value range, you can do so in the Details panel.

![Default values Roughness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de1c24e0-d6fc-4a66-bc62-1153f68824ce/roughness-default-values.png)

For example, the Roughness input accepts a value from 0 to 1. To make sure the Roughness parameter always stays within this expected range, set the **Slider Min** and **Slider Max** values to 0 and 1.

If you want a default Roughness value other than 0, enter it in the **Default Value** field.

Select the Roughness parameter and press **Ctrl+D** to duplicate the node. Rename the second scalar parameter **Metallic** and connect it to the appropriate input. Your graph should now look like this:

![Metallic and Roughness parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a42adf9-552d-438e-9307-1bbbdec88cba/metallic-roughness.png)

### Converting a Node into a Parameter

You can also convert standard Material Expressions into parameters within an existing Material graph.

For the sake of demonstration, place a **Constant3Vector** node in your Material graph. This is a standard (non-parameterized) Material expression, which is often used to define the Base Color of a Material.

![Insert Constant3 Vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93ab52cf-08df-432a-b44f-6bad912edf45/constant-3-vector.png)

To convert this node into a parameter, **right-click** the node and choose **Convert to Parameter** from the contextual menu.

![Convert to parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dafe552-e16d-4f82-9bad-25f9c1b5fedc/convert-to-param-ue5.png)

Remember to give the parameter a unique, descriptive name like BaseColor. The naming field is selected automatically when you convert a node.

![Rename parameter in details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67cc43bd-de09-4f5a-b57b-18742b43fdf9/rename-parameter-details.png)

You can change the color in the **Default Value** field shown above, or you can double click the BaseColor node to open the color picker.

![Color picker interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb0b4884-50e3-42e1-b9d0-3718abba0807/color-picker-interface.png)

You cannot parameterize every Material node in Unreal Engine, but the **Convert To Parameter** option is available from the right-click menu for any Material expression that can be parameterized.

### Parameterized Material Example

Your Material graph should now contain a Vector parameter plugged into BaseColor and two Scalar parameters, plugged into the Metallic and Roughness inputs:

![Parameterized Material example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/518aff68-6e37-4040-b416-ade1fe8d3b8f/parameterized-material-example.png)

These three parameters will allow you to change the color, roughness, and metallic properties of the Material once you create a Material instance.

Click **Apply** in the upper left corner of the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-ui) to compile the Material, and then click **Save**.

![Compile Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/170dc30f-ebf4-475c-bd85-830d878827ee/apply-and-save-ue5.png)

## Creating a Material Instance

Now that you have a simple parameterized Material, you can create Material instances and customize them in the [Material Instance Editor](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui).

To create a Material instance, right-right click your Material in the Content Browser and choose **Create Material Instance** from the menu.

![Create Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/428194c4-0a6a-453e-95a0-b83ae031d8b0/create-material-instance-ue5.png)

Your Material instance will derive its name from the Material that you are using to create it. You can rename the Material instance by selecting it and pressing **F2** or by **single-clicking** the name field.

![Rename Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68caf338-7c3d-4f33-a736-9d3b4582f88d/rename-material-instance-ue5.png)

## Editing a Material Instance

**Double-click** the Material instance in the Content Browser to open the **Material Instance Editor**.

![Open Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1aa63e3-9b07-4835-a1a9-7547a0d396d0/double-click-instance.png)

The Material Instance Editor is the interface where you can customize Material parameters to produce different looking variations of your parent Material.

A Material instance in the Material Instance Editor.

### Adjusting Material Parameters

Material Parameters are found in the Details panel on the right side of the Material Instance Editor. Note that these parameters take their names from the parameter nodes in your original Material graph.

Use the following steps to edit a parameter:

![Override Material Parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bca6136-8f54-4f62-aefb-0ea064925717/override-parameters.png)

1.  Place a check in the box next to the parameter to enable it for editing.
2.  Type a new value in the field or left-click and drag to slide the value up and down. For Vector parameters, left-click the color swatch to activate the color picker.
3.  To reset a parameter to its default value, click the arrow icon pictured here.

As you adjust parameters, the Material preview will update in real-time in the Material Instance Editor, and in the Level if the Material is currently applied to any Actors.

## Using Parameter Groups

You can sort your parameters into **Parameter Groups** to improve the organization and readability of your Material instances.

While the above example with only three parameters is easy to read, heavily parameterized master Materials can be inefficient to interact with if you do not use parameter groups.

The slider below shows a Material instance with and without groups. In the example without parameter groups, scalar parameters appear in a single unorganized list. The instance with parameter groups is neatly organized by Material attribute.

![Material Instance without Parameter Groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c479c5a9-ff84-40bb-9ff5-27910956e225/without-groups.png)

![Material Instance with Parameter Groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb01ea72-5b20-4a45-94e5-2201861c2412/with-groups.png)

### How to Use Parameter Groups

Parameter groups are configured within the parent Material, not within the Material instance. This is done in the details panel of the Material Editor.

Select a Material parameter node in your Material graph.

![Color tint Vector 3 Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f9f4adf-ac62-4df7-9b56-63b7fcf7d487/tint-parameter.png)

In the Details panel, type a name into the **Group** field. You can name your groups however you wish, but one suggestion is to group parameters by the Material attribute they control.

![Base color parameter group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de41a456-cd8b-4b51-abeb-02a3174d077c/base-color-group.png)

Once you assign a parameter group name to one Material parameter expression, that name will appear in the drop-down menu next to the Group field.

For the rest of your parameters, you can either type in new group names or select one of the existing parameter groups from the drop-down menu.

![Select existing parameter group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e029ac9-ee2a-4556-a704-e8ab85c42294/parameter-group-dropdown.png)

### Ordering Parameters Within Groups

You can use the **Sort Priority** field to change the order that parameters are listed within a group. By default all parameters are listed alphabetically, which can lead to clumsy or inefficient ordering in the Material Instance Editor. In the slider below, the UV tiling and offset controls are broken up when listed alphabetically, but by assigning a sort priority value to each parameter the experience is improved.

![Alphabetical parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2361f55b-4b96-4eb4-88e8-441468422525/uv-controls-unordered.png)

![Reordered parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a7ac028-f965-458c-a77a-0f1ec73ee110/uv-controls-reordered.png)

To change order of a parameter, select the node and enter a new value in the **Sort Priority** field in the Details Panel.

![Parameter group sort priority](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ad094f8-a6c4-4eea-81e8-8db013f500f1/sort-priority.png)

### Ordering Parameter Groups

By default, parameter groups appear alphabetically in the Material Instance Editor.

There are two ways to change the order of your parameter groups. One solution is to simply add numbers to your group names.

The Megascans parent Material uses this approach, with parameter groups numbered from **00 – 07**.

![Megascans Parameter Groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbc37e4a-fbcb-4dbe-af86-cf460ba98f04/megascans-group-sorting.png)

This allows the parameter groups to display in the same order they appear in the Main Material Node.

#### Group Sort Priority

You can also use the **Group Sort Priority** property in the details panel to change the order of your parameter groups. This property is found in the parent Material, not in the Material Instance.

1.  Deselect all nodes in the Material Graph to access its Material Properties.
2.  In the Details Panel, expand **Group Sorting**, and then **Parameter Group Data.**
3.  The array in this section lists all the parameters in your Material. Expand each Index and change the **Group Sort Priority** to modify the order of the groups.
    
    ![Group Sort Priority](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5da580b6-49c9-4945-a914-c9f9f4c00a33/parameter-group-sorting.png)

## Changing the Parent Material of a Material Instance

You can easily change the parent Material used by a Material instance, in the Material Instance Editor.

To change the parent Material, open a Material instance in the Material Instance Editor. Under the **General** section in the Details panel, find the **Parent** property.

![Parent Material Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/721c5bf6-23d5-4e90-bee7-d8d21ad1fc50/parent-material-ue5.png)

Use the drop-down menu to search for and select a different parent Material. You can also select a Material in the Content Browser and click the **Use Selected Asset in Content Browser button** (left-facing arrow).

Note that if you change the parent Material it can completely change the appearance and properties of the Material instance. The parameters you were using before may no longer be available in the new parent.

![Change parent Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9b24ac2-fe33-48c0-98ba-0b95bad4e332/change-parent.png)

For example, if you select the **M\_Metal\_Gold** Material from the drop-down list, the three parameters that were present in the **M\_Parameterized** example (roughness, metallic, base color) are no longer available in the gold instance.

![New parent Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68ac9e22-e728-43ed-a84f-d6609b0e0038/new-parent-gold.png)

## Conclusion

Material Instancing is a powerful tool that you can use across all aspects of your project. From helping to add some variation to weapons and props, to helping artists make better use of available Materials, Material Instances can help to streamline and unify how Materials are created and used in your project.