# Using Customizable States

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine)  
**Processed:** 2025-06-14 16:58:37

---

When an application uses complex Customizable Objects with many parameters, updating the instances may be a costly process that takes many milliseconds. In game, there are some usage scenarios that require these updates to be interactive (big delays are not acceptable). Mutable addresses these problems with the concept of **States**.

A State represents a specific use case of a Customizable Object in your game. For example, at some point during the character creation you may want to let the player customize the face and hair of a character. During this stage, you show a close up camera of the character head and display a user interface for the related parameters: hair color, nose size, hair style, and so on. During this stage, you will not be modifying other parameters, like t-shirt color or torso tattoos. In order for Mutable to provide maximum performance, you can create a State in your Customizable Object, with the subset of parameters that you will modify in this stage. The system will generate an optimized version of the data that updates faster while in this State.

In the **Editor Preview Instance** window, you can choose which state to use by using the **State** dropdown:

The Mutable States dropdown.

You must set the state of the Customizable Object Instance before the update is issued by calling `void SetCurrentState(const FString& StateName)`.

## Runtime Parameters

The **Runtime Parameters** array defines the set of parameters that Mutable uses to optimize a given State. Each of these parameters can be of the following types:

-   [Object Group](https://github.com/anticto/Mutable-Documentation/wiki/Node-Object-Group)
-   [Float Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Float-Parameter)
-   [Enum Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Enum-Parameter)
-   [Color Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Color-Parameter)
-   [Texture Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Texture-Parameter)
-   [Projector Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Projector-Parameter)
-   [Group Projector Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Group-Projector-Parameter)

The Runtime Parameters array can be found at the bottom of the **Base Object** and **Child Object** properties:

The Runtime Parameters Array

## Optimization Options

States also give you more options in order to optimize the construction time of the Customizable Object Instance. For example, the game may have more graphic resources available because, instead of being inside a level, you are in a smaller lobby scene. This means that you can afford to temporarily use more memory for your character. For each individual State, Mutable gives you these three optimization options in addition to the Runtime Parameters:

-   **Do not Compress Runtime Textures**: Avoids texture compression for textures that may change in this State.
-   **Build Only First LOD**: Generates only the LOD 0 of the object.
-   **Forced Parameter Values**: Lists the Enumeration Parameters that are modified when the state is selected. For example, allows hiding of jackets when editing the shirt underneath. The first field represents the Enumeration Parameter name, while the second field is the forced value.

Mutable Optimization options

States are created at any Base Object Node. If no state is created, a default State with no optimized parameters and optimization options are automatically created. Also a Child Object can contain its own States. A State defined at a Child Object functions identically to a state defined at the Base Object.

Ideally, a game should have an in-game state with no optimized parameters, and several customization states to create and update objects in the different in-game customization scenarios.