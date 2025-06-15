# Using Mutable from C++

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mutable-from-cplusplus-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mutable-from-cplusplus-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:17

---

You can use the following document to learn about how to set up and use Mutable Characters in C++.

## Creating an Instance of a CustomizableObject

A **CustomizableObjectInstance** contains a set of values for the parameters of a **CustomizableObject**. These values can be used by actors to create in-game meshes and materials.

To create an instance of a **CustomizableObject**, you need a reference to the **Object** and a **CustomizableObjectInstance**. Getting the **Object** reference can be done either by adding a pointer as `UPROPERTY()` to the actor’s class and then setting the value from blueprints or by loading it using the asset’s path. Having both, then calling the `SetObject` function tells the instance which object to represent. This way the instance knows what parameters to store and what their default values are.

```cpp_programming
`UCustomizableObject* CustomizableObject =      LoadObject<UCustomizableObject>(nullptr, TEXT("/Game/MyCustomizableObject"));  if (CustomizableObject) {     CustomizableObjectInstance = NewObject<UCustomizableObjectInstance>();     CustomizableObjectInstance->SetObject(CustomizableObject); }`
Copy full snippet
```
UCustomizableObject\* CustomizableObject = LoadObject<UCustomizableObject>(nullptr, TEXT("/Game/MyCustomizableObject")); if (CustomizableObject) { CustomizableObjectInstance = NewObject<UCustomizableObjectInstance>(); CustomizableObjectInstance->SetObject(CustomizableObject); }

## Connecting Instances with Actors

The best way to link an instance to an actor is to use the **CustomizableSkeletalComponent**, which can be attached to the actor’s **SkeletalMeshComponent** in order to update and replace the mesh asset with a Mutable generated SkeletalMesh (in case of [Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Mesh-Component) node), or a standard Unreal Engine SkeletalMesh (in case of a [Passthrough Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Passthrough-Mesh-Component) node).

Creating the component, when the actor is added to a level, it will automatically show the customized skeletal mesh. You can reference an example setup below:

```cpp_programming
`CSkeletalComponent =          NewObject<UCustomizableSkeletalComponent>(UCustomizableSkeletalComponent::StaticClass());  // Set the instance that will be used by the actor CSkeletalComponent->CustomizableObjectInstance = CustomizableObjectInstance;  // Select the Mesh Component or Passthrough Mesh Component declared in the Customizable Object graph CSkeletalComponent->SetComponentName(TEXT("Body"));  // Attach the CustomizableSkeletalComponent to the Actor's SkeletalMeshComponent CSkeletalComponent->AttachToComponent(GetMesh(), FAttachmentTransformRules::KeepRelativeTransform);`
Copy full snippet
```
CSkeletalComponent = NewObject<UCustomizableSkeletalComponent>(UCustomizableSkeletalComponent::StaticClass()); // Set the instance that will be used by the actor CSkeletalComponent->CustomizableObjectInstance = CustomizableObjectInstance; // Select the Mesh Component or Passthrough Mesh Component declared in the Customizable Object graph CSkeletalComponent->SetComponentName(TEXT("Body")); // Attach the CustomizableSkeletalComponent to the Actor's SkeletalMeshComponent CSkeletalComponent->AttachToComponent(GetMesh(), FAttachmentTransformRules::KeepRelativeTransform);

## Changing Parameters

Parameters are stored in public arrays within each instance. These parameters can be modified directly, although it is recommended to use the API functions to avoid invalid values. Below is an example of how to modify different types of parameter:

```cpp_programming
`// Sets the bool value of the parameter "Frackles" CustomizableObjectInstance->SetBoolParameterSelectedOption(FString("Freckles"), true);  // Sets the int value of the parameter "Shirt" (Enum Type) CustomizableObjectInstance->SetIntParameterSelectedOption(FString("Shirt"), FString("BasicShirt"));  // Sets the float value of the parameter "Fatness", range from 0 to 1 CustomizableObjectInstance->SetFloatParameterSelectedOption(FString("Fatness"), 0.5f);  // Sets the color value of the parameter "EyeColor" CustomizableObjectInstance->SetColorParameterSelectedOption(FString("EyeColor"),                                                               FLinearColor(FColor::Blue));  // Sets the vector value of the parameter "VParam" CustomizableObjectInstance->SetVectorParameterSelectedOption(FString("VParam"),                                                               FLinearColor(120.f, 50.f, 180.f));  // Sets the projectors values of the parameter "Tatto" CustomizableObjectInstance->SetProjectorValue(FString("Tatto"), LocalPosition, Direction, Up, Scale, Angle,                                                 ECustomizableObjectProjectorType::Planar);`
Copy full snippet
```
// Sets the bool value of the parameter "Frackles" CustomizableObjectInstance->SetBoolParameterSelectedOption(FString("Freckles"), true); // Sets the int value of the parameter "Shirt" (Enum Type) CustomizableObjectInstance->SetIntParameterSelectedOption(FString("Shirt"), FString("BasicShirt")); // Sets the float value of the parameter "Fatness", range from 0 to 1 CustomizableObjectInstance->SetFloatParameterSelectedOption(FString("Fatness"), 0.5f); // Sets the color value of the parameter "EyeColor" CustomizableObjectInstance->SetColorParameterSelectedOption(FString("EyeColor"), FLinearColor(FColor::Blue)); // Sets the vector value of the parameter "VParam" CustomizableObjectInstance->SetVectorParameterSelectedOption(FString("VParam"), FLinearColor(120.f, 50.f, 180.f)); // Sets the projectors values of the parameter "Tatto" CustomizableObjectInstance->SetProjectorValue(FString("Tatto"), LocalPosition, Direction, Up, Scale, Angle, ECustomizableObjectProjectorType::Planar);

## Changing States

As explained in the [States](/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine) page, Mutable has the concept of States that enable certain optimizations depending on the use case. Given an Customizable Object Instance, its State can be queried and changed using the following API functions:

```cpp_programming
`// Get the current State CustomizableObjectInstance->GetCurrentState(FString("InGame"));  // Set the current State. Requires the Customizable Object Instance to be updated FString State = CustomizableObjectInstance->SetCurrentState();`
Copy full snippet
```
// Get the current State CustomizableObjectInstance->GetCurrentState(FString("InGame")); // Set the current State. Requires the Customizable Object Instance to be updated FString State = CustomizableObjectInstance->SetCurrentState();

Given a Customizable Object, we can query the available States and the parameters in each State:

```cpp_programming
`// Get the number of States int32 Count = CustomizableObject->GetStateCount()  // Get the State Name of the given State index FString Name = CustomizableObject->GetStateName(1);  // Get the number of parameters of a given State int32 ParameterCount = CustomizableObject->GetStateParameterCount(FString("InGame"));  // Get the name of parameter index in a given State FString ParameterName = CustomizableObject->GetStateParameterName(FString("InGame"), 1);`
Copy full snippet
```
// Get the number of States int32 Count = CustomizableObject->GetStateCount() // Get the State Name of the given State index FString Name = CustomizableObject->GetStateName(1); // Get the number of parameters of a given State int32 ParameterCount = CustomizableObject->GetStateParameterCount(FString("InGame")); // Get the name of parameter index in a given State FString ParameterName = CustomizableObject->GetStateParameterName(FString("InGame"), 1);

## Updating Instances

Changing parameters or States does not update the Instance automatically. To apply these changes, the instance must be updated by calling the `UpdateSkeletalMeshAsync()` method, within the **CustomizableSkeletalComponent** class. Doing so will replace the **SkeletalMesh** component of all actors using the same **CustomizableObjectInstance** with a generated instance using those changes.

```cpp_programming
`// Update Instances CSkeletalComponent->UpdateSkeletalMeshAsync();`
Copy full snippet
```
// Update Instances CSkeletalComponent->UpdateSkeletalMeshAsync();

## Instance Updated Delegate

You might want to run a specific method after the mesh has been updated, such as to trigger an animation, or to make the mesh visible. In order to run a method after the mesh has been updated, Mutable provides a delegate where callbacks can be registered. This delegate will broadcast the completion of the skeletal mesh update to the registered callbacks.

```cpp_programming
`// Bind "this" UObject's "OnCustomizableSkeletalUpdated" method as a callback for the delegate  CSkeletalComponent->UpdatedDelegate.BindUObject(this, &MyCustomCharacter::OnCustomizableSkeletaUpdated);  // Unbind callbacks  CSkeletalComponent->UpdatedDelegate.Unbind();`
Copy full snippet
```
// Bind "this" UObject's "OnCustomizableSkeletalUpdated" method as a callback for the delegate CSkeletalComponent->UpdatedDelegate.BindUObject(this, &MyCustomCharacter::OnCustomizableSkeletaUpdated); // Unbind callbacks CSkeletalComponent->UpdatedDelegate.Unbind();