# Customizing Keyboard Shortcuts

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-keyboard-shortcuts-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-keyboard-shortcuts-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:18

---

**Keyboard shortcuts**, also known as **keybinds**, are combinations of key presses on your keyboard that execute specific commands or actions. You can configure the shortcuts for common commands, as well as some tool-specific commands, to suit your workflow and personal preferences. To do this, open the **Editor Preferences** window: from the main menu, go to **Edit > Editor Preferences**, then select the **Keyboard Shortcuts** section.

![Keyboard Shortcuts editor in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bca09de-b9b1-47e7-b421-8c5bc8ffb618/keyboard-shortcuts.png)

The Keyboard Shortcuts editor in the Editor Preferences window.

Commands are grouped by functional area. Each command can have up to two keyboard shortcuts associated with it.

## Creating a New Keyboard Shortcut

1.  Click inside the **text field** for the command you want to bind to a keyboard shortcut.
    
2.  Press the combination of keys you want to use to execute the command.
    
    ![Adding a new keyboard shortcut](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e84dd0d-e65a-41a7-bc07-cbd6a2a62fc4/adding-new-shortcut.png)

Unreal Engine will automatically save the new shortcut when you click anywhere outside the text field.

If the combination of keys you pressed is already bound to another command, you will see a warning.

![Keyboard shortcut already exists](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b01163a3-5c70-4fcb-95ac-337bce722d25/shortcut-already-exists.png)

If you want to remove the existing binding and assign the keyboard shortcut to the new command, click the **Override** button. If you want to keep the existing binding and cancel the new one, click anywhere outside the text field.

## Removing an Existing Keyboard Shortcut

To remove an existing keyboard shortcut, click the **Delete** (**X**) button next to it.

![Removing a keyboard shortcut](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b8d0db5-0c77-4c77-8adb-3dc5585c6087/removing-a-shortcut.png)

## Importing and Exporting Keyboard Shortcuts

You can migrate your custom keybinds between different installations of Unreal Engine by exporting them as an `.ini` file that you can then import into another UE installation. This is useful, for example, if you work on different computers, or if you rebuild or reinstall Unreal Engine often.

To save your custom keybinds as an `.ini` file, click the **Export** button. To import a set of custom keybinds from an `.ini` file, click the **Import** button. Both of these buttons are located at the top of the **Keyboard Shortcuts** editor.

![Export and Import buttons in the Keyboard Shortcuts editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/483b8eee-6e74-4964-ae64-e977e90e2928/export-import-buttons.png)

Location of the Export and Import buttons.