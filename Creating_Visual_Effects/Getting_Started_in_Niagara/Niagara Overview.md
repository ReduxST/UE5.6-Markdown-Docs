# Niagara Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine)  
**Processed:** 2025-06-14 16:41:00

---

Niagara is Unreal Engine's next-generation VFX system. With Niagara, the technical artist has the ability to create additional functionality on their own, without the assistance of a programmer. The system is adaptable and flexible. Beginners can start out by modifying templates or behavior examples, and advanced users can create their own custom modules.

## Core Niagara Components

In the Niagara VFX system, there are four core components:

-   Systems
    
-   Emitters
    
-   Modules
    
-   Parameters
    

### Systems

A Niagara system is a container for everything you will need to build that effect. Inside that system, you may have different building blocks that stack up to help you produce the overall effect.

You can modify some system-level behaviors that will then apply to everything in that effect.

[![Niagara System Settings](https://dev.epicgames.com/community/api/documentation/image/2a6c4270-64ac-4889-9435-513db28acc29?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2a6c4270-64ac-4889-9435-513db28acc29?resizing_type=fit)

The **Timeline** panel in the System Editor shows which emitters are contained in the system, and can be used to manage those emitters.

### Emitters

Emitters are where particles are generated in a Niagara system. An emitter controls how particles are born, what happens to that particles as they age, and how the particles look and behave.

The emitter is organized in a stack. Inside that stack is several groups, inside which you can put modules that accomplish individual tasks. The groups are as follows.

[![Emitter Groups](https://dev.epicgames.com/community/api/documentation/image/f33d847b-8d5b-4bee-88c3-2648d55da32f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f33d847b-8d5b-4bee-88c3-2648d55da32f?resizing_type=fit)

1.  **Emitter Spawn**
    
    This group defines what happns when an emitter is first created on the CPU. Use this group to define initial setups and defaults.
    
2.  **Emitter Update**
    
    This group defines emitter-level modules that occur every frame on the CPU. Use this group to define spawning of particles when you want them to continue spawning on every frame.
    
3.  **Particle Spawn**
    
    This group is called once per particle, when that particle is first born. This is where you will want to define the initialization details of the particles, such as the location where they are born, what color they are, their size, and more.
    
4.  **Particle Update**
    
    This group is called per particle on each frame. You will want to define here anything that needs to change frame-by-frame as the particles age. For example, if the color of the particles is changing over time. Or, if the particles are affected by forces like gravity, curl noise, or point attraction. You may even want the particles to change size over time.
    
5.  **Event Handler**
    
    In the Event Handler group, you can create Generate events in one or more emitters that define certain data. Then you can create Listening events in other emitters which trigger a behavior in reaction to that generated event.
    
6.  **Render**
    
    The last group is the Render group. This is where you define the display of the particle and set up one or more renderers for your particles. You may want to use a Mesh renderer if you want to define a 3D model as the basis of your particles, upon which you could apply a material. Or, you may want to use a sprite renderer and define your particles as 2D sprites. There are many different renderers to choose from and experiment with.
    

### Modules

Modules are the basic building blocks of effects in Niagara. You add modules to groups to make a stack. Modules are processed sequentially from top to bottom.

[![Emitter Modules](https://dev.epicgames.com/community/api/documentation/image/70d7b895-67ba-4ead-867a-e013c23b363e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/70d7b895-67ba-4ead-867a-e013c23b363e?resizing_type=fit)

You can think of a module as a container for doing some math. You pass some data into the module, then inside the module you do some math on that data, and then you write that data back out at the end of the module.

Modules are built using High-Level Shading Language (HLSL), but can be built visually in a Graph using nodes. You can create functions, include inputs, or write to a value or parameter map. You can even write HLSL code inline, using the **CustomHLSL** node in the Graph.

You can double-click any module from an emitter in Niagara to take a look at the math that's happening inside. You can even copy and create your own modules. For example, if you double-click on the Add Velocity module to take a look inside, you can inspect the data flow.

[![Add Velocity Module](https://dev.epicgames.com/community/api/documentation/image/06cc8496-4b5d-44ff-972c-e61b5a200438?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/06cc8496-4b5d-44ff-972c-e61b5a200438?resizing_type=fit)

Click image for full size.

The script starts by retrieving inputs - the velocity input and the coordinate space. It then gets the current velocity of the particles, as well as an inputted scaling factor. Then, the input velocity is scaled, transformed in the correct coordinate space, and added to the current velocity of the particles. Once that work is complete, the new particle velocity is written back out so that any modules that need velocity information further on down the stack can retrieve it.

All modules are built with that basic methodology, though for some the internal math may be more complex.

### Parameters and Parameter Types

*Parameters* are an abstraction of data in a Niagara simulation. Parameter *types* are assigned to a parameter to define the data that parameter represents. There are four types of parameters:

-   **Primitive**: This type of parameter defines numeric data of varying precision and channel widths.
    
-   **Enum**: This type of parameter defines a fixed set of named values, and assumes one of the named values.
    
-   **Struct**: This type of parameter defines a combined set of Primitive and Enum types.
    
-   **Data Interfaces**: This type of parameter defines functions that provide data from external data sources. This can be data from other parts of UE4, or data from an outside application.
    

[![Parameters](https://dev.epicgames.com/community/api/documentation/image/187b1349-c1af-46cd-b12b-ac95b124d8c1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/187b1349-c1af-46cd-b12b-ac95b124d8c1?resizing_type=fit)

You can add a custom parameter module to an emitter by clicking the **Plus sign** icon (**+**) and selecting **Set new or existing parameter directly**. This adds a **Set Parameter** module to the stack. Click the **Plus sign** icon (**+**) on the **Set Parameter** module and select **Add Parameter** to set an existing parameter, or **Create New Parameter** to set a new parameter.

## Templates and Behavior Examples

### Niagara Asset Browser Window

When you first create a Niagara emitter or Niagara system, an **asset browser** window displays the available Niagara systems and emitters in your project. You can filter the available assets by type or by categories. You can also create custom categories for filtering purposes.

To create a new Niagara system, right-click in the **Content Browser** and click **FX > Niagara System**.

[![right-click in the Content Browser and click FX - Niagara System](https://dev.epicgames.com/community/api/documentation/image/4952919e-a06a-48f9-b482-57a91dcf4a2d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4952919e-a06a-48f9-b482-57a91dcf4a2d?resizing_type=fit)

The **Niagara Asset Browser** window will open and display all available systems in the project. The window consists of the following sections:

[![The window consists of the following sections](https://dev.epicgames.com/community/api/documentation/image/913a7b62-0082-4acf-88a7-7508686e0a86?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/913a7b62-0082-4acf-88a7-7508686e0a86?resizing_type=fit)

Click image for full size.

#### 1\. Content Area

The **content area** displays the systems and emitters available based on the selected category and filters.

#### 2\. Categories

The **categories** section displays all available categories in the project. Select any of the categories to see the systems and emitters available.

[![Select any of the categories to see the systems and emitters available](https://dev.epicgames.com/community/api/documentation/image/f53e28d1-8d87-48da-9e3e-75f77e8e429b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f53e28d1-8d87-48da-9e3e-75f77e8e429b?resizing_type=fit)

#### 3\. Toolbar

The toolbar has the following options available:

##### Filter

[![The filter button displays a dropdown with the available FX and Niagara filters](https://dev.epicgames.com/community/api/documentation/image/0cf54fd8-a5dd-4b4f-9423-93053b50811d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0cf54fd8-a5dd-4b4f-9423-93053b50811d?resizing_type=fit)

The **filter** button displays a dropdown with the available FX and Niagara filters. Select the Niagara Emitter filter to display the available emitters in the content area.

[![Click the Filter button and enable the Niagara Emitter filter](https://dev.epicgames.com/community/api/documentation/image/2e1d7a36-07e0-4e25-bb83-1e4bb9dfe2f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2e1d7a36-07e0-4e25-bb83-1e4bb9dfe2f7?resizing_type=fit)

You can click on the filter button to enable and disable the filter.

![Niagara emitter filter active](https://dev.epicgames.com/community/api/documentation/image/7822d3aa-465c-4f3d-a787-84449906c22f?resizing_type=fit&width=1920&height=1080)

![Niagara emitter filter inactive](https://dev.epicgames.com/community/api/documentation/image/d888dca9-52d2-48a0-9119-89509e2f6294?resizing_type=fit&width=1920&height=1080)

Niagara emitter filter active

Niagara emitter filter inactive

##### Search

[![The search bar is used to search for systems and emitters by name](https://dev.epicgames.com/community/api/documentation/image/8672e8a9-5d66-4c3e-a36e-cc94e48e1e77?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8672e8a9-5d66-4c3e-a36e-cc94e48e1e77?resizing_type=fit)

The **search bar** is used to search for systems and emitters by name. In the example below we searched for **fire** to see all the systems that contain that word in their name.

[![In this example, we searched for fire to see all the systems that contain that word in their name](https://dev.epicgames.com/community/api/documentation/image/3b2bcf8c-9566-4058-ae91-e7ece6add951?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3b2bcf8c-9566-4058-ae91-e7ece6add951?resizing_type=fit)

If the systems above are not available in your project, go to the **Plugins** window and enable the **Niagara Fluids** plugin.

#### 4\. Details

The **details** section displays information about the selected system or emitter.

[![In this example an emitter is selected and you can see the asset’s details](https://dev.epicgames.com/community/api/documentation/image/1e8d17a3-46ac-43e7-9e84-1e4fbc49d3ed?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1e8d17a3-46ac-43e7-9e84-1e4fbc49d3ed?resizing_type=fit)

In the above example an **emitter** is selected and you can see the asset’s **description**, **primary tags** (category), whether the emitter is **inherited** from another asset, and whether it **runs on the CPU or GPU**.

#### Add your own categories

The Niagara asset browser uses tags to organize the Niagara systems and emitters inside the window. The tags are visualized as a folder hierarchy on the left-hand side of the window, as shown below.

[![The tags are visualized as a folder hierarchy on the left-hand side of the window](https://dev.epicgames.com/community/api/documentation/image/a1d5a3a2-c209-43af-996d-752f8394d5a7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a1d5a3a2-c209-43af-996d-752f8394d5a7?resizing_type=fit)

Each asset has a corresponding **Primary Tag** which is used to place it in the correct category. In the example below, the system **Grid2D\_Gas\_Color** has the Primary Tag **2D Gas**, which corresponds to the **2D Gas category** on the left-hand side.

[![In this example, the system Grid2D_Gas_Color has the Primary Tag 2D Gas, which corresponds to the 2D Gas category](https://dev.epicgames.com/community/api/documentation/image/a0815b45-b9ed-4f60-9045-15b98b3dbd15?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a0815b45-b9ed-4f60-9045-15b98b3dbd15?resizing_type=fit)

You can create your own tags and assign them to your assets inside the Content Browser. This, in turn, creates custom categories in the Asset Browser.

For this example, we created three Niagara emitters named **NE\_Hit\_Concrete**, **NE\_Hit\_Glass**, and **NE\_Hit\_Wood** to represent different hit effects.

[![We created three Niagara emitters named NE_Hit_Concrete, NE_Hit_Glass, and NE_Hit_Wood](https://dev.epicgames.com/community/api/documentation/image/9b77c67f-e953-4a44-8938-6381b90f13e6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b77c67f-e953-4a44-8938-6381b90f13e6?resizing_type=fit)

To create custom tags follow these steps:

1.  Right click in the **Content Browser** and click **FX > Advanced > Niagara Asset Tag Definitions**. Name the asset **NAD\_HitEffects**.
    
    [![Right click in the Content Browser and click FX - Advanced - Niagara Asset Tag Definitions](https://dev.epicgames.com/community/api/documentation/image/832929a1-6ae6-497d-b2cc-2cda49d90d9d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/832929a1-6ae6-497d-b2cc-2cda49d90d9d?resizing_type=fit)
    
2.  Double click **NAD\_HitEffects** to open it. Enter a **Display Name** and **Description**. This will be used in the categories view inside the Asset Browser.
    
    [![Open NAD_HitEffects and enter a Display Name and Description](https://dev.epicgames.com/community/api/documentation/image/632fa8a9-8d11-48cf-bcc7-852bd9a6bad5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/632fa8a9-8d11-48cf-bcc7-852bd9a6bad5?resizing_type=fit)
    
3.  Click the **\+ sign** next to **Tag Definitions** to add a new tag. Expand Index \[0\] and enter **Hit\_Glass** as the **Asset Tag** and select **Emitters** as the **Asset Flags**.
    
    [![Click the + sign and enter Hit_Glass as the Asset Tag and select Emitters as the Asset Flags](https://dev.epicgames.com/community/api/documentation/image/2d97c3b4-838a-45d7-984c-1d51cb96c562?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2d97c3b4-838a-45d7-984c-1d51cb96c562?resizing_type=fit)
    
4.  Follow the previous step and add two additional tags: **Hit\_Concrete** and **Hit\_Wood**.
    
    [![Add the Hit_Concrete and Hit_Wood tags](https://dev.epicgames.com/community/api/documentation/image/9a9ce26c-da15-484f-b3a0-7a279862bfe2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a9ce26c-da15-484f-b3a0-7a279862bfe2?resizing_type=fit)
    
5.  Right-click **NE\_Hit\_Concrete** and click **Manage Tags > Hit\_Concrete**. This will add the Hit\_Concrete tag to the asset.
    
    [![Right-click NE_Hit_Concrete and click Manage Tags > Hit_Concrete](https://dev.epicgames.com/community/api/documentation/image/107df5a2-4469-4cd3-929c-9108e6219210?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/107df5a2-4469-4cd3-929c-9108e6219210?resizing_type=fit)
    
6.  Add the **Hit\_Glass** and **Hit\_Wood** tags to the **NE\_Hit\_Glass** and **NE\_Hit\_Wood** emitters, respectively.
    
7.  Right-click in the **Content Browser** and click **FX > Niagara System** to open the **Asset Browser**. Click the **Hit Effects** category to see the emitters with tags that are part of that Asset Tag Definition.
    
    [![Open the Asset Browser and click the Hit Effects category to see the emitters with tags that are part of that Asset Tag Definition](https://dev.epicgames.com/community/api/documentation/image/5edf1939-5613-4c1e-8df4-6ededf67a0de?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5edf1939-5613-4c1e-8df4-6ededf67a0de?resizing_type=fit)
    
8.  Now click the **Hit\_Glass** category to see the emitter with the Hit Glass tag.
    
    [![Click the Hit_Glass category to see the emitter with the Hit Glass tag](https://dev.epicgames.com/community/api/documentation/image/04396b20-f865-474c-90d5-703fd9f7856d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/04396b20-f865-474c-90d5-703fd9f7856d?resizing_type=fit)
    
9.  You can create as many Asset Tag Definitions as you want for your project. In the example below we created another definition with the name **Splash Effects** and two tags: **Splash\_Clear** and **Splash\_Mud**.
    
    [![In the example below we created another definition with the name Splash Effects and the Splash_Clear and Splash_Mud tags](https://dev.epicgames.com/community/api/documentation/image/ff6a145c-dd23-41c3-abec-8cc6752e19d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ff6a145c-dd23-41c3-abec-8cc6752e19d5?resizing_type=fit)
    

## Niagara VFX Workflow

### Create Systems

First create a Niagara System in which you can add one or more emitters. You can then set up the properties of each emitter.

### Create or Add Emitters

In the Niagara Editor, you can adjust your emitter by changing the properties of the modules already in it, or add new modules for the desired effect. You can also copy emitters and add multiple emitters into a single Niagara system. For an example of this, see the Sparks tutorial.

### Create or Add Modules

In your emitter, you can add existing modules from Niagara by clicking on the **Plus (+)** of the group where you want to add the module. Niagara comes with a lot of pre-existing modules, and for the majority of circumstances you will be able to create your effects without needing to do any custom module design.

However, if you want to create your own modules, it can be helpful to understand how the data flows through a module.

[![Data Flow Through a Module](https://dev.epicgames.com/community/api/documentation/image/2504f82c-4f3e-4ff6-b565-b982eab481ec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2504f82c-4f3e-4ff6-b565-b982eab481ec?resizing_type=fit)

Data flow through a module. Click image for full size.

-   Modules accumulate to a temporary namespace, then you can stack more modules together. As long as they contribute to the same attribute, the modules will stack and accumulate properly.
    
-   When writing a module, there are many functions available for you to use:
    
    -   Boolean operators
        
    -   Math expressions
        
    -   Trigonometry expressions
        
    -   Customized functions
        
    -   Nodes that make boilerplate functions easier
        
-   Once you create a module, anyone else can use it.
    
-   Modules all use HLSL. The logic flow is as follows:
    
    [![HLSL Logic Flow](https://dev.epicgames.com/community/api/documentation/image/22535d5f-f196-490b-ae3b-bbeabdd6fed5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/22535d5f-f196-490b-ae3b-bbeabdd6fed5?resizing_type=fit)
    
    HLSL logic flow. Click image for full size.
    

Remember that each module, emitter and system you create uses resources. To conserve resources and improve performance, look through the modules already included in Niagara to see if you can accomplish your goal without creating a new module. [Dynamic Inputs](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine) can be used to great effect here.

## Niagara Paradigms

### Inheritance

-   With a flat hierarchy, you cannot effectively locate and use the assets you already have in your library, which leads to people recreating those assets. Duplication of effort lowers efficiency and increases costs.
    
-   Hierarchical inheritance increases discoverability and enables effective reuse of existing assets.
    
-   Anything inherited can be overridden for a child emitter in a system.
    
-   Modules can be added, or can be reverted back to the parent value.
    
-   This is also true with emitter-level behaviors such as spawning, lifetime, looping, bursts, and so on.
    

### Dynamic Inputs

-   Dynamic inputs are built the same way modules are built.
    
-   Dynamic inputs give users infinite extensibility for inheritance.
    
-   Instead of acting on a parameter map, dynamic inputs act on a value type.
    
-   Any value can be driven by Graph logic and user-facing values.
    
-   Dynamic inputs have almost the same power as creating modules, but can be selected and dropped into the stack without actually creating new modules.
    
-   Existing modules can be modified and customized in many ways by using and chaining Dynamic Inputs; this can reduce module bloat and improve performance.
    

### Micro Expressions

-   Any inline value can be converted into an HLSL expression snippet.
    
-   Users can access any variable in the particle, emitter, or system, as well as any HLSL or VM function.
    
-   This works well for small, one-off features that do not need a new module.
    

### Events

-   Events are a way to communicate between elements (such as particles, emitters, and systems).
    
-   Events can be any kind of data, packed into a payload (such as a struct) and sent. Then anything else can listen for that event and take action.
    
-   Options you can use:
    
    -   Run the event directly on a particle by using Particle.ID.
        
    -   Run the event on every particle in a System.
        
    -   Set particles to spawn in response to the event, then take some action on those particles.
        
-   Events are a special node in the graph (structs). How to use the Event node:
    
    -   Name the event.
        
    -   Add whatever data you want to it.
        
    -   Add an Event Handler into the Emitter stack.
        
    -   Set the options for the Event Handler.
        
-   There is a separate execution stack for events.
    
    -   You can put elaborate graph logic into Event Handlers.
        
    -   You can have a whole particle system set up, with complex logic, and then have a whole separate set of behaviors that occur when the event triggers.
        

### Data Interfaces

-   There is an extensible system to allow access to arbitrary data.
    
-   Arbitrary data includes mesh data, audio, external DDC information, code objects, and text containers.
    
-   Data interfaces can be written as plugins for greater extensibility moving forward.
    
-   Users can get any data associated with a skeletal mesh by using a skeletal mesh data interface.
    

### Houdini

-   Using Houdini, you can calculate split points, spawn locations, impact positions, impact velocity, normals and so on.
    
-   You can then export that data from Houdini to a common container format (CSV).
    
-   You can import that CSV into Niagara in your UE4 project.