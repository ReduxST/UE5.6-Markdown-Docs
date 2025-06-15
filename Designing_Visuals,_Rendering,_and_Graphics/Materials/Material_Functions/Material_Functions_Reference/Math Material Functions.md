# Math Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/math-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/math-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:22

---

Math functions perform basic math equations on the values of pixels within a Material network.

## Add Components

The **AddComponents** function takes in a Vector2, a Vector3, or a Vector4, combines their components together and then outputs the result. You must use the appropriate output for the corresponding input. For example, if you input an image into *f3 (Vector3)*, then you must use the *f3* output.

| Item | Description |
| --- | --- |
| Inputs |   |
| **f2 (Vector2)** | Takes in a Vector2 value so that its components can be added together and sent to the *f2* output. |
| **f3 (Vector3)** | Takes in a Vector3 value so that its components can be added together and sent to the *f3* output. |
| **f4 (Vector4)** | Takes in a Vector4 value so that its components can be added together and sent to the *f4* output. |
| Outputs |   |
| **f2 (Vector2)** | Outputs the combined value of the components from the *f2* input. |
| **f3 (Vector3)** | Outputs the combined value of the components from the *f3* input. |
| **f4 (Vector4)** | Outputs the combined value of the components from the *f4* input. |

![Add Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70823f81-3266-497e-89fb-4842c2fd509c/add-components.png)

Since each input is calculated individually for its corresponding output, you may use all three inputs on a single node, so long as you also use an output for each one. For instance, you may use one AddComponents function node to combine the components of a Vector2, utilizing the *f2* output, and use the same node to combine the components of a Vector3, utilizing the *f3* output.

## Pi

The **Pi** function serves as a constant for Pi, as calculated to the 6th decimal place (3.141592). The node also comes with an input for a multiplier.

| Inputs | Description |
| --- | --- |
| **Multiplier (Scalar)** | Input a value that will be multiplied times pi. |

![Pi](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2384008b-a7dc-4967-a602-4d4a89da50c9/pi-function.png)

## LinearSine

The **LinearSine** function takes in a scalar value and outputs the linear sine (or rounded linear sine) of that value, running between 0 and 1. If you connect a Time expression to the value input and use the Linear Sine, you can see animation in the output that coincides with a linear sine wave.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Value** (Scalar) | This is the incoming value to which the linear sine function will be applied. If this value changes over time, the output will be a wave. |
| **Period** (Scalar) | Period controls the time required to make one full transition. Input values higher than 1 to slow the wave down. |
| **\-1 to 1** (StaticBool) | Setting this to *true* scales and offsets the wave to run between -1 and 1, rather than 0-1. |
| **Sine Phase** (StaticBool) | Setting this *true* will output normal sine behavior rather than linear behavior. |
| Outputs |   |
| **Linear Sine** | This outputs a linear sine wave. |
| **Rounded Linear Sine** | Outputs a linear sine with rounded edges. |
| **Direction** | Outputs 0 or 1, depending on whether the sine wave is traveling downward (0) or upward (1). |

## VectorToRadialValue

The **VectorToRadialValue** function transforms the vector of a Vector2 into an angle, or transforms UV coordinate data into radial coordinates. In the case of a vector, the angle will output in one channel and the length of the vector in the other.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Vector or UVs (Vector2)** | Takes in either a Vector2 or a set of UV coordinates. |
| **Swizzle Coordinate Output (StaticBool)** | Flips the U and V components of the output. |
| Outputs |   |
| **Radial Coordinates** | Returns the radial coordinates of the input. In the case of a vector, the angle is on one channel and the distance is on the other. |
| **Vector Converted to Angle** | Returns the angle of the input vector or a radial gradient in the case of UVs. |
| **Linear Distance** | Returns the linear length of the input vector, or in the case of UVs, outputs a radial gradient of distances. |

![Vector To Radial Value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfb30aa9-0b8b-4dff-8380-2de2b0e2d230/vector-to-radial.png)