# UMG Viewmodel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-viewmodel-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-viewmodel-for-unreal-engine)  
**Processed:** 2025-06-14 16:55:39

---

Typically, UI developers break backend data and visual design into separate systems. This makes the process of building the user interface (UI) less destructive and more efficient, as designers can change the visual presentation without breaking the code behind the UI, and programmers can focus on data and systems without needing a completed frontend. The **Viewmodel** plugin provides a medium for this workflow by introducing Viewmodel assets and **View Bindings**.

## Workflow

Viewmodels contain variables that you can use in your UI. Designers can bind fields in their UI to these using the **View Binding** panel, while programmers can build the Viewmodels themselves and tie them in with the application's code as they see fit.

Once you add a Viewmodel to a **UMG** widget, you can access it and call functions or update variables. The Viewmodel pushes updates to any widgets whose fields are bound to its variables.

[![Flow chart describing the Viewmodel workflow](https://dev.epicgames.com/community/api/documentation/image/626d320b-962d-4d5d-b36f-63bec9034800?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/626d320b-962d-4d5d-b36f-63bec9034800?resizing_type=fit)

This is a more efficient alternative to raw attribute binding, as it only updates widgets when you update the variables. It also provides the benefits of an event-driven UI framework without the implementation time setting one up manually.

## Required Setup

To use Viewmodels in your project's UI, enable the **UMG Viewmodel** plugin in the **Plugins** menu.

[![Enabling the Viewmodel plugin in the plugins menu](https://dev.epicgames.com/community/api/documentation/image/77785f7a-3c30-40d0-9037-fbca305cea68?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/77785f7a-3c30-40d0-9037-fbca305cea68?resizing_type=fit)

If you do not enable this plugin, you will not be able to use the `UMVVMViewModelBase` class, and you will not be able to use View Bindings in UMG.

## Viewmodels

Viewmodels have two main purposes:

-   Maintain a manifest of the variables needed for your UI.
    
-   Provide a medium of communication between your UI and the rest of your application.
    

When you need your UI to be aware of a variable, you can add it to a Viewmodel, then add the Viewmodel to your widget and bind fields to it. When you need to update your variables, you can get a reference to the Viewmodel and set them from there. They then notify the widgets bound to those variables about the changes and update them.

### Create a Viewmodel in Blueprint

You can create a Viewmodel in Blueprint by extending the **MVVMViewModelBase** class.

[![Select MVVMViewModelBase for your Blueprint class](https://dev.epicgames.com/community/api/documentation/image/578747d3-8fdd-445a-9bf7-6cd7fd24a3b5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/578747d3-8fdd-445a-9bf7-6cd7fd24a3b5?resizing_type=fit)

You can also create a Viewmodel by implementing the `INotifyFieldValueChanged` interface in C++.

#### Viewmodel Variables in Blueprint

To broadcast changes to widgets that are bound to your parameters, you need to mark variables or functions as **FieldNotifies**. Click the bell icon next to a function or variable to make it a FieldNotify.

[![Create variables in the Variables panel](https://dev.epicgames.com/community/api/documentation/image/5a718bbb-9a31-4b56-a572-e90a5dc640b7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5a718bbb-9a31-4b56-a572-e90a5dc640b7?resizing_type=fit)

Any calls to set a FieldNotify variable are labeled **Set W/Broadcast** instead of the usual Set node.

[![A Set with Broadcast node in Blueprint](https://dev.epicgames.com/community/api/documentation/image/145026e1-bfb9-4cfa-bd39-9e373aff15df?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/145026e1-bfb9-4cfa-bd39-9e373aff15df?resizing_type=fit)

Whenever you set these variables with a new value in your gameplay code, they send a message to any widgets that are bound to them telling them to update.

#### Viewmodel Functions in Blueprint

Functions can also be treated as FieldNotifies. To use a function as a FieldNotify, it must meet the following conditions:

-   It must be a Pure function.
    
-   It must be marked Const.
    
-   It must return only one value.
    
-   It must not take any input variables.
    

For example, you can create a Getter function that returns the percentage of a character's current health versus their maximum health. This is a good alternative if you do not want to create a separate variable to hold the character's health as a percentile.

[![Example of a Getter that converts Current Health and Max Health to a percentile](https://dev.epicgames.com/community/api/documentation/image/3ac674f8-fc20-4d9c-9187-f1939887d4fc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3ac674f8-fc20-4d9c-9187-f1939887d4fc?resizing_type=fit)

You have to trigger your FieldNotify functions from a FieldNotify variable when it changes. See [Use a FieldNotify Variable to Trigger Other FieldNotifies](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-viewmodel-for-unreal-engine) for more information.

Getter and Setter utility functions in your Viewmodel can perform other operations and handle derived values. For example, if you have a Viewmodel that tracks a player's health, you might need to display it in text as an integer even though your gameplay logic treats it as a float, and you will need to convert it to a percentage if you are using it in a ProgressBar widget.

A SetCurrentHealth function gives you the opportunity to set derived values in other FieldNotify variables, or to perform other logic your game may need.

[![A function setting current health with limitations.](https://dev.epicgames.com/community/api/documentation/image/7eef0fe4-c5b3-4fbe-b095-f64b67c0317a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7eef0fe4-c5b3-4fbe-b095-f64b67c0317a?resizing_type=fit)

You should not create Getter functions just to return the value of a FieldNotify variable, as getting the FieldNotify variable's value directly is sufficient and the extra Getter function may be confusing when you try to bind your Viewmodel variables to widgets later. However, you can use FieldNotify Getters to handle conversions to needed formats, like strings, without making an extra variable to hold that information.

[![A function that outputs Current Health and Max Health as a string](https://dev.epicgames.com/community/api/documentation/image/f3849b43-da69-48b2-9253-eac09ce615ea?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f3849b43-da69-48b2-9253-eac09ce615ea?resizing_type=fit)

#### Use a FieldNotify Variable to Trigger Other FieldNotifies

FieldNotify variables can automatically broadcast other FieldNotify functions when they change. To set this up, follow these steps:

1.  Click the FieldNotify variable you want to use in the Variables panel.
    
2.  In the Details panel, click the dropdown next to the Field Notify checkbox. It displays all valid FieldNotifies you can trigger with this variable, including the FieldNotifies for other variables and functions.
    
    [![Set a FieldNotify in the Details Panel](https://dev.epicgames.com/community/api/documentation/image/ed96de1b-263e-4fd8-9fc3-22c63a6c90d0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ed96de1b-263e-4fd8-9fc3-22c63a6c90d0?resizing_type=fit)
    
3.  Check the boxes for each FieldNotify you want to trigger in response to changing this variable.
    

Now when you change your target variable, any FieldNotify functions you have tied to it will trigger in addition to the one for the target variable itself. This can simplify handling derived values compared with using more variables.

### Create a Viewmodel in C++

You can create a Viewmodel in C++ by implementing the `INotifyFieldValueChanged` interface. You can also extend the class `UMVVMViewModelBase`, which implements it by default. Viewmodels are `UObjects` that depend on FieldNotify variables and functions to broadcast changes to widgets that are bound to them.

Unlike in Blueprint, in C++ you need to manually call FieldNotify broadcasts.

The Viewmodel system uses the same access rights as Blueprint. The variables and functions need to be accessible in Blueprint to be accessed by the Viewmodel system.

#### Variables with FieldNotifies

When you define variables in your Viewmodel, each variable must have a `UPROPERTY` macro with the `FieldNotify` specifier. The full list of specifiers used for FieldNotify variables is as follows:

| UPROPERTY Specifier | Description |
| --- | --- |
| 
`FieldNotify`

 | 

Make the property available for the field notification broadcasts system.

 |
| 

`Setter`

 | 

States that the variable should allow setting its value. This assumes that the Setter function will have a name with the format `Set[Variable Name]`

 |
| 

`Setter="[FUNCTION_NAME]"`

 | 

As Setter, but you can provide the name of a custom function to use it as the Setter.

 |
| 

`Getter`

 | 

States that the variable should allow retrieving its value. This assumes that the Getter function will have a name with the format `Get[VariableName]`

 |
| 

`Getter="[FUNCTION_NAME]"`

 | 

As Getter, but you can provide the name of a custom function to use it as the Getter.

 |

The `FieldNotify` specifier is required to broadcast value changes to widgets. Any variable with this specifier will appear in the View Binding menu. Without `FieldNotify` you will only be able to bind to the variable in OneTime mode.

You can decide whether to provide the `Setter` or `Getter` specifiers. If you decide not to provide one of them, you will not be able to perform that operation outside of this class. Specifying only the Getter and Setter specifiers without a function name is sufficient when you only want to trigger a notification for the variable itself. They are automatically executed from script (Blueprint, viewmodel, sequencer, …) when accessing the variable. They are not automatically called from cpp code.

Custom Getters and Setters are useful when:

-   You need to perform an operation before retrieving a variable.
    
-   You want to trigger other functions or update other variables when setting a variable.
    

If you create custom Getter or Setter functions, do not make them `UFUNCTIONS`, as it will create redundant listings for Get and Set functions in Blueprint. The `UPROPERTY` macro for the variable already provides access to these in the form of the variable's Get and Set nodes. You should also make any custom Getters `const` functions, as their only job should be returning a value.

Since C++ does not force the user to call the Getter or Setter functions, the variables should be protected or private to prevent user mistakes.

C++

```code
`protected:  	  /** 	   * The variable can be accessed from the viewmodel system and can be written to. Enable TwoWay. 	   * FieldNotify enabled the OneWay binding mode (enable notification). 	   * It's protected in cpp (force the user to use the Getter/Setter). 	   * It's public in Blueprint 	   * Blueprint/ViewBindings/... will use the Getter/Setter. 	   */`


```

Expand codeCopy full snippet(25 lines long)

#### Functions with FieldNotifies

You can create custom functions that broadcast `FieldNotifies`, and you can bind widgets' properties to these functions the same way as you can with variables. Functions used in this way must follow these requirements:

-   They must have the `UFUNCTION` macro with the `FieldNotify` and `BlueprintPure` specifiers.
    
-   They must take no arguments.
    
-   They must be `const` functions.
    
-   They must return only a single value (no out argument).
    
-   They must be accessible.
    

Functions can be useful if you want a widget bound to values that are derived or converted from other variables, but do not want to create an extra variable to hold that information.

For example, the following function is a FieldNotify for returning the percent value of a character's current health divided by their maximum health:

C++

```code
`UFUNCTION(BlueprintPure, FieldNotify)  		float GetHealthPercent() const 		{ 			//Check to avoid dividing by zero  			if (MaxHealth != 0) 			{ 				return (float) CurrentHealth / (float) MaxHealth; 			}`

```

Expand codeCopy full snippet(15 lines long)

You need to manually notify that `GetHealthPercent` changed when `CurrentHealth` or `MaxHealth` changed.

#### Triggering FieldNotifies with Macros

When changing variables, functions need to call one of the Viewmodel notification macros to broadcast changes to bound widgets. The list of available macros is as follows:

| ViewModel Macro | Description |
| --- | --- |
| 
UE\_MVVM\_BROADCAST\_FIELD\_VALUE\_CHANGED(\[Member name\])

 | 

Broadcasts the event.

 |
| 

UE\_MVVM\_SET\_PROPERTY\_VALUE(\[Member Name\], \[New Value\])

 | 

Test if the value of the field has changed, then set the new value of the field and broadcast the event..

 |

The `SET_PROPERTY_VALUE` macros do the same thing as `BROADCAST_FIELD_VALUE` macros, except that the `SET_PROPERTY_VALUE` macros check to see if the value changed before assigning the value and then broadcasting. This is a very common check when creating Setters for Viewmodels, and it is included for convenience.

The `BROADCAST_FIELD_VALUE_CHANGED` macros can take either the variable itself, if you want to notify widgets bound directly to that value, or they can take the names of functions.

#### Example

The following code snippet is an example of a Viewmodel class using the above concepts. GetHealthPercent is defined as a separate function from the Getters and Setters, but the Setters call it in addition to notifying when the variables themselves are changed.

C++

```code
`UCLASS(BlueprintType) 	class UVMCharacterHealth : public UMVVMViewModelBase 	{ 	GENERATED_BODY()  	private: 	UPROPERTY(BlueprintReadWrite, FieldNotify, Setter, Getter, meta=(AllowPrivateAccess)) 		int32 CurrentHealth; 		 		UPROPERTY(BlueprintReadWrite, FieldNotify, Setter, Getter, meta=(AllowPrivateAccess))`

```

Expand codeCopy full snippet(55 lines long)

### Add a Viewmodel to a Widget

You can add Viewmodels to a widget in the Viewmodels window in UMG. You can find this under **Window** > **Viewmodels** in the UMG Designer tab.

[![Locating the Viewmodel window in the Window dropdown](https://dev.epicgames.com/community/api/documentation/image/1492a433-63e5-431a-99dc-b032411a9acd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1492a433-63e5-431a-99dc-b032411a9acd?resizing_type=fit)

Click the **\+ Viewmodel** button to select one of your project's Viewmodels, then click **Select**.

[![Adding a Viewmodel to a widget](https://dev.epicgames.com/community/api/documentation/image/c0ab41a2-c4f1-489f-940d-295dc94b33be?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c0ab41a2-c4f1-489f-940d-295dc94b33be?resizing_type=fit)

### Initialize Your Viewmodel

When you click a Viewmodel in the Viewmodels window, you can choose how to initialize it with the **Creation Type** setting. The following methods are available:

| Viewmodel Creation Type | Description |
| --- | --- |
| 
**Create Instance**

 | 

The widget automatically creates its own instance of the Viewmodel.

 |
| 

**Manual**

 | 

The widget initializes with the Viewmodel as null, and you need to manually create an instance and assign it.

 |
| 

**Global Viewmodel Collection**

 | 

Refers to a globally-available Viewmodel that can be used by any widget in your project. Requires a **Global Viewmodel Identifier**.

 |
| 

**Property Path**

 | 

At initialization, execute a function to find the Viewmodel. The **Viewmodel Property Path** uses member names separated by periods. For example: GetPlayerController.Vehicle.ViewModel. Property paths are always relative to the widget.

 |

Viewmodels do not necessarily have a one-to-one relationship with widgets. There are multiple ways to set them up and assign them to widgets, and it is possible for multiple widgets to take information from a single Viewmodel. Each creation type method is detailed below.

#### Create Instance

The **Create Instance** creation method automatically creates a new instance of the Viewmodel for each unique instance of the widget. This means, if you have several copies of the same widget in the viewport, and you change the Viewmodel variables for one of them, only that widget will update, while all the other copies will remain the same. Similarly, if you create multiple different widgets that use the same Viewmodel, none of those widgets will be aware of changes to each other's information. The other methods below are useful for when you want multiple widgets to reference the same data. You also have the option to set the viewmodel after its creation.

You can assign the viewmodel after the Initialize callback in C++ or during the Initialize callback in Blueprint. The system will only create a new instance if the viewmodel was not set. Viewmodel creation is done between the PreConstruct and the Construct event.

#### Manual

The **Manual** creation method requires you to create an instance of the Viewmodel yourself somewhere in your application's code, then assign it to the widget manually. The widget has a Viewmodel object reference, but it will have a null value until you assign a Viewmodel to it. You can also assign your Viewmodel on creation in the Create Widget node.

[![Example of the Manual creation mode](https://dev.epicgames.com/community/api/documentation/image/6b36887e-ab9c-4833-9d65-9f2592d286ca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b36887e-ab9c-4833-9d65-9f2592d286ca?resizing_type=fit)

Once you have assigned your Viewmodel, you can update it whenever you want to update your UI without getting any references to widgets. This provides an opportunity to assign the same Viewmodel from an Actor class to multiple different widgets in your UI.

#### Property Paths

The **Property Path** creation method provides an alternative that is potentially cleaner and requires less code support. Instead of other classes reaching inside the widget to set its Viewmodel reference, the widget reaches out with a series of function calls and references to fetch the Viewmodel. The Property Path field in the editor expects a series of member names separated by periods, and it assumes that the starting point for calling these functions is `Self`. In other words, it always starts at the widget you are editing.

Do not manually specify `Self` in your Property Paths, as the Property Path field already assumes you are starting with a reference to `Self`.

As an example, the following field gets the owning player controller of the widget, then gets a Viewmodel on the vehicle it is currently controlling:

C++

`GetPlayerController.Vehicle.ViewModel`

GetPlayerController.Vehicle.ViewModel

Copy full snippet(1 line long)

You can also call functions you define in your Blueprint, which can help condense the logic for your Property Paths and provide extra flexibility. For example, the following function gets the Character Health Viewmodel from the character who owns the widget:

[![Example of the Property Path creation mode](https://dev.epicgames.com/community/api/documentation/image/f76253a4-9fc1-4a22-a35c-3354e559562e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f76253a4-9fc1-4a22-a35c-3354e559562e?resizing_type=fit)

You can then use this function's name as the Property Path:

C++

`GetHealthViewModel`

GetHealthViewModel

Copy full snippet(1 line long)

#### Global Viewmodel Collection

The **Global Viewmodel Collection** is a globally accessible list of Viewmodels in the **MVVM Game Subsystem**. These are ideal for handling variables that may need to be accessed throughout your UI, such as settings for your game's option's menu. To add a Viewmodel to the Global Viewmodel Collection in Blueprint, follow these steps:

1.  Add a reference to the MVVM Game Subsystem.
    
2.  Drag a pin from the MVVM Game Subsystem node, then call **Get Viewmodel Collection**.
    
3.  Drag a pin from the Global Viewmodel collection, then call **Add Viewmodel Instance**.
    

You can then construct an instance of the Viewmodel and add it to the collection with this node. The **Game Instance** class is a convenient place to initialize these.

[![Example of the Global View Model Collection creation mode](https://dev.epicgames.com/community/api/documentation/image/cfc58ba8-6b3d-4865-93cd-1ab43173305c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cfc58ba8-6b3d-4865-93cd-1ab43173305c?resizing_type=fit)

When choosing Global Viewmodel Collection as an initialization mode, provide the **Context Name** from your Add Viewmodel Instance node in the **Global Viewmodel Identifier**. This name must match the class name for the Viewmodel. For example, if your Viewmodel is called VM\_GraphicsOptions you would provide that as both the Context Name and the Global Viewmodel Identifier.

### Access Your Viewmodel's Members

After you have assigned a Viewmodel to a widget, you can access it as a property of the widget in your Blueprint. It will be located under the **Variables** > **Viewmodel** category. Once you have a reference to a Viewmodel, you can access its variables and functions.

[![Accessing Viewmodel properties in Blueprint](https://dev.epicgames.com/community/api/documentation/image/b3940c2d-93e2-4c0b-bee2-427e73f2b78b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b3940c2d-93e2-4c0b-bee2-427e73f2b78b?resizing_type=fit)

Depending on what options are configured in the Viewmodel, you may not have access to all internal functions or Setters.

### Working With Arrays

Arrays are not normally accessible in Viewmodels. To access an array in your Viewmodel, create your own `FieldNotify` functions to add, remove, and get members in the array directly from the Viewmodel itself.

You can use arrays with Views (ListView, TreeView, TileView). You need to notify when an element was added, removed, or moved in the array.

## View Bindings

After you have created a Viewmodel, you can add it to a widget in the UMG editor and target it with the View Bindings window.

### Add a View Binding to a Widget

There are two methods for adding View Bindings to widgets: you can add them with the property binding dropdown in the Details panel, or you can use the View Binding menu to manage all of your widget's bindings.

#### Using Drag-and-Drop

In the Viewmodels window, click a variable or function you want to bind to a widget, then drag it to the **Bind** dropdown for the field you want to bind it to. This is the simplest, fastest method for creating View Bindings.

#### Using the Details Panel

To use View Bindings in the Details Panel, select the widget you want to add a binding to, then click the **Bind** dropdown on the property you want to bind. Any Viewmodel variables and functions that are valid for that property will appear at the bottom of the dropdown. Click one to assign the binding.

[![Add a binding through the Details Panel using the binding drop-down](https://dev.epicgames.com/community/api/documentation/image/8859af2c-5b8a-4e71-90e1-5d240f96ac31?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8859af2c-5b8a-4e71-90e1-5d240f96ac31?resizing_type=fit)

To avoid confusion, disable the legacy binding system. To do this, go into **Project Settings** > **Editor > Widget Designer (Team)** and set the **Property Binding Rule** to **Prevent**. This will remove the option to bind traditional properties to your widgets' parameters.

[![Disable the legacy binding system in the Project Settings mennu](https://dev.epicgames.com/community/api/documentation/image/db225e79-f061-41a0-abd4-4f4a42cdfce8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/db225e79-f061-41a0-abd4-4f4a42cdfce8?resizing_type=fit)

You can also disable Details Panel bindings for Viewmodels by disabling **Allow Binding from Detail View** in the **Plugins** > **Model View Viewmodel** section. You can still use the View Binding menu to bind Viewmodel variables.

[![Disable all bindings in the Details Panel](https://dev.epicgames.com/community/api/documentation/image/427155d8-f8f5-489f-88dd-f62a0da3cc7e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/427155d8-f8f5-489f-88dd-f62a0da3cc7e?resizing_type=fit)

#### Using the View Binding Menu

The View Bindings window offers more detailed control over how your View Bindings behave. Open the View Binding window by clicking **Window** > **View Binding** in the UMG Designer tab.

[![Locating the View Binding menu in the Window dropdown](https://dev.epicgames.com/community/api/documentation/image/5c5e8cd9-14d3-4610-b471-acae00c130db?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5c5e8cd9-14d3-4610-b471-acae00c130db?resizing_type=fit)

Click **\+ Add Widget** to add an entry to the View Binding list.

[![Adding a widget to the View Binding list](https://dev.epicgames.com/community/api/documentation/image/99aa1fca-c463-41d4-a161-4ba4e55de77d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/99aa1fca-c463-41d4-a161-4ba4e55de77d?resizing_type=fit)

Any Viewmodel you have added in the Viewmodels window is eligible for bindings.

In the current version of Unreal Engine, if you bind a Viewmodel with the View Bindings menu, then reassign it with the Details panel, the binding might become invalid. To fix this, you should delete the binding from the View Bindings menu, then reassign it.

### Configure Your View Binding

View Bindings contain the following information:

-   The **target widget** and **target** **Viewmodel** for the binding.
    
-   The **widget property** and **Viewmodel** **property** that you want to bind to one another.
    
-   The **direction** of the binding, which determines the flow of information between the two target properties.
    
-   The **update type** of the binding.
    
-   The **enabled / disabled** toggle, which removes the binding from runtime on disable. This means the binding will not compile and will not be available at runtime.
    

The following sections provide details about each of these fields and how to configure them.

#### Choose the Target Widget

The first dropdown for a View Binding entry chooses the widget you want to add the View Binding to. When you click it, the dropdown shows the hierarchy for your widget, and you can choose either the parent widget itself or any of its child widgets. Click **Select** to confirm your selection.

[![Selecting the widget you want to target for a View Binding](https://dev.epicgames.com/community/api/documentation/image/f46a622f-a48d-4827-9baf-36d6359f66cd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f46a622f-a48d-4827-9baf-36d6359f66cd?resizing_type=fit)

#### Create View Binding Entries

Underneath the target widget, there are entries for individual properties you want to set up Viewmodel bindings for. Each binding is indented from the widget that it belongs to. You can add multiple bindings for a single widget by clicking the **+** button next to the widget's dropdown. Each binding must target a different property.

[![Adding View Binding entries to a target widget](https://dev.epicgames.com/community/api/documentation/image/f0fedea2-44a1-4571-8797-0361ae328374?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0fedea2-44a1-4571-8797-0361ae328374?resizing_type=fit)

#### Select the Widget Property

The first dropdown in a View Binding entry displays a list of the target widget's variables and functions. For example, if you use a select Progress Bar widget, the **Percent** property will be available.

[![Select the target property for the view binding](https://dev.epicgames.com/community/api/documentation/image/9574ddba-47a4-4c85-8e57-aea9f868c2c4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9574ddba-47a4-4c85-8e57-aea9f868c2c4?resizing_type=fit)

For a property or function defined in C++ to appear in this list, it must be visible to the Unreal Engine reflection system with the `UFUNCTION` or `UPROPERTY` macros. Blueprint-defined variables and functions are automatically available.

#### Select the Viewmodel Property

The third dropdown selects both the Viewmodel you want to target, as well as which of its properties you want to use for the View Binding. When you click it, it displays a list of the Viewmodels you added to this widget.

[![Choosing the target property for a View Binding](https://dev.epicgames.com/community/api/documentation/image/be343dbb-f7e4-4505-a3d9-4f9362238161?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/be343dbb-f7e4-4505-a3d9-4f9362238161?resizing_type=fit)

Click the Viewmodel you want to use to display a list of variables and functions that are viable for View Bindings. Because this is a `One Way To Widget`, for variables and functions to appear here, they must have the `FieldNotify` specifier.

#### Set The Bind Direction

The second dropdown selects the **Bind Direction** for the View Binding. This determines how information flows between the widget and the Viewmodel.

[![The bind direction dropdown](https://dev.epicgames.com/community/api/documentation/image/a816260a-2fe7-4920-a80a-5da593a1ebc3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a816260a-2fe7-4920-a80a-5da593a1ebc3?resizing_type=fit)

The available bind directions are as follows:

| Bind Direction | Description |
| --- | --- |
| 
One Time to Widget

 | 

The binding applies from the Viewmodel to the widget only once. It updates the selected widget property.

 |
| 

One Way to Widget

 | 

The binding applies only from the Viewmodel to the widget. Any time you update the corresponding variable in the Viewmodel, it notifies the widget that the variable has changed and updates the selected widget property. Alternatively, if you chose a function, calling that function updates the selected widget property.

 |
| 

One Way to Viewmodel

 | 

The binding applies only from the widget to the Viewmodel. Any time either the user or your code changes the selected property in the widget, it applies that change to the Viewmodel property. Typical examples include user-edited text fields or graphics options.

 |
| 

Two Way

 | 

The binding applies in both directions.

 |

All bindings are executed once, between the PreConstruct and the Construct event. If the Bind direction is TwoWay, then only the OneWay binding will be executed. If a viewmodel value changes, with a SetViewmodel, all bindings that include that viewmodel will be executed.

### Using Conversion Functions

As an alternative to binding directly to a variable, you can select **Conversion Functions**. These provide an interface for translating variables from your Viewmodel into different types of data, such as changing integers into text. Conversion Functions appear in the Viewmodel property dropdown underneath the list of Viewmodels.

[![Selecting conversion functions](https://dev.epicgames.com/community/api/documentation/image/4db5af7f-ebab-4417-9d82-3088094c0903?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4db5af7f-ebab-4417-9d82-3088094c0903?resizing_type=fit)

When you choose a Conversion Function, a list of options for configuring that function's arguments appears beneath the dropdowns for the View Binding.

[![A list of the options for conversion functions in the View Bindings menu](https://dev.epicgames.com/community/api/documentation/image/94085347-480f-4d6e-87fd-3e0307747a1f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/94085347-480f-4d6e-87fd-3e0307747a1f?resizing_type=fit)

If you click the **link** button for one of these properties, you can bind that property to any Viewmodel value.

[![Adding a value to a conversion function](https://dev.epicgames.com/community/api/documentation/image/db3da564-3729-4b28-bf7e-67b47c8a2677?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/db3da564-3729-4b28-bf7e-67b47c8a2677?resizing_type=fit)

New conversion functions can be added globally or on the UserWidget (Widget Blueprint). The function cannot be an event, network, deprecated, or editor-only. The function needs to be visible to Blueprint, have one input argument, and one return value. If defined globally, the function also needs to be static. If defined on the UserWidget, the function also needs to be pure and const.

## Best Practices for Creating Viewmodels

When creating your Viewmodels, you should use small, concise Viewmodels instead of large, monolithic ones. This practice makes debugging your UI easier.

For example, you could create a Viewmodel representing a Character in an RPG, with a complete array of characteristics, an inventory, and hit points. However, to debug any part of the UI that depends on this Viewmodel, you would first need to spawn an entire character to fill the Viewmodel's data. If you split these up into different components, you can more easily fill them with test data when debugging.

### Nested Viewmodels

You can nest Viewmodels inside other Viewmodels, which can provide more flexibility when working with complex sets of data.

For example, you can create a Viewmodel for a Character's health, another Viewmodel for their attributes (Strength, Dexterity, Magic), and then you can nest both of those in a Viewmodel representing a full Character. For testing purposes, individual widgets can take in data from Viewmodels that are relevant to them (for example, a health bar can reference character health), while your final product can use the full set in the nested Viewmodel.