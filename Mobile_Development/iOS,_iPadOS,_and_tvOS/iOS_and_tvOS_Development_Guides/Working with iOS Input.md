# Working with iOS Input

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-ios-input-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-ios-input-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:44

---

In iOS, tvOS, and iPadOS 14 and later, Apple supports a wide variety of input devices, including gamepads, keyboard, mouse, and trackpad. This includes the ability to remap gamepad buttons for Xbox, PlayStation, and MFi gamepad controllers at the OS-level. The OS provides handling for the button glyph displays for these devices, enabling applications to obtain glyphs that are accurate to users' custom mappings. This is required for all apps targeting OS version 14 and later.

Apple requires that your in-game button displays must be accurate to the user's OS-level input bindings. The App Store and Apple Arcade may reject your Apps for distribution if you do not comply with this requirement.

**Unreal Engine** supports input handling, enabling your applications to take full advantage of the expanded range of devices. As long as users correctly connect their input to their Apple device, no additional setup is required to use this functionality. However, functionality is included to assist in complying with Apple's requirements for the UI.

## Obtaining Gamepad Button Glyphs

Use the **Get Gamepad Button Glyph** node in **Blueprint** to retrieve glyphs accurate to your users' mappings.

![The Get Gamepad Button Glyph node in Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01ef4c19-b78c-4d65-b740-dddd4c9fc028/getbuttonglyphbp.png)

The Get Button Glyph node, with the text Gamepad\_Facebutton\_Top provided in the Button Key field.

Its parameters are as follows:

| Parameter | Type | Description |
| --- | --- | --- |
| Button Key | String | The `FKey` name for the intended button, as defined in `InputCoreTypes.h`, converted to a string. |
| Controller Index | Integer | The index of the connected controller that you want to fetch button glyphs for. |
| Return Value | Texture2D | A 2D texture containing the button glyph to use in your UI widgets. |

As an example, if you wanted to obtain the button glyph for the top face button on a controller, you would use the string **Gamepad\_Facebutton\_Top**.

When requesting buttons like this, you should request the button that you expect the user to use based on the default mapping. If the user has remapped the buttons within the OS, the function will automatically return the re-mapped button they're using instead. For instance, if the user swaps the X and Y buttons on an Xbox controller, `Gamepad_Facebutton_Top` would return the X button glyph instead of Y.