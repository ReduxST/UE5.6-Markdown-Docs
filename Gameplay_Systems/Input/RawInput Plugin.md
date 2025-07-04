# RawInput Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rawinput-plugin-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rawinput-plugin-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:41

---

The **\*RawInput** plugin provides support for specific, user-defined devices that aren't properly handled by Microsoft's XInput API (Application Programming Interface), usually flight sticks and steering wheels. The buttons and axes of these input devices can be custom-mapped to gameplay inputs, including new inputs created by the plugin itself.

## Enabling RawInput

By default, the plugin is not enabled. It can be enabled from the **Plugins** menu, in the **Input Devices** section.

![RawInput plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07682803-bf28-4571-9041-2294ab6870a2/rawinputplugin.png)

After the plugin is enabled, the **Raw Input** section will appear in the **Project Settings** menu.

![RawInput location in Project Settings menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/755f298a-60ab-48ef-a6cf-025d55eec4ba/rawinput.png)

## Configuring Devices

Within this section, you can add new devices. Each device is identified by a vendor ID and a product ID, which are hexadecimal values that can be found in the device's driver properties. An array of axes (by default, eight) and buttons (by default, twelve) will be added to the controller's configuration. This provides the ability to map any of the controller's axes or buttons (indicated by the array index) to any **Unreal Engine** axis or key. The plugin provides eight new axes ("Generic USB Controller Axis 1" through "Generic USB Controller Axis 8") and twenty new buttons ("Generic USB Controller Button 1" through "Generic USB Controller Button 20"). Each axis and button can be enabled or disabled, and axes can also be inverted and offset.

![Windows Device Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/013b9081-8307-47d6-abf5-98db5cf16da7/windowssettings.png)

Above, you can see the Hardware ID information in Windows Control Panel (under Device Manager) for the Logitech G920. The Vendor ID is the four-character string following "VID\_" test (046D), and the Product ID is the four-character string following "PID\_" (C262). This information will be required when configuring the device in RawInput.

## Example (Vehicle Templates)

As an example, the Vehicle templates that ship with the **Unreal Engine** have been configured to work with the **Logitech G920**, a driving-game controller with a steering wheel and gas/brake pedals.

### Configuring the Device in RawInput

The steering wheel is reported by the driver as Axis 1, the brake is reported as Axis 3, and the gas pedal is reported as Axis 4. In the RawInput plugin settings, each input must be entered into the array at the corresponding axis from the device driver. That is, the steering wheel's data must be in array element 1, the brake's data must be in array element 3, and the gas pedal's data must be in array element 4. All other entries may be removed or marked as disabled.

Note that the array index of an input does not need to correspond to the "Generic USB Controller Axis" or "Generic USB Controller Input" value. For example, the brake is bound to "Generic USB Controller Axis 2" even though it is in array position 3. This is necessary to ensure that different controllers can be configured to work the same way, even if they use different input axes. ![RawInput settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3125f1f1-e260-4efc-8b83-368a9e649da5/rawinputdata.png)

Because the device's output range doesn't match what we might expect from a standard controller, we will remap the input ranges. The wheel returns values from 0.0 (left) to 1.0 (right), but we want the input range to center on 0.0, so we will give it an offset of -0.5. The brake and gas pedals also return values from 0.0 to 1.0, but the device uses 0.0 to indicate that the pedal is pressed down, and 1.0 to indicate that the pedal is up, where our project expects the reverse. To make this adjustment, we set the axis values to be inverted, and then add a 1.0 offset.

### Mapping our RawInput Axes to Input Bindings

![Input settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14fb995a-7ead-409a-bf98-d2045a5c1c27/inputdata.png)

We can then map the new axes to our game's input bindings. The wheel (on "Generic USB Controller Axis 1") is mapped to the range \[-0.5, 0.5\], but we want it to be more sensitive, so we can scale it up by a factor of 3.0. Similarly, the brake (on "Generic USB Controller Axis 2") needs to go in the negative direction, and should be more powerful than the gas pedal, so it will be scaled by -2.0. The gas pedal (on "Generic USB Controller Axis 3") requires no modification, and only needs to be added to the appropriate input binding. By using RawInput and adding these input bindings, we are able to support the Logitech G920 without needing any new input bindings or making any changes to our project's code or Blueprints.

This use of scaling provides a good argument for using the "Generic USB Controller" axes instead of configuring the device to the standard gamepad stick inputs.