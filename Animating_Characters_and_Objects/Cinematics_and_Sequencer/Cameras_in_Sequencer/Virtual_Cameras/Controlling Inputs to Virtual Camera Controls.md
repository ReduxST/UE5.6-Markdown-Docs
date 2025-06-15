# Controlling Inputs to Virtual Camera Controls

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/controlling-inputs-to-virtual-camera-controls-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/controlling-inputs-to-virtual-camera-controls-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:57

---

The [Enhanced Input](/documentation/en-us/unreal-engine/enhanced-input-in-unreal-engine) features of Unreal Engine is capable of managing a large number of actions and changing them dynamically. Inputs can change behavior depending on their current state. This means that you can assign more mappable keys than there are buttons for in the user interface. In this case, it's ideal for mapping inputs of hardware devices to virtual camera controls in Unreal Engine through the [Live Link VCAM](https://apps.apple.com/us/app/live-link-vcam/id1547309663) app.

This page covers how to:

-   [Map hardware inputs to virtual camera actions.](/documentation/en-us/unreal-engine/controlling-inputs-to-virtual-camera-controls-in-unreal-engine#mappinghardwareinputstovirtualcameraactions)
-   [Create an Input Profile for customized workflows and device actions.](/documentation/en-us/unreal-engine/controlling-inputs-to-virtual-camera-controls-in-unreal-engine#creatinganinputprofile)
-   [Set an Input Profile for all Virtual Camera Actors and for individual ones.](/documentation/en-us/unreal-engine/controlling-inputs-to-virtual-camera-controls-in-unreal-engine#settinganinputprofile)
-   [Specify type of input for a Virtual Camera Actor.](/documentation/en-us/unreal-engine/controlling-inputs-to-virtual-camera-controls-in-unreal-engine#specifyingtypeofinputfromadevice)

## Mapping Hardware Inputs to Virtual Camera Actions

You can set input mappings in two ways: globally through the Project Settings, or on individual Virtual Camera Actors. You can edit, add, and configure them from either of these locations.

Change default inputs from:

-   **Project Settings** under **Game > VCam Input Settings**
-   Select a Virtual Camera Actor and in the **Details** panel look under the **Virtual Camera** section and expand the **Input Profile** section.

### Adding an Input

To add a hardware input to a virtual camera action:

![Adding an Input to a Input Profile.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bce69dc-62f5-47fe-89ec-4319d4a59a8a/vcam-adding-an-input.png)

1.  Select a **Virtual Camera** Actor in your scene.
2.  In the **Details** panel under **Virtual Camera**, expand the **Input Profile** section.
3.  Expand **Mappable Key Overrides** and look for a desired input action to change.
4.  Next to the named input, you can do one of the following:
    1.  Click the **Keyboard** icon and then press the key / button you want to handle the input..
    2.  Use the dropdown and search for the key / button / action you want to handle the input.

When choosing an input to map, the desired button is listed as long as it provides the correct type of input to handle that action. For example, the input "NextLens" requires a bool (button) input and cannot be mapped to a float (joystick).

### Creating an Input Profile

To create an **Input Profile**:

1.  Open the **Project Settings** and navigate to **Game > VCam Input Settings**.
2.  **Add** (+) an element to the **Input Profiles** array and give it a **Name**.
    
    ![Add a new Input Profile and give it a name.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aa5aa81-a4fb-4349-869d-5443f798f64b/vcam-inputs-profile-add-and-name.png)
3.  **Add** (+) elements to the **Mappable Overrides** array.
    
    ![Add mappable key overrides to your Input Profile.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce9bd45f-7c37-428e-8119-99a06afc1500/vcam-add-mappable-key-overrides.png)
    
    Each element that you add must be named before another can be added. If you intend to use the mappings of the Default VCam Actor profile as a starting point, you can right-click on the list, choose **Copy** and then **Paste** it onto your custom input profile.
    
4.  Expand **Mappable Key Overrides**. Add new inputs or look for one to edit if you copied the ones from the default Input Profile.
    
    ![Add mappable key override elements to the list Input Profile list.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1868f82-de34-40b5-bfc2-b7a0f1a489a0/vcam-add-and-edit-mappable-key-overrides.png)
5.  Next to the named input, you can do one of the following:
    1.  Click the **Keyboard** icon and then press the key / button you want to handle the input.
    2.  Use the dropdown and search for the key / button / action you want to handle the input.
6.  Repeat **Step 5** for each input you wish to change.

Your list may look similar to the one below, whether you added entries manually or copied and pasted from the default profile to build your own Input Profile.

![A list of mappable key overrides for the created Input Profile.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01ffb024-8d54-49cf-a5d2-7e5ddf266fb9/vcam-input-profile-mappable-keys-completed.png)

### Setting an Input Profile

Input Profiles can be set in one of two ways: globally for all virtual cameras through the Project Settings, or on individual Virtual Camera Actors in the scene.

To setting an input profile in the Project Settings:

1.  Open the **Project Settings** and navigate to **Game > VCam Input Settings**.
2.  In the **Input** section next to **Default Input Profile**, choose the global default you want to use from the dropdown list.

![Setting the default input profile from the Project Settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce5b23dd-fa20-4443-b3e8-4fbd90288a04/vcam-setting-default-input-profile-project-settings.png)

To set an Input Profile for individual Virtual Camera Actors:

1.  Select a **Virtual Camera** actor in the scene.
2.  In the **Details** panel under **Virtual Camera**, use the dropdown list next to **Input Profile** to select the profile you want to use.

![Setting the default input profile for a single virtual camera actor.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eacc0a6d-9ace-42be-87de-a2339dc2f3bf/vcam-default-input-profile-vcam-actor.png)

## Specifying Type of Input from a Device

For set ups using multiple Virtual Camera Actors, you can assign specific input devices to each virtual camera in the scene. This is useful when you have multiple virtual cameras being controlled from a single workstation and is most useful when using gamepads.

Each input device has an ID that starts at 0 and increases by 1 as more devices are connected. The registered ID is recycled when a device disconnects, and is then available for reassignment to the next device that connects. When a device is connected, the lowest possible ID is reassigned. For example, if you have a workstation with two gamepads connected: Gamepad A and Gamepad B. Gamepad A would receive ID 0, and Gamepad B would receive ID 1. If Gamepad A is disconnected, Gamepad B would maintain its registered ID 1. When another gamepad is plugged in and registered, that gamepad would be given the lowest available ID — in this case, that would be ID 0 that was unregistered when Gamepad A was disconnected.

To specify input for a virtual camera:

1.  Select a **Virtual Camera** Actor in your scene.
2.  In the **Details** panel under **Virtual Camera**, expand the **Input Device Settings**.
3.  Remove the checkmark from **Allow All Input Devices**. A new property called **Allow Input Device Ids** will appear.
    
    Click image for full size.
    
4.  Click the **Add (+)** icon to add a device to the array.
    
    ![Add a new Input Device element to the device array.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e2fba60-05fb-4797-980b-54d08cb08409/vcam-add-new-input-device.png)
5.  Connect a physical gamepad to your workstation, if one is not already.
6.  Click the **Gamepad** icon. Then, press any button on your physical gamepad to register its ID.

This Virtual Camera Actor now responds to inputs from the registered gamepad and any other input devices in the list.

### Using Keyboards and Mice with an Input Device

-   Keyboards and mice cannot be assigned to specific Virtual Camera Actors. Workflows involving multiple keyboards and mice are not supported.
-   Keyboards always have a device ID equal to 0. The first connected gamepad will also use ID 0.
-   Mice always have a device ID equal to -1.