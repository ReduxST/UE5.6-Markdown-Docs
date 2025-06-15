# Function Calls

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/function-calls-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/function-calls-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:30

---

**Function Calls** are actions that can be formed within Blueprints that correspond to functions belonging to a targeted Actor or Object. In the case of Level Blueprints, the associated Actor in many cases is the Level Blueprint itself. Function Calls are displayed as boxes with titles that show the name of the function. Different types of function calls have different color titles.

## Self

**Self Function Calls** are functions that belong to the Blueprint itself, by way of being declared in the class the Blueprint derives from or a parent class.

## Other

**Other Function Calls** are functions that belong to other Objects or Actors besides the Blueprint. For example, the Blueprint might have a StaticMeshComponent that can have its mesh changed via a SetStaticMesh function call. Since this function belongs to the StaticMeshComponent and not the Blueprint, it is an Other Function Call.

## Pure

**Pure Function Calls** are special actions that can be performed that do not directly affect the world or the Objects in it. These are generally things like functions that output a property value, or mathematical operations such as adding, subtracting, multiplying, dividing, etc. two values, the results of which have no impact on anything. It is the assigning or use of the result that generates an effect on the world.

|   |   |
| --- | --- |
| ![Pure Function Call Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8001290-6e1a-4bb8-8c45-b2a99e0860a0/k2_node_func_pure.png) | ![Math Pure Function Call Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c8e75b2-39f2-4acc-b6cd-0909e657b7ba/k2_node_func_pure_math.png) |
| Standard | Compact |