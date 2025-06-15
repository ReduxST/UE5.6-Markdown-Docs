# Templates Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-templates-reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-templates-reference)  
**Processed:** 2025-06-14 16:57:09

---

When you create a new Unreal Engine project, you have the option to use one of the existing templates as a base for your game or application. Unreal Engine templates contain character controllers, Blueprints, and other features that work without the need for additional configuration.

To learn how to create a new project from a template, see the [Creating New Project](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) page.

When you select a template, you will see a description that tells you more about the template and what it contains. Scroll down to read the full description.

Example of a template description for the Handheld AR template. Click the image for full size.

You can also create custom templates from any one of your existing projects. To learn more, see the [Creating Custom Templates](/documentation/en-us/unreal-engine/converting-a-project-to-an-unreal-engine-template) page.

## Configuring Input for Playable Characters

Many templates include a character you can control using your keyboard, mouse, or controller. In Unreal Engine terms, this is called a Pawn.

You can view existing controls for your Pawn and configure new ones in the **Input** section of the **Project Settings**. To open it:

1.  From the main menu, go to **Edit > Project Settings.**
    
2.  In the left sidebar, scroll down to the **Engine** section, then click **Input**.
    

Expand the **Bindings** section to edit the:

-   **Action Mappings:** Defines the keys that control actions such as jumping.
-   **Axis Mappings:** Controls movement. Depending on the template, movement may be restricted on one or more axes. For example, in the Side Scroller template, the Pawn can only move left / right and jump.

## Available Templates in Unreal Engine

The templates in Unreal Engine are split into the following categories:

-   Games
    
-   Film, Television, and Live Events
    
-   Architecture, Engineering, and Construction
    
-   Automotive, Product Design, and Manufacturing
    
-   Simulation
    

Each of these categories also includes a **Blank** template, which consists of an empty project with no additional content and settings. This is the most basic template available.

### Games Templates

![Vehicle Advanced template in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c82430f-db7b-4758-96f1-e302afd09744/templates-vehicle-advanced.png)

Vehicle Advanced template in Unreal Engine 5.

Unreal Engine's **Games** templates offer quick starting points for various kinds of games such as first- and third-person, side-scroller, or driving.

Although these are tagged as "Game" templates, you can use them as a starting point for any kind of project. For example, you can use the VR Template to create a virtual reality walkthrough of a three-dimensional space. The Third Person template is generally a good starting point for many different kinds of projects.

| Template Name | Template Contents | Additional Documentation |
| --- | --- | --- |
| **First Person** | A first-person character armed with a gun that shoots physics-based projectiles. Player experience Level contents from the character's viewpoint. | [First Person Template Overview](/documentation/en-us/unreal-engine/first-person-template-in-unreal-engine) |
| **Third Person** | A third-person character and basic geometry. The camera is located above and behind the character. | [Third Person Template Overview](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) |
| **Top Down** | A character you move by clicking or tapping to a new location. The camera is in a fixed position above the character and follows their movement. |   |
| **Handheld AR** | A starting point for creating AR applications you can deploy to Android or iOS. Includes runtime logic for scanning an environment to gather data for creating interactive planes in the virtual scene, and lighting and scene depth information. | 
-   [Handheld AR Template Quickstart](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine)
    
-   [Handheld AR Template Technical Reference](/documentation/en-us/unreal-engine/handheld-ar-template-technical-reference)
    



 |
| **Vehicle** | A simple physics-driven vehicle with two different camera views — one inside the vehicle, the other above and behind it — as well as a HUD. |   |
| **Virtual Reality** | A starting point for all of your virtual reality (VR) projects in Unreal Engine 5. It includes encapsulated logic for teleport locomotion and common input actions, such as grabbing and attaching items to your hand. | 

-   [VR template](/documentation/en-us/unreal-engine/vr-template-in-unreal-engine)
    
-   [Developing for VR in Unreal Engine](/documentation/en-us/unreal-engine/developing-for-xr-experiences-in-unreal-engine)
    



 |

### Film, Television, and Live Events Templates

![DMX template in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fb7bbd2-10a3-48d7-be27-5a7d53c6a01b/templates-dmx.png)

DMX template in Unreal Engine 5.

The **Film, Television, and Live Events** templates provide a starting point for live production work.

| Template Name | Template Contents | Additional Documentation |
| --- | --- | --- |
| **Virtual Production** | Functionality for VR Scouting, Virtual Camera, SDI Video, Composure, and nDisplay. | 
-   [Virtual Scouting Overview](/documentation/en-us/unreal-engine/virtual-scouting-in-unreal-engine)
    
-   [Controlling Virtual Camera Actors](/documentation/en-us/unreal-engine/controlling-a-virtual-camera-actor-using-live-link-in-unreal-engine)
    



 |
| **DMX** | Examples for addressing, patching, and controlling proxy lighting fixtures, as well as recording and playback of live DMX data streams in and outside Unreal Engine. | [DMX](/documentation/en-us/unreal-engine/dmx-in-unreal-engine) |
| **InCamera VFX** | Blueprints, plugins, and example stages for in-camera VFX workflows. Use this as a starting point for Virtual Production shoots with LED volumes. | 

-   [In-Camera VFX Template](/documentation/en-us/unreal-engine/in-camera-vfx-template-in-unreal-engine)
    
-   [In-Camera VFX Overview](/documentation/en-us/unreal-engine/in-camera-vfx-in-unreal-engine)
    



 |
| **nDisplay** | Display functionality using a cluster of PCs. Use as a starting point for rendering on complex arrangements of physical displays for live performances. | 

-   [nDisplay Template](/documentation/en-us/unreal-engine/ndisplay-template-in-unreal-engine)
    
-   [Rendering to Multiple Displays with nDisplay](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine)
    



 |

### Architecture, Engineering, and Construction Templates

![Archviz template in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45a48a0f-7879-47a6-8edd-6ef350765379/templates-aec.png)

Archvis template in Unreal Engine 5.

The **Architecture, Engineering, and Construction** templates use Datasmith to import content from various 3D programs into Unreal Engine, where you can further refine that content for desktop and XR applications.

| Template Name | Template Contents | Additional Documentation |
| --- | --- | --- |
| **Archvis** | Example architectural visualisation workflows with sample scenes for sun studies, interior renderings, and non-photorealistic stylized renderings. |   |
| **Design Configurator** | Uses Variant Manager, UMG, and Blueprint functionality to build a project where you can toggle between different object states such as visibility, initiate animation sequences, switch between views, and toggle between different design options. |   |
| **Collab Viewer** | Navigation and interaction for desktop and VR in collaborative sessions. This template contains some archviz-specific starter content and has several additional plugins enabled by default, including OpenXR and LiveLink. | [Collab Viewer Template](/documentation/en-us/unreal-engine/collab-viewer-templates-in-unreal-engine) |
| **Handheld AR** | A starting point for creating AR applications you can deploy to Android or iOS. Includes runtime logic for scanning an environment to gather data for creating interactive planes in the virtual scene, and lighting and scene depth information. | 
-   [Handheld AR Template Quickstart](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine)
    
-   [Handheld AR Template Technical Reference](/documentation/en-us/unreal-engine/handheld-ar-template-technical-reference)
    



 |

### Automotive, Product Design, and Manufacturing Templates

![Photo Studio template in Unreal Engine 5.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e72e14e-5c4d-424d-8ca0-36e619cf8687/templates-apm.png)

Photo Studio template in Unreal Engine 5.

The **Automotive, Product Design, and Manufacturing** templates use Datasmith to import content from various 3D programs into Unreal Engine, where you can further refine that content for desktop and XR applications.

| Template Name | Template Contents | Additional Documentation |
| --- | --- | --- |
| **Photo Studio** | A premade photographic studio environment you can use for cinematics and product presentations. |   |
| **Product Configurator** | Uses Variant Manager, UMG, and Blueprint functionality to build a generic product configurator (that is, a program that lets you swap out different parts to test out new looks for a product, such as different colors for a car). | [Product Configurator](/documentation/en-us/unreal-engine/product-configurator-template-in-unreal-engine) |
| **Collab Viewer** | Navigation and interaction for desktop and VR in collaborative sessions. This template also contains a sample model car that can be explored in VR. | [Collab Viewer Template](/documentation/en-us/unreal-engine/collab-viewer-templates-in-unreal-engine) |
| **Handheld AR** | A starting point for creating AR applications you can deploy to Android or iOS. Includes runtime logic for scanning an environment to gather data for creating interactive planes in the virtual scene, and lighting and scene depth information. | 
-   [Handheld AR Template Quickstart](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine)
    
-   [Handheld AR Template Technical Reference](/documentation/en-us/unreal-engine/handheld-ar-template-technical-reference)
    



 |

### Simulation Templates

![Simulation template in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/740240c2-b568-40b0-82ae-8a948daea485/templates-simulation.png)

Illustrative use of a Simulation template in Unreal Engine 5.

**Simulation** templates offer a broad range of starting points for various enterprise simulation applications. These templates contain the following functionality:

-   Specific settings for outdoor environments.
-   Realistic sky and lighting.
-   Georeferencing tools.

| Template Name | Template Contents | Additional Documentation |
| --- | --- | --- |
| **Simulation Blank** | 
A template that consists of an empty project with the required settings and plugins enabled. This template is suitable as a starting point for most simulation applications and contains the following features:

-   Earth atmosphere
-   Atmospheric lighting
-   Volumetric clouds
-   Geographical coordinates
-   [World Geodetic System (WGS84)](https://en.wikipedia.org/wiki/World_Geodetic_System)



 |   |
| **Handheld AR** | A starting point for creating AR applications you can deploy to Android or iOS. Includes runtime logic for scanning an environment to gather data for creating interactive planes in the virtual scene, and lighting and scene depth information. | 

-   [Handheld AR Template Quickstart](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine)
    
-   [Handheld AR Template Technical Reference](/documentation/en-us/unreal-engine/handheld-ar-template-technical-reference)
    



 |
| **Virtual Reality** | A starting point for all of your virtual reality (VR) projects in Unreal Engine 5. It includes encapsulated logic for teleport locomotion and common input actions, such as grabbing and attaching items to your hand. | 

-   [VR template](/documentation/en-us/unreal-engine/vr-template-in-unreal-engine)
    
-   [Developing for VR in Unreal Engine](/documentation/en-us/unreal-engine/developing-for-xr-experiences-in-unreal-engine)
    



 |