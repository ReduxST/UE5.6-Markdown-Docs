# Dynamic Delegates

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-delegates-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-delegates-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:23

---

Dynamic delegates can be serialized, their functions can be found by name, and they are slower than regular delegates.

## Declaring Dynamic Delegates

Dynamic delegates are declared in the same manner as you [declare standard delegates](/documentation/en-us/unreal-engine/delegates-and-lambda-functions-in-unreal-engine) except they use the macro variations specific to dynamic delegates.

| Declaration Macro | Description |
| --- | --- |
| `DECLARE_DYNAMIC_DELEGATE[_RetVal, ...]\( DelegateName \)` | Creates a dynamic delegate. |
| `DECLARE_DYNAMIC_MULTICAST_DELEGATE[_RetVal, ...]\( DelegateName \)` | Creates a dynamic multi-cast delegate. |

## Dynamic Delegate Binding

| Helper Macro | Description |
| --- | --- |
| `BindDynamic( UserObject, FuncName )` | Helper macro for calling BindDynamic() on dynamic delegates. Automatically generates the function name string. |
| `AddDynamic( UserObject, FuncName )` | Helper macro for calling AddDynamic() on dynamic multi-cast delegates. Automatically generates the function name string. |
| `RemoveDynamic( UserObject, FuncName )` | Helper macro for calling RemoveDynamic() on dynamic multi-cast delegates. Automatically generates the function name string. |

## Executing Dynamic Delegates

The function bound to a delegate is executed by calling the delegate's `Execute()` function. You must check if delegates are "bound" before executing them. This is to make the code more safe as there may be cases where delegates have return values and output parameters that are uninitialized and subsequently accessed. Executing an unbound delegate could actually scribble over memory in some instances. You can call `IsBound()` to check if the delegate is safe to execute. Also, for delegates that have no return value, you can call `ExecuteIfBound()`, but be wary of output parameters that may be left uninitialized.

| Execution Functions | Description |
| --- | --- |
| `Execute` | Executes a delegate without checking its bindings |
| `ExecuteIfBound` | Checks that a delegate is bound, and if so, calls Execute |
| `IsBound` | Checks whether or not a delegate is bound, often before code that includes an `Execute` call |

See [Multi-cast Delegates](/documentation/en-us/unreal-engine/multicast-delegates-in-unreal-engine) for details on executing multi-cast delegates.