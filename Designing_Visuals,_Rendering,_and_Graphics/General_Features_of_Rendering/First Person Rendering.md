# First Person Rendering

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/first-person-rendering](https://dev.epicgames.com/documentation/en-us/unreal-engine/first-person-rendering)  
**Processed:** 2025-06-14 16:23:45

---

Native first-person rendering supports functionality often required when creating experiences using a first-person camera perspective, such as being able to render only certain objects with a field of view that differs from the one rendering the rest of the scene. For example, rendering things like the character's hands and arms or weapons are ideal for first person rendering so that they don’t clip with (protrude into) walls as you get close to them. 

The First Person rendering offers the following features:

-   Render first person primitives with a custom field of view (FOV).
    
-   Apply a scaling factor to first person primitives to effectively shrink them closer towards the camera, making it possible to avoid most cases where first person geometry would intersect, often called clipping, with the scene. This enables first person primitives to always render on top of the scene.
    
-   Includes a complete shadowing solution where first person geometry receives scene shadows, it casts shadows on itself, and players can see their own shadow being cast onto the scene.
    
-   Has integration with [Hardware Ray Tracing](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) (HWRT) whereby players can see themselves reflected in the scene, and they can cast ray-traced shadows.
    
-   Integration with materials:
    
    -   Per-vertex control over the first person effect. This optional output allows for interpolating between world space and what is considered first person space. It is useful when there is a need to have some parts of the geometry be in world space to connect with the world, such as having the characters feet on the ground.
        
    -   Use the material graph to query first person rendering parameters and to transform arbitrary positions from world space into first person space.
        

-     It works on most primitive types. This includes static meshes, skinned meshes, and [Niagara Particle Effects](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine).
    

## First Person Rendering Implementation

For development of first-person games, you usually want the player camera to render first person geometry in a way that it has a custom field of view and does not intersect with the world. The implementation of First Person rendering in Unreal Engine can be thought of as morphing the first-person geometry in such a way that it achieves the desired effect of a custom field of view and has anti-clipping behavior. This morphing happens after World Position Offset is applied but before the vertex is projected into clip space.

Consequently, the geometry technically exists in world space but for the most part looks like it is rendered with a different projection matrix. The caveat here is that the geometry is now very small and slightly skewed. This is done so that it will look good from the point of view of the camera, but it is unsuitable for other perspectives and therefore shouldn’t cast shadows on the scene or be visible in hardware ray tracing reflections — which is prevented by design.

The advantage of implementing First Person rendering in this way is that it allows first person primitives to render in the same pass as other primitives, thus avoiding the need for, or the complexity of, additional rendering passes which would have an impact on memory and performance.

### First Person Primitives Settings

Components include a setting to determine how they are rendered by the first-person camera when their **First Person Primitive Type** is set to **First Person** or **World Space Representation**. 

[![](https://dev.epicgames.com/community/api/documentation/image/8ce03764-6fed-47b8-8f39-4493c52c4185?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8ce03764-6fed-47b8-8f39-4493c52c4185?resizing_type=fit)

First Person settings for Primitives.

This setting includes the following selection: 

-   **None:** This primitive does not interact with first person rendering.
    
-   **First Person:** This primitive is rendered as first person and is affected by first person properties on the camera for First Person Field of View and First Person Scale, which are used to render the component with different fields of view and smaller depth range such that clipping with the scene can be avoided. The primitive does not cast shadows onto the scene and will also not be visible in the raytracing world.
    
-   **World Space Representation:** This primitive represents a first person primitive in world space. This is the primitive that other players would see and is used to cast shadow onto the ground and for reflections with hardware ray tracing, among other things. It is invisible to the owning first person camera. This implicitly sets Cast Hidden Shadow to false and Owner No See to true behind the scenes, which is required for first person shadow to work correctly with Virtual Shadow Maps.
    

### First Person Shadows

There are two considerations for shadowing you need to take into account when setting up a player character using first person rendering: 

-   Enabling lights to cast shadows so that primitives set to First Person can cast shadows onto themselves.
    
-   Setting up components that are the world space representation of first person primitives for scene shadows and reflections.
    

#### First Person Self-Shadow

**First Person Self-Shadowing** is a specialized shadowing solution for primitives rendered in first person perspective. It enables these first person primitives to cast shadows on themselves, such as a weapon casting a shadow onto itself and the player’s arm, but not onto the scene. This prevents the geometry that is morphed and skewed to the first person camera perspective from being visible in the scene shadows. 

Currently, first person self-shadowing is implemented with screen space tracing. While this method is fairly cheap, it is limited to only shadow casters on screen. For most first person setups this won’t be a problem in practice since  all relevant shadow casters are usually on the screen. Keep in mind that other typical limitations of screen space rendering also apply to first person rendering, such as a single layer depth buffer (rays can go behind geometry). 

Below are examples with a Directional light that has enabled First Person Self Shadow.

![First Person Self-Shadow: Disabled](https://dev.epicgames.com/community/api/documentation/image/a3868e44-becf-40aa-ac84-56b6afe12239?resizing_type=fit&width=1920&height=1080)

![First Person Self-Shadow: Enabled](https://dev.epicgames.com/community/api/documentation/image/7a8b89c4-a0b1-42fe-8f11-6db8d8637239?resizing_type=fit&width=1920&height=1080)

First Person Self-Shadow: Disabled

First Person Self-Shadow: Enabled

First Person Self-Shadow is currently (as of 5.6) controlled with console variables. This was done to make it easier to control the effect in maps with many lights. The effect only actually costs performance if the light overlaps the first person geometry, so assuming there are little to no overlapping lights, it’s fine to enable it on all local lights. However, this means of controlling the feature might change in the future.To set up First Person Self-Shadow, follow these steps: 

1.  Set `r.FirstPerson.SelfShadow` to **`1`**. This enables the feature on shadow casting lights (Cast Dynamic Shadows) as determined by the following console variable:
    
2.  Set `r.FirstPerson.SelfShadow.LightTypes` to:
    
    1.  `0`, enabling First Person Self-Shadow only on directional lights
        
    2.  `1`, enabling it on local lights only
        
    3.  `2`, enabling it on all lights (local and directional)
        

Enabling **First Person Self Shadow** does have some small impact on performance. Having many overlapping lights with it enabled might affect performance negatively. Be mindful of the light sources you’re enabling this on. For additional info on limitations of this feature, see the [Limitations](https://docs.google.com/document/d/1bpB1RC9AwW5TfIGOOEpOjGn37kZnBaA9cTUq5Gdeaag/edit?tab=t.0#heading=h.omf7u01n5o43) section below. 

#### First Person World Space Representation Shadows

When you have a first person player character that has the property **First Person Primitive Type** set to **First Person**, shadows are not cast onto the scene from these components. Having a mesh that is seen by the world and other players is necessary to cast a shadow, and its primitive type must be set to **World Space Representation**. Once set, this mesh will cast shadows onto the scene, along with making this primitive visible in hardware ray-traced reflections.

### Setting Up A First Person Camera

When setting up a camera for first person rendering, the complexity depends on the type of game or experience you’re building. You can follow along with the basic setup below to get you started with a first person player character. The advanced setup offers guidance on setting up parts of your character that are viewed by the world, or other players in a multiplayer game. 

For example, in a basic setup, you would set up a character with only components you would see while in a first person perspective. This can be a skeletal mesh with only arms to hold a weapon. In an Advanced setup, you can add to this by adding visible legs in first person and a full character mesh that is visible to the world for casting shadows and appearing in reflections. 

#### Basic Setup of a First Person Camera

The process of creating a First Person camera setup is fairly straightforward; primitives can be tagged as being first person and cameras can be configured to apply a custom field of view and scaling to these assets separate from the rest of the scene’s rendering. 

The steps to do this can be broken up into two categories: 

-   Setting up the components and their initial settings.
    
-   Configuring properties of these components to fit the look of your primitives and first person game
    

#### Setting up the Camera and First Person Components

Follow these steps to set up the camera and its first person components:

1.  Create a new **Camera** actor.
    
2.  In the Details panel, click **Add** and select a desired **Primitive** component (Static Mesh, Skeletal Mesh, Particle System, and so on) to add to this actor.
    
    [![Add a primitive component.](https://dev.epicgames.com/community/api/documentation/image/140f328a-840e-4c99-8dbd-97fe966bd4ac?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/140f328a-840e-4c99-8dbd-97fe966bd4ac?resizing_type=fit)
    
    1.  While this is not necessary, it’s considered a good idea to do so because it ensures that the camera is the owner of the first person primitives, which is an important property for more advanced setups where the flags for **Owner No See** and **Only Owner See** are required.
        
    2.  With the Primitive component selected, use the **Details** panel to locate the property **First Person Primitive Type** under **Rendering > Advanced** properties. Use the dropdown selection to set it to **First Person**.
        
        [![Set the First Person Primitive Type to First Person.](https://dev.epicgames.com/community/api/documentation/image/4fe848ee-bf4f-4eb2-88dd-842799450795?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4fe848ee-bf4f-4eb2-88dd-842799450795?resizing_type=fit)
        
    3.  In the Details panel, click on the **Camera Component** and check the boxes next to **Enable First Person Field Of View** and **Enable First Person Scale** under **Camera Options** properties.
        
        [![Enable First Person Field of View and First Person Scale on the Camera Component.](https://dev.epicgames.com/community/api/documentation/image/709ad4dc-f4ae-4e47-9c29-96d6c7018914?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/709ad4dc-f4ae-4e47-9c29-96d6c7018914?resizing_type=fit)
        

With the **Camera Component** selected, you can observe the results in the camera preview window in the bottom-right corner of the editor viewport.

[![First Person Camera view result.](https://dev.epicgames.com/community/api/documentation/image/24c3f24c-394d-4a77-b14e-f61c3cdd2c79?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/24c3f24c-394d-4a77-b14e-f61c3cdd2c79?resizing_type=fit)

#### Configuring First Person Field of View and Scale Settings

When you’ve enabled the Camera Component properties for **Enable First Person Field of View** and **Enable First Person Scale**, you can use the similarly named settings under the **Camera Settings** category to make adjustments.

[![First Person field of view and scale camera settings.](https://dev.epicgames.com/community/api/documentation/image/c666fee7-23d0-4884-a04b-3f6cd1ad1a21?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c666fee7-23d0-4884-a04b-3f6cd1ad1a21?resizing_type=fit)

First Person Field of View and First Person Scale camera settings.

These settings will work for this camera on any primitives that have had their **First Person Primitive Type** set to **First Person**. Otherwise the camera will see them in World Space. Use the Camera Preview window in the viewport to inspect the changes. The editor viewport still shows any First Person primitive as unchanged. This is because the implicit camera used for the viewport does not have the first person properties set up. 

You can adjust the **First Person Field of View** value to change the horizontal field of view (in degrees) of any primitives this First person camera renders. When you adjust the field of view slider, you can observe the primitive’s field of view changing in the camera preview window. 

You can adjust the **First Person Scale** value to scale down “first person” primitives towards the camera such that they are small enough to not intersect with the scene for this First Person camera. From the camera’s point of view, the primitive should look the exact same, even though it’s now smaller. When the scale value is too small, the primitive will disappear. This is because it’s been scaled small enough that it intersects the near clipping plane.

When adjusting the scale for a proper setup with your camera and primitives, you should find a scale value that is small enough to not cause clipping with the scene but that is big enough to not disappear because of the Near Clip Plane. In practice, it is often sufficient to scale down the first person geometry only as much as is required for it to be contained in the player bounds.

Depending on your content and setup, it may be necessary to adjust the Near Clip Plane’s default value for the editor. You can adjust this in the project settings under **Engine > General** settings with the **Near Clip Plane**, but this does adjust it globally for the entire project.  

The advanced setup of the First Person camera and components is similar to how you would set up this view using the basic setup outlined above. When using the advanced setup below, you'll want to consider how the character is represented in the world for a multiplayer game or how they're represented in game scenes using hardware ray tracing features. This will ensure consistency between how the player is seen by the world — or other players — around them. It also affects how the player sees their character in shadows and reflections.

Consider the following when using the advanced first person workflow: 

-   Adding World Space Representation primitives for casting shadow onto the world.
    
-   a character's feet in first person and having the feet connect to the shadows cast by the player onto the ground.
    
-   Player reflections when viewing themselves with hardware ray-traced reflections.
    

All of these features require a suitable representation of the first person primitives in the world. That representation is what other players would see in a multiplayer game when they look at this player. Alternatively, you can think of this as the third-person version of the player character. In Unreal Engine, this is called the **First Person World Space Representation**. It is used to cast shadows onto the scene and is how the player is represented in the raytracing scene.

#### First Person Geometry

First Person geometry should include a mesh for the lower body and legs. This mesh can either be completely in World Space or could use an interpolation gradient in the material to have the feet fully in World Space, and the rest of the body in First Person space (see the [Integration with Materials](https://docs.google.com/document/d/1bpB1RC9AwW5TfIGOOEpOjGn37kZnBaA9cTUq5Gdeaag/edit?tab=t.0#heading=h.gsqdca9vnkhz) section below). 

This setup alone will improve realism as players can now see their own legs when looking down in First Person view.

#### Set Up of First Person Components and Their World Space Representations

In the [Basic Setup of a First Person Camera](https://docs.google.com/document/d/1bpB1RC9AwW5TfIGOOEpOjGn37kZnBaA9cTUq5Gdeaag/edit?tab=t.0#heading=h.3jwunk43ou84), the components you want seen by only the first person camera have their **First Person Primitive Type** set to **First Person**. For any geometry you want to be seen in world space by features like hardware raytraced reflections or other players in multiplayer games, you can set the primitive type to **World Space Representation**, and this ensures they can cast shadows onto the world and have player representation in ray-traced reflections.

In the scene below, there are two immediate things to be aware of when setting a component to **World Space Representation**: 

-   The component is no longer visible to the first person camera in the camera preview window.
    
-   The component casts a shadow onto the world.
    

[![First Person components and their world space representations.](https://dev.epicgames.com/community/api/documentation/image/fd9c5f06-5363-4f09-ade0-1026464d4401?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fd9c5f06-5363-4f09-ade0-1026464d4401?resizing_type=fit)

First Person components and their world space representations.

Behind the scenes, this World Space Representation option uses the “Owner No See” functionality to hide the geometry from the camera, but this requires that the primitives be owned by the camera, which can be achieved by making them child components of the camera actor. 

Once you have a character set up with a first person mesh primitive and a World Representation mesh primitive, the feet of your first person mesh should line up with its world representation. You can see an example of this set up below looking at the first person primitives only and then the combined first person and world representation primitives to cast shadows onto the scene and have them “connect” the shadows at the feet of your character.

|  |  |
| --- | --- |
| 
[![First person mesh only.](https://dev.epicgames.com/community/api/documentation/image/ad9a1e64-e25f-45fb-a667-34ae8447e47f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ad9a1e64-e25f-45fb-a667-34ae8447e47f?resizing_type=fit)



 | 

[![First person mesh with world representation mesh casting shadows.](https://dev.epicgames.com/community/api/documentation/image/35055168-2cb5-4657-8c74-56da1151bb51?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35055168-2cb5-4657-8c74-56da1151bb51?resizing_type=fit)



 |
| 

**Only the first person mesh primitive set the “First Person” is shown. This mesh doesn’t cast shadows onto the scene.**                                                                                                                                                                                                                                                                                                

 | 

**Both the mesh primitives set to First Person and World Representation are shown together. The World Representation mesh is invisible to the first person camera but casts shadows onto the world. These should line up with the First Person primitive mesh.**

 |

To the world, or any other players in a multiplayer setup, your character’s mesh and components should be set to World Space Representation. 

The demonstration below shows a “world” camera looking at the first person character reflected on a mirror-like surface. You can also see the first person camera view and how the world representation mesh is viewed when set to None, First Person, or World Space Representation and how this affects its ability to cast shadows on the scene, or be rendered by the first person camera.

## Integration with Materials

The material graph includes the following nodes that support first person rendering configurations:

### First Person Output Node

The **First Person Output** node uses an alpha value to interpolate between world space and first person space using values between 0 and 1 on a per-vertex frequency. This is very useful if first person geometry needs to connect to the rest of the scene. One example of this would be having the feet mesh of the first person character geometry connecting to the ground. You can achieve this by applying a gradient from 0.0 (world space) to 1.0 (first person space) along the length of the legs (which would be set as a first person primitive).

[![First Person Output material expression.](https://dev.epicgames.com/community/api/documentation/image/b8f9f43e-861b-4258-bb8d-a657a36343ab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b8f9f43e-861b-4258-bb8d-a657a36343ab?resizing_type=fit)

First Person Output material expression.

Alternatively, you can also use **Set Material Attributes** to set the same property without needing to add the First Person Output node to the material. This is useful in cases where you want to set the value from a material function, as material functions do not allow usage of custom output nodes.

[![First Person Set Material Attributes material expression.](https://dev.epicgames.com/community/api/documentation/image/7725c46d-17c7-48c0-939b-c3f944b0c117?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7725c46d-17c7-48c0-939b-c3f944b0c117?resizing_type=fit)

First Person Set Material Attributes material expression.

### Transform Position Node

The **Transform Position** node supports transforming arbitrary positions to first person space. This is useful for calculating where some point would end up on the screen when it is rendered as first person.

[![First Person Transform Position material expression.](https://dev.epicgames.com/community/api/documentation/image/13c1799d-14eb-49aa-aa0c-20e63796b4a8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/13c1799d-14eb-49aa-aa0c-20e63796b4a8?resizing_type=fit)

First Person Transform Position material expression.

With the node selected, use the **Details** panel to set the following:

[![First Person Transform Position settings.](https://dev.epicgames.com/community/api/documentation/image/6ef2208c-5093-458f-931e-fb2e4742a633?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6ef2208c-5093-458f-931e-fb2e4742a633?resizing_type=fit)

First Person Transform Position settings.

-   **Source:** Camera Relative World Space
    
    -   This is the source format of the position that will be transformed.
        
-   **Destination:** First Person Space (Camera Relative World Space)
    
    -   This is the type of transform to apply to the input expression.
        
-   **(Optional) First Person Interpolation Alpha:** 0 to 1
    
    -   This interpolates between translated world space and first person space, where 0 is world space and 1 is first person space. This node can be used in any material, including post process materials, where it can be used to transform any arbitrary position to first person so we can't know the value of the First Person Output node. This value is supplied by the user for what makes sense for their game, but in most cases, it is sensible to leave the default value.  
        
    -   An example of when to use this node is when calculating where the reticule should be at in first person for something like a scoped weapon's post process material. In this case, you can assume that every position that needs to be cared about (points on the gun and scope) will be fully in first person. 
        

### Is First Person Node

The **Is First Person** node can be used to apply different effects in the material depending on whether the current primitive being rendered has its **First Person Primitive Type** set to **First Person** or not.

[![Is First Person material expression.](https://dev.epicgames.com/community/api/documentation/image/f642ad77-80fc-451f-ae21-fc0765a0ee3a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f642ad77-80fc-451f-ae21-fc0765a0ee3a?resizing_type=fit)

Is First Person material expression.

The material graph below is a simple setup using the IsFirstPerson node to set a color for geometry that is rendered in World Space (red) versus First Person Space (green).

[![Example using the Is First Person material expression.](https://dev.epicgames.com/community/api/documentation/image/8b5f2a11-2e78-4e95-9279-ea4eb18475b4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8b5f2a11-2e78-4e95-9279-ea4eb18475b4?resizing_type=fit)

Example using the Is First Person material expression.

In the scene below, you can see how this material with the Is First Person node is used to drive the color of the rifle used for its world space representation and the first person view. The First Person Rifle primitive (green) is visible in the player camera (bottom right) and is rendered with the first person parameters on the camera. The World Space Representation Rifle (red) is invisible to the player camera, but it is used to cast shadow onto the ground and will be seen by hardware ray-traced reflections and shadows in the raytracing world.

[![Example scene using the Advanced Setup of a First person Camera with first person and world space representation mesh primitives.](https://dev.epicgames.com/community/api/documentation/image/f0d15bc2-5e87-480b-9857-4a2e11bcee84?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0d15bc2-5e87-480b-9857-4a2e11bcee84?resizing_type=fit)

Example scene using the Advanced Setup of a First person Camera with first person and world space representation mesh primitives.

### View Property Node

The **View Property** node can be used for querying the **First Person Field of View** and **First Person Scale** of the current view. 

-   **First Person Field of View** returns the horizontal and vertical first person field of view angles in radians.
    
    [![First Person Field of View material expression](https://dev.epicgames.com/community/api/documentation/image/448a88fd-471d-4781-924d-930945a69c9e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/448a88fd-471d-4781-924d-930945a69c9e?resizing_type=fit)
    
-   First Person Scale returns the scaling factor applied to first person primitives to keep them from intersecting with the scene.  
    
    [![First Person Scale material expression](https://dev.epicgames.com/community/api/documentation/image/1ddf2ce7-5c66-471a-a66b-41a0b00e24bc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1ddf2ce7-5c66-471a-a66b-41a0b00e24bc?resizing_type=fit)
    

With the node selected, use the **Details** panel to set the **View Property** dropdown list to the view you want to query.

[![First Person View Property Selection.](https://dev.epicgames.com/community/api/documentation/image/b31c7ef8-2160-4cdc-8e47-1647649a54dc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b31c7ef8-2160-4cdc-8e47-1647649a54dc?resizing_type=fit)

### Scene Texture Node

The **Scene Texture** node can sample the GBuffer to tell whether a given pixel was drawn by a first person primitive that uses an opaque material.

[![Scene Texture: Is First Person material expression.](https://dev.epicgames.com/community/api/documentation/image/d3183e2e-02b2-43e5-a6d5-7f67e4225ff2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d3183e2e-02b2-43e5-a6d5-7f67e4225ff2?resizing_type=fit)

Scene Texture: Is First Person material expression.

With the node selected, use the **Details** panel to set the **Scene Texture Id** dropdown list to set the scene texture to **IsFirstPerson.**

[![IsFirstPerson Scene Texture ID](https://dev.epicgames.com/community/api/documentation/image/df1bc449-eb66-4e5e-a08c-0719d3dc06ae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/df1bc449-eb66-4e5e-a08c-0719d3dc06ae?resizing_type=fit)

IsFirstPerson Scene Texture ID

  For additional info, see the [Limitations](https://docs.google.com/document/d/1bpB1RC9AwW5TfIGOOEpOjGn37kZnBaA9cTUq5Gdeaag/edit?tab=t.0#heading=h.omf7u01n5o43) section below.

## Limitations and Notes

-   The custom first person field of view (FOV), anti-clipping scaling, the per-vertex interpolation controls and most of the material graph integration features work on all platforms and in all configurations.
    
-   **First Person GBuffer Bit**
    
    -   Certain advanced first person rendering features require first person pixels to be marked with a bit in the GBuffer.
        
    -   The first consequence of this is that these features do not work with the mobile renderer or with forward rendering.
        
    -   The second consequence is that **Allow Static Lighting** needs to be **disabled** in the project settings. By disabling static lighting for the project, some GBuffer bits are freed up to be used by first person rendering.
        
    -   This might change in the future, but as of 5.6, this is a tradeoff that needs to be made. Alternatively, very advanced users could instead decide to do local changes to their version of Unreal Engine and instead sacrifice a different feature in the GBuffer that is not needed for their project.
        
    -   The impacted features are as follows:
        
        -   First Person Self-Shadow
            
        -   Using World Space Representation primitives to cast shadow onto the scene.
            
        -   Seeing World Space Representation primitives reflected in the scene.
            
        -   Using the Scene Texture node to tell whether a given pixel is first person.
            
    -   All these features have a graceful fallback in case the first person GBuffer bit is not available: Shadows and reflections will simply not be there and the Scene Texture node will always return 0.0 (false).
        
-   **General Feature Support**
    
    -   Without Virtual Shadow Map (or Ray-traced Shadows) there won't be first person shadows on the ground. 
        
    -   Grooms and strand-based hair is currently not supported.
        
    -   Nanite meshes are not yet fully supported. When set to first person, any primitives using Nanite will render their fallback mesh in the first person view instead.
        

## Additional Resources

### First Person Template

The **First Person Template** is setup to use native First Person rendering. You can explore the First Person Shooter variant when creating the First Person template to see this feature in action. 

For more information on this template, see [First Person Template](https://dev.epicgames.com/documentation/en-us/unreal-engine/first-person-template-in-unreal-engine).