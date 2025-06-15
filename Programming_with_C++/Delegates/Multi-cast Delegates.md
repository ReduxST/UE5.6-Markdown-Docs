# Multi-cast Delegates

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-delegates-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-delegates-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:36

---

Multi-cast delegates have most of the same features as single-cast delegates. They only have weak references to objects, can be used with structs, can be copied around easily, etc. Just like regular delegates, multi-cast delegates can be loaded/saved, and triggered remotely; however, multi-cast delegate functions cannot use return values. They are best used to easily pass a collection of delegates around.

## Declaring Multi-Cast Delegates

Multi-cast delegates are declared in the same manner as you [declare standard delegates](/documentation/en-us/unreal-engine/delegates-and-lambda-functions-in-unreal-engine) except they use the macro variations specific to multi-cast delegates.

| Declaration Macro | Description |
| --- | --- |
| `DECLARE_MULTICAST_DELEGATE[_RetVal, ...]\( DelegateName \)` | Creates a multi-cast delegate. |
| `DECLARE_DYNAMIC_MULTICAST_DELEGATE[_RetVal, ...]\( DelegateName \)` | Creates a dynamic multi-cast delegate. |

## Binding Multi-Cast Delegates

Multicast delegates can have multiple functions bound that all get called when the delegate fires. As a result, the binding functions are more array-like in semantics.

| Function | Description |
| --- | --- |
| `Add()` | Adds a function delegate to this multi-cast delegate's invocation list. |
| `AddStatic()` | Adds a raw C++ pointer global function delegate. |
| `AddRaw()` | Adds a raw C++ pointer delegate. Raw pointer does not use any sort of reference, so may be unsafe to call if the object was deleted out from underneath your delegate. Be careful when calling Execute()! |
| `AddLambda()` | Adds a functor. This is generally used for lambda functions that do not capture pointers. |
| `AddSPLambda()` | Adds a functor that will only be called if the weak reference to the target shared pointer is valid. |
| `AddWeakLambda()` | Adds a functor that will only be called if the weak reference to the target UObject is valid. |
| `AddSP()` | Adds a shared pointer-based (fast, not thread-safe) member function delegate. Shared pointer delegates keep a weak reference to your object. |
| `AddUObject()` | Adds a UObject-based member function delegate. UObject delegates keep a weak reference to your object. |
| `Remove()` | Removes a function from this multi-cast delegate's invocation list (performance is O(N)). Note that the order of the delegates may not be preserved! |
| `RemoveAll()` | Removes all functions from this multi-cast delegate's invocation list that are bound to the specified UserObject. Note that the order of the delegates may not be preserved! |

`RemoveAll()` will remove all registered delegates bound to the provided pointer. Keep in mind that Raw delegates that are not bound to an object pointer will not be removed by this function!

See `DelegateSignatureImpl.inl` (located in `..\Engine\Source\Runtime\Core\Public\Delegates\`) for the variations, arguments, and implementations of these functions.

## Multi-Cast Execution

Multi-cast delegates allow you to attach multiple function delegates, then execute them all at once by calling the multi-cast delegate's `Broadcast()` function. Multi-cast delegate signatures are not allowed to use a return value.

It is always safe to call `Broadcast()` on a multi-cast delegate, even if nothing is bound. The only time you need to be careful is if you are using a delegate to initialize output variables, which is generally very bad to do.

The execution order of bound functions when calling `Broadcast()` is not defined. It may not be in the order the functions were added.

| Function | Description |
| --- | --- |
| `Broadcast()` | Broadcasts this delegate to all bound objects, except to those that may have expired. |