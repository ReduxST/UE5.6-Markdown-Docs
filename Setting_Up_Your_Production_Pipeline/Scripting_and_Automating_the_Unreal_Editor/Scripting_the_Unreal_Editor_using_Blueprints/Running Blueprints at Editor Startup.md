# Running Blueprints at Editor Startup

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/running-blueprints-at-unreal-editor-startup](https://dev.epicgames.com/documentation/en-us/unreal-engine/running-blueprints-at-unreal-editor-startup)  
**Processed:** 2025-06-14 16:47:30

---

You can set up the **Unreal Editor** to always run predefined Blueprint graphs every time your Project is opened. This can help you to ensure that the editing environment is set up the way you are expecting, regardless of who opens your Project or what computer they open it on. For example, depending on the needs of your content development pipeline or production standards, you may need to initialize some editing systems that you have created, load or modify content, reimport **Assets** from disk to pick up latest modifications, open custom **Editor Utility Widgets**, or bind to events that may occur during the editing session.

The instructions on this page show how you can register Editor-only Blueprint classes as **startup objects**, so that the Unreal Editor will invoke functions on those objects every time it starts up.

These instructions work with any Editor Utility Blueprint that derives directly or indirectly from **EditorUtilityObject**, and with any Editor Utility Widget.

## Steps

1.  If you don't already have an Editor Utility Blueprint that derives from **EditorUtilityObject**, or an Editor Utility Widget, create one. For example, these instructions create a new Editor Utility Blueprint:
    
    1.  Right-click in the **Content Browser** and choose **Editor Utility > Editor Utility Blueprint**.
        
        ![Create a new Editor Utility Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/181f3b26-21cb-49c0-907c-3a98cf972a69/01_createeubp.png "Create a new Editor Utility Blueprint")
    2.  Choose a parent class. **EditorUtilityObject** is a safe choice, but you could choose any other class that derives from **EditorUtilityObject**. Click **Create**.
        
        ![EditorUtilityObject parent class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ca431ff-e5cb-411c-95f8-9e740793d67f/02_chooseeuobjectclass.png "EditorUtilityObject parent class")
    3.  Enter a descriptive name for your new class, and press **Enter**.
        
        ![Rename the new class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4eb03ffa-5092-410c-a702-cab701fb8146/03_renameeubp_soclass.png "Rename the new class")
2.  Double-click your Blueprint class to open it in the **Blueprint Editor**.
    
3.  Override the **Run** function for the class.
    
    To do this, hover over the **Functions** group in the **My Blueprint** panel until the **Override** button appears. Click the **Override** button and select **Run** from the dropdown list.
    
    ![Override the Run function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d818fb6-69d4-459d-8a81-68ef2104b907/04_overriderun.png "Override the Run function")
    
    The Blueprint Editor creates a new **Event Run** node in the **Event Graph**. Add the Blueprint logic you want to trigger here.
    
    For example, this implementation writes a message to the log to indicate that the function was called, then spawns a cube in the middle of the editor's default startup Level.
    
    ![A simple Run implementation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0c4b054-9808-47e9-a283-e0caf50f9bf2/05_eventrunscript.png "A simple Run implementation")
4.  **Compile** and **Save** your Blueprint class.
    
5.  Shut down the Unreal Editor.
    
6.  Find the `DefaultEditorPerProjectUserSettings.ini` file, which is located in your Project folder at `Project/Config/DefaultEditorPerProjectUserSettings.ini`. If this file does not exist, create it.
    
7.  Open `DefaultEditorPerProjectUserSettings.ini` in a text editor.
    
8.  Find the following section of the file:
    
    ```
            `[/Script/Blutility.EditorUtilitySubsystem]`
    		
    Copy full snippet
    ```
    \[/Script/Blutility.EditorUtilitySubsystem\]
    
    If this section doesn't exist, create it.
    
9.  For each Blueprint class that you want to act as a startup object, add the path to that class as a new value in the `StartupObjects` array. Start the path with `/Game/`, then add the path to the Blueprint class as shown in the **Content Browser**. Follow the object name with a period (`.`) character, then repeat the object name again.
    
    For example, to register the object created under step 1 above, you would use:
    
    ```
        `[/Script/Blutility.EditorUtilitySubsystem]     StartupObjects=/Game/ThirdPerson/CustomBP/MyStartupObject.MyStartupObject`
    
    Copy full snippet
    ```
    \[/Script/Blutility.EditorUtilitySubsystem\] StartupObjects=/Game/ThirdPerson/CustomBP/MyStartupObject.MyStartupObject
    
    If you need to register multiple startup objects, precede each additional line with a plus (`+`) character. For example, a possible configuration with three startup objects might look like this:
    
    ```
        `[/Script/Blutility.EditorUtilitySubsystem]     StartupObjects=/Game/Folder/MyClass.MyClass     +StartupObjects=/Game/AnotherFolder/MyOtherClass.MyOtherClass     +StartupObjects=/Game/AnotherFolder/MyThirdClass.MyThirdClass`
    
    Copy full snippet
    ```
    \[/Script/Blutility.EditorUtilitySubsystem\] StartupObjects=/Game/Folder/MyClass.MyClass +StartupObjects=/Game/AnotherFolder/MyOtherClass.MyOtherClass +StartupObjects=/Game/AnotherFolder/MyThirdClass.MyThirdClass
10.  Save and close the `.ini` file.
    
11.  Restart the Unreal Editor and reload your Project.
    

## End Result

When you reload your Project, the editor Utilities Subsystem automatically creates an instance of each Blueprint class that you identified as a startup object. For each instance, it calls your custom implementation of the **Run** function.

For example, the **Run** function implemented in the preceding steps has two effects:

-   A line printed in the **Output Log**:
    
-   A newly spawned cube in the center of the Level:
    

## Binding to Editor Events

One useful possibility for startup objects is to bind custom events in your Blueprint class to other events that may occur as a user works on your Project content in the Unreal Editor. Because the startup object is guaranteed to be invoked any time the Project content is opened by any user, this can help you to guarantee a consistent editing experience.

For example, this implementation of the **Run** function binds to an event triggered by the **Import Subsystem** any time the editor imports a new Asset. In this case, it prints the name of the Asset to the screen and the log. You could also use the information returned about the new Asset to carry out additional steps, like validating that the name or folder location of the new Asset matches the naming conventions and content conventions that you use in your Project. Putting this kind of check in a startup object helps guarantee that the same validation steps happen for all users that contribute content to your Project.

Drag left from the **Event** input on the **Bind Event to...** node and choose **Add Event > Add Custom Event** to get a custom event node that exposes additional inputs, like the **In Factory** and **In Created Object** shown above.

Your startup object can only bind to other objects that exist at the time the editor starts up. In addition, the binding becomes lost if the bound object leaves memory—for example, if a Level is closed and reopened. For that reason, it's safest to bind to objects that will be available during the entire editing session, like the Subsystem shown in the example above.

For more about binding to Blueprint events, see [Event Dispatchers](/documentation/en-us/unreal-engine/event-dispatchers-in-unreal-engine) and [Binding and Unbinding Events](/documentation/en-us/unreal-engine/binding-and-unbinding-events-in-unreal-engine). For more about Subsystems and how to access them, see [Programming Subsystems](/documentation/en-us/unreal-engine/programming-subsystems-in-unreal-engine).