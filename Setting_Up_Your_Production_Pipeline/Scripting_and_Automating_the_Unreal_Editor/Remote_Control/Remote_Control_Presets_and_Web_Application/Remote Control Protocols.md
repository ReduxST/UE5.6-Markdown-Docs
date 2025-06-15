# Remote Control Protocols

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-protocols-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-protocols-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:36

---

With Remote Control Protocols you can bind protocol input data to exposed properties, to control them using external devices. This page describes how to use the Remote Control plugins for the DMX, MIDI, and OSC plugins, and how to create your own Protocol plugin.

## Prerequisites

1.  Enable the **Remote Control API** plugin.
    
2.  Enable the Remote Control plugin specific to the protocol you're using:
    
    1.  For DMX, enable the **Remote Control Protocol DMX** plugin.
        
    2.  For MIDI, enable the **Remote Control Protocol MIDI** plugin.
        
    3.  For OSC, enable the **Remote Control Protocol OSC** plugin.
        
3.  Restart the editor.
    

Once you enable these plugins, create a **Remote Control Preset Asset** and expose properties to the Preset. Refer to [Getting Started with Remote Control Presets](/documentation/en-us/unreal-engine/getting-started-with-remote-control-presets-in-unreal-engine) for more details.

## Mapping Protocols in Remote Control

Follow these steps to be able to control properties from your external device.

1.  In the Remote Control Panel, select the property you want to map to a Protocol.
    
    ![Select a property to map to a protocol](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e5cbae3-877e-41d1-8797-cc3167ca9151/01-sl-pr.png)
2.  Select the Protocol from the dropdown list and press the plus button next to it to add a new mapping.
    
    ![Select a protocol mapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8f9e9a6-0148-47fd-a1a3-2ef4ab6edc88/02-pr-m.png)
3.  Modify the settings in the mapping section to connect to your external device. Refer to the [Remote Control Panel Reference](/documentation/en-us/unreal-engine/remote-control-panel-reference-for-unreal-engine) for more details on the fields.
    
    You can quickly autobind an input by using the autobinding button located in the top right of the mapping panel. Refer to the [Remote Control Panel Reference](/documentation/en-us/unreal-engine/remote-control-panel-reference-for-unreal-engine) for more details.
    
4.  In the **Ranges** section, add more range steps by selecting the plus button on the right. Enter different values in the range points to make the property interpolate between them when controlling from the external device.
    
    Press the left-facing arrow next to a range value to capture its current value in the world.
    
5.  Verify your mapping and inputs are set up correctly by using your external device and seeing the changes in the object's **Details** panel or the viewport.
    

## Adding a New Protocol

To add your own protocol support to Remote Control, you need to implement `IRemoteControlProtocol` and `FRemoteControlProtocolEntity`.

Follow these steps to add your own implementation for a Remote Control Protocol.

1.  Create a new blank plugin. See [Creating a New Plugin](/documentation/en-us/unreal-engine/plugins-in-unreal-engine#creatingnewplugins) for instructions.
    
    The recommended naming convention is **RemoteControlProtocol{Name}**, where **{Name}** is the name of your protocol. For example the MIDI implementation is called `RemoteControlProtocolMIDI`.
    
2.  Within the created \*.uplugin file, add a dependency to the RemoteControl plugin:
    
    ```
             `"Plugins": [              {                  "Name": "RemoteControl",                  "Enabled": true              }          ]`
    		
    Copy full snippet
    ```
    "Plugins": \[ { "Name": "RemoteControl", "Enabled": true } \]
3.  In Visual Studio's Solution Explorer for your project, find the module, defined in a `.Build.cs` file. Append `RemoteControl` and `RemoteControlProtocol` to the `PrivateDependencyModuleNames` range.
    
4.  Create a new class that implements `IRemoteControlProtocol`, or inherit from the base implementation `FRemoteControlProtocol`, with overrides for:
    
    1.  **GetProtocolScriptStruct()**: Provide the class of your **Protocol Entity** implementation. For the example with MIDI, it's `FRemoteControlProtocolMIDIEntity::StaticStruct()`.
        
    2.  **Bind(Entity)**: This is typically used to register the entity with a local collection to iterate over whenever input is received. The provided entity will be specific to your implementation which is described below.
        
    3.  **Unbind(Entity):** Similar to Bind, this is typically used to remove the provided entity from a collection.
        
    4.  **UnbindAll():** Removes all entities from the collection.
        
5.  Create a new struct that represents the protocol binding for a given entity (the exposed property) by inheriting from the FRemoteControlProtocolEntity struct, with overrides for:
    
    1.  **GetRangePropertyName():** For example `FFloatProperty` if the input from the device is a float.
        
    2.  A transient, non-visible, and non-editable UPROPERTY() called RangeInputTemplate: You can specify additional constraints such as min and max values. This is used to create the appropriate editor widget. You can optionally store the property elsewhere and specify it by overriding `IRemoteControlProtocol::GetRangeTemplateType()`.
        
6.  Register your `IRemoteControlProtocol` implementation with:
    
    ```
             `IRemoteControlProtocolModule::Get().AddProtocol({Name}, MakeShared<{Implementation}>());`
    Copy full snippet
    ```
    IRemoteControlProtocolModule::Get().AddProtocol({Name}, MakeShared<{Implementation}>());

For further examples, including how to create and register project settings, see the implementations for DMX, MIDI, and OSC Remote Control Protocol Plugins in the UE source code.