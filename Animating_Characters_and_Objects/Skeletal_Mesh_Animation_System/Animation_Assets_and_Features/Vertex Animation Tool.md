# Vertex Animation Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vertex-animation-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/vertex-animation-tool-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:55

---

Storing complex animation data into 2D Textures or a meshes UV's is a great way to reduce animation overhead while still maintaining the required look and feel of the animation. In the past you might have used [Morph Targets](/documentation/en-us/unreal-engine/static-mesh-morph-targets-in-unreal-engine) to do the exact same thing, however this new method has a few advantages that Morph Targets do not. One of those advantages is allowing you to use complex animation data inside systems that would not otherwise be capable of utilizing Morph Targets like the Cascade Particle Editor. In the following documents we will cover how you can use this script to generate content for your projects.

## Prerequisites

Before we can begin using the script there are few things to be aware of so you can get the best results possible when using this technique.

### Script Location

The Vertex Animation Script will be in the following location and is called **VertexAnimationTools.ms.**

```
		`Engine\Extras\3dsMaxScripts\VertexAnimationTools.ms`

Copy full snippet
```
Engine\\Extras\\3dsMaxScripts\\VertexAnimationTools.ms

The newest version of the Verext Animation Script has been updated to correct for the way 3Ds Max 2014 and later handle image gamma.

### Tool Caveats

While this tool is very good at reducing animation overhead by storing complex animation data into a texture, there are a few drawbacks to using the tool. First of all the tool can only affect a maximum of **8192 vertices** in a single 2D Texture. This is because the maximum Texture size a Texture can be for DirectX 11 is 8192 pixels in either the X or Y direction. The tool generates the data in the Texture using the following formula.

```
		`Final texture resolution:  X = number of vertex in the mesh, Y = Number of frames captured.`

Copy full snippet
```
Final texture resolution: X = number of vertex in the mesh, Y = Number of frames captured.

Due to this limitation this tool is best suited for Visual Effects or ambient Static Meshes that require animations but might not justify using a complex animation rig to do so. This tool will also **not work** with Skeletal Mesh Animations as the bone transforms are not available to the Material Editor. This means that if you want to affect the vertices of a Skeletal Mesh in a similar manner you will need to use [Morph Targets](/documentation/en-us/unreal-engine/static-mesh-morph-targets-in-unreal-engine) instead.

### Vertex Animation Tools Break Down

Inside of the Vertex Animation Tools you will find two entirely different methods for affecting the vertices of Static Meshes. In the following section we will go over what these two methods are and how they differ from one another.

-   **Vertex Animation Tools:** The top section of the Vertex Animation Tools, called Vertex Animation Tools, is for generating a 2D Texture that will store the morph target vertex positions and normals.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15d7fa6f-2445-4a2e-b756-3689ef59502f/vat_tool_breakdown_01.png)
    
    | Property Name | Description |
    | --- | --- |
    | **Animation Options:** | Animation Options allows you to pick between using animation that was created using the Timeline in 3Ds Max or use individual Key Frame Meshes that were created in 3Ds Max or another 3D package like Maya or Blender and then exported out of that package frame by frame so the animation could then be re-constructed inside 3Ds Max. |
    | **Process Animated Meshes:** | This button will process the animated meshes that are in the 3Ds Max scene, creating and then exporting the required Textures. |
    | **Anim Start:** | This option defines the frame that the animation should start from. |
    | **Anim End:** | This option defines the frame that the animation should end on. |
    | **Frame Skip:** | This option allows you skip frames to try and save on Texture space. |
    | **Process Selected Meshes:** | This option, only available if Key Frame Meshes is enabled, will process the selected Key Frame Meshes in the order that they were selected. |
    
-   **Sequence Painter:** The Sequence Painter does something similar to the Vertex Animation Tool's but with one key difference, the information for the vertices positions is stored in the meshes UV's instead of a 2D Texture.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fb35f8a-242e-469f-bf79-1b2965ce8c54/vat_tool_breakdown_02.png)
    
    | Property Name | Description |
    | --- | --- |
    | **Paint Selection Sequence:** | This stores the information about the meshes Vertices inside of the meshes UVs instead of storing that data in a 2D Texture. |
    

### 3Ds Max Version & Script Installation

This tool has only be tested using **3Ds Max 2015**. While it might be able to work with other 3Ds Max versions, none of them have been tested so use other version of 3Ds Max at your own risk. To install the script just drag it from its location in **4.8\\Engine\\Extras\\3dsMaxScripts** right into the 3Ds Max viewport and the script will launch itself.

If you find that you are using this script a lot you can always add the script to one of the tool bars or quad menus. If you are unfamiliar how to do this the [Autodesk site has a very detailed walk through](http://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/3DSMax/files/GUID-A2CF8BAA-7B52-40A8-8C40-803B1AB5FC05-htm.html) that will explain how you go about doing this.

## 3Ds Max Unit Setup

Before we can begin to use the tool we need to first ensure that the units of measurement 3Ds Max uses is setup to correctly match the units of measurement UE4 uses. This way we can ensure that the data the tool exports from 3Ds Max will work in the same manner inside UE4. Since UE4 uses Centimeters for its default unit of measurement we will need to ensure that 3Ds Max uses this as well and to change this we must do the following.

1.  First open up 3Ds Max 2015 and once loaded from the Main Toolbar select **Customize** > **Unit Setup**.
2.  Next click on **System Unit Setup** and change the **System Unit Setup** from Inches to **Centimeters** and then press the **OK** button.
3.  Finally change the **Display Unit Scale** to **Generic Units** and then press the **OK** button.

It is extremely important that you **DO NOT** skip this step. Skipping this step could result in rendering errors when the content is imported into UE4 because UE4 and 3Ds Max's units are not the same.

## Tool Choices

The Vertex Animation 3Ds Max script offers two different ways to store the vertex animation data. One method will store the vertices positions in a 2D Texture while the other method will store the vertex position data in the UV's of the mesh. Below you will find links that show you how to setup and use both methods.

[Key framed Method](/documentation/en-us/unreal-engine/vertex-animation-tool---key-framed-meshes-in-unreal-engine) - This method uses individual key frames that can be exported from other 3D packages and imported into 3Ds Max. That information is saved to the meshes UVs.

[Animation Timeline Method](/documentation/en-us/unreal-engine/vertex-animation-tool---timeline-meshes-in-unreal-engine) - This method uses the 3Ds Max animation timeline and the results are encoded into a 2D Texture.

## Tips & Tricks

To get the most out this technique, there are a few tips and tricks that you can follow which are outlined below.

### Speeding Up the Animation Play Rate

If you feel that the rate at which the animations are playing is to slow, you can use the **TimeWithSpeedVariable** Material Function to speed up the play rate. To do this just plugging the output of the **TimeWithSpeedVariable** into the **0-1 Animation** input if you are using the **MS\_SequencePainter\_SequenceFlibook** Material Function. If you are using the **MS\_VertexAnimationTools\_MorphTargets** Material Function plug the output of the **TimeWithSpeedVariable** into the **Morph Animations** input.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfb998ab-6ebe-4612-8597-a17381d4e991/vat_sp_speed_up_time.png)

### Multiple Animated Meshes

You can select multiple animated meshes at a time and the script will bake all of that data down to one mesh and one set of Textures. This is very useful when working with characters that are made up of different parts. Just select the parts that you want to use and the run the script like normal. The script will then combine the pieces you selected and generate a new mesh from them along with the required 2D Textures.

### Frame Skip

Using the **Frame Skip** option that is under the **Vertex Animation Tools** section of the script will allow you to skip certain frames. This is a very useful option as it allows you to reduce the final Texture size while still maintaining the look and feel of the original animation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/549ad873-e95a-4a3b-a6b4-6884ae72ec38/vat_frame_skip.png)

If we take a look at the example video below, we can see the Frame Skip feature in action. The first Teapot you see in front of the word, Original, shows how the Teapot will animate using the full frame range. The next Teapot, with the number 2 in front of it, shows how the teapot animates skipping every 2nd frame and so on. As you can see the last example, the effect will still maintain its look and feel even if you skip 10 frames.

| Mesh Name /Number | Texture Size | Memory Savings |
| --- | --- | --- |
| Original | 175 KB | N/A |
| 2 | 59 KB | 116 KB |
| 5 | 30 KB | 145 KB |
| 10 | 21 KB | 154 KB |

## Technical Information

The following section is for technical information about how the Vertex Animation script works. Please note that this is here purely for reference or for people who would like to know more about how the script works in case they want to modify it.

### Limitations

Vertex positional morph target information is stored in a 16 bit signed floating point file format. A 32 bit image would be more precise but 16 should suffice for most FX work. With that said, the offset vertex positions will be less precise as they move further away from their resting positions.

Also note that the scripts Textures should be sampled using the nearest neighbor method.

### Memory Usage

The memory usage for each frame per vert is as follows :

-   Vertex Offset Texture: 8 bytes per vertex per frame (each pixel)
-   Normal Texture: 4 bytes per vertex per frame (each pixel)