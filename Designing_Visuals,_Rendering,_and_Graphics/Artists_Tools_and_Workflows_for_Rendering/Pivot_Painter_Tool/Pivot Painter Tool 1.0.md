# Pivot Painter Tool 1.0

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pivot-painter-tool-1.0-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pivot-painter-tool-1.0-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:05

---

The latest version of the [Pivot Painter Tool](/documentation/en-us/unreal-engine/pivot-painter-tool-2.0-in-unreal-engine) can be found here. Version 2.0 offers a simplified pipeline to create interactive foliage.

The **Pivot Painter Tool** is a MAXScript that stores model pivot and rotation information in the model's vertex data. That information can then be referenced inside of Unreal's shader system to create interactive effects.

The motion shown in the sample video is generated in real-time using vertex shaders. Each blade of grass rotates and bends around its root. The trees branches and leaves form a hierarchy and animate around their individual pivots points, while inheriting the parent's motion. The sub-objects rotation is stored as well, which allows for realistic dynamic reactions to wind forces.

Creating these shaders has been made much simpler with the addition of the Pivot Painter material functions. Sample content also helps by showing how an animation, like the one featured above, can be generated. Retrieving sub-object pivot points is now simply a matter of processing a mesh in 3ds Max with the Pivot Painter script, importing the file and creating a material using the Pivot Painter functions. The material functions contain pivot point outputs for both two level hierarchies and single level hierarchies.

Creating motion this way has its benefits. A model processed using this technique is only 18% larger in terms of memory than a standard Static Mesh. Animations are far less expensive than skeletal animations because they do not need to be stored as they are calculated on the fly. Vertex shader instruction counts are generally less of a performance concern than pixel instruction counts, due to the number of vertices on a model compared to the number of pixels on the screen.

The example shaders in the link below are only the tip of the iceberg in terms of what is possible. Experimenting with the information available may entice one to explore the other possible uses. Player interaction, interesting wind sources, non-foliage related motion and other effects are all possible when given access to sub-object level information.

## Installation

You can find the **Pivot Painter** script in the following location:

```
	`[UERootDirectory]/Engine/Extras/3dsMaxScripts/PivotPainter.ms`

Copy full snippet
```
\[UERootDirectory\]/Engine/Extras/3dsMaxScripts/PivotPainter.ms

This video covers installing the script and creating a keyboard shortcut and menu to open the Pivot Painter tool.

## Prep Tools

This video will cover the "Prep Tools" section of the script as well as workflow tips and information about the overall process. Prep Tools contains options to detach model elements as separate objects and several tools to help create new pivot points easily.

The **Prep Tools** are designed to separate a given models elements into a series of new models and to move their pivots into ideal locations. It is not necessary to use these tools. They are simply provided for convenience. If the model being processed is already separated, its pivot is located at the point from which it is supposed to rotate, and the models X axis is facing down the length of the model, then your model is good to go to the next step.

**Example:** A clump of grass should be separated into its individual blades. A given blade of grass should rotate around its base when blown around by wind. So its pivot point should be located at the grass models base and the x axis of the pivot should point down the length of the model - in most cases with grass that would be upward.

## Hierarchy Painter

This video covers the "Hierarchy Painter" segment of the script. This portion of the tool is used to store child parent relationships like the relation between a branch and leaf for instance, as well as the model pivot and rotation information in the meshes.

Models should only be processed with the "Hierarchy Painter" section of the script if the model requires a hierarchy. A tree with leaves is a good use case whereas grass is not. Grass should be painted with the "Per Object Painter" section.

Also, branches/parent pivots need to be positioned within a box as described by "Max dist for parent piv". For instance: if "Max dist for parent piv" is set to 4096 when the model is painted, then a branch/parent objects pivot point can be located anywhere within negative or positive 2048 in x and y and from 0 to 4096 on the z axis. Additionally, if "Max dist for parent piv" is set to anything other than 4096 during the model processing stage, that same number should be used within the models shader in unreal.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c866d92-09b9-4907-a9a2-11d810c21932/pivotpainter_hierarchydata.png)

## Per Object Painter

This video goes over the options available under the "Per Object Painter" script section. It also discusses some of the possible uses and some information about how the data is stored on the model.

## 3ds Max Example File

The file contains a copy of the tree used in the video tutorials.

-   [https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/6b515f17-47b9-474a-84cf-5619b5d0f428/tree.max](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/6b515f17-47b9-474a-84cf-5619b5d0f428/tree.max) (**right-click**, then select **Save As** to download)

## Requirements

-   3ds Max - The script has been tested using 3ds Max versions 2010 and 2012.
-   The Pivot Painter material functions. It is possible to use the script without the functions but they make the data far easier to use.

## Other Notes

You should only process your models with either the "Hierarchy Painter" or "Per Object Painter" section of the script but not both. If you paint your model with "Hierarchy Painter", then the "PivotPainter\_HierarchyData" material function should be used within the objects material. If the "Per Object Painter" section of the script is used, then "PivotPainter\_PerObjectData" should be used to decode the pivot information within the material.

3ds Max's world unit settings should be set to centimeters when painted and not scaled/changed on export. It is important to maintain scale between 3ds Max and Unreal. Not doing so will produce undesirable results.