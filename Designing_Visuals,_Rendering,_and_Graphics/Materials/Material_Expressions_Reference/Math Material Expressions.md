# Math Material Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:20

---

## Abs

**Abs** is an abbreviation for the mathematical term "absolute value". The Abs expression outputs the absolute, or unsigned, value of the input it receives. Essentially, this means it turns negative numbers into positive numbers by dropping the minus sign, while positive numbers and zero remain unchanged.

**Examples:** Abs of -0.7 is 0.7; Abs of -1.0 is 1.0; Abs of 1.0 is also 1.0

**Example Usage:** Abs is commonly used with Dot Product to determine the angular relationship between two vectors: whether they are parallel, perpendicular, or somewhere in between. Normally, when you get the dot product of two vectors, the value is interpolated between 1.0 (for two parallel vectors) and -1.0 (for two exactly opposite vectors), with the midpoint of 0 indicating that the two vectors are perpendicular. When you take the absolute value of this dot product, the positive values remain unchanged, but the negative values are converted into positive numbers by dropping the minus sign. The result is therefore interpolated between 0 (for perpendicular vectors) and 1.0 (for parallel vectors, regardless of whether the vectors point in the same direction or opposite directions). This tells you simply how far the two vectors are from being orthogonal.

![Absolute value Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b29e8e52-261b-4313-96b6-615523906aad/abs.png)

## Add

The **Add** expression takes two inputs, adds them together, and outputs the result. 

If you pass values with multiple channels, each channel is added separately. For example, if you pass RGB color values to each input, the R channel of the first input is added to the R channel of the second input and the result is stored in the R channel of the output; the G channel of the first input is added to the G channel of the second input and the result is stored in the G channel of the output, and so on.

Both inputs must have the same number of values, unless one of the values is a single Constant value. In that case, each channel of the multi-channeled input is added to the single float value, and the result is stored in a separate channel of the output value.

| Property | Description |
| --- | --- |
| **Const A** | Takes in the value(s) to add to. Only used if the A input is not used. |
| **Const B** | Takes in the value(s) to be added. Only used if the B input is not used. |
| Inputs |   |
| **A** | Takes in the value(s) to add to. |
| **B** | Takes in the value(s) to be added. |

**Examples:** Add of 0.2 and 0.4 is 0.6; Add of (0.2,-0.4,0.6) and (0.1,0.5,1.0) is (0.3,0.1,1.6); Add of (0.2,-0.4,0.6) and 1.0 is (1.2,0.6,1.6)

**Example Usage:** Add is often used to brighten/darken colors or to offset UV texture coordinates.

![Add Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e1fe730-4806-46f8-9726-b18a76732a66/add.png)

## AppendVector

The **AppendVector** expression enables you to combine channels together to create a vector with more channels than the original. For example, you can take two individual **Constant** values and append them to make a two-channel **Constant2 Vector** value. This can be useful for reordering the channels within a single texture or for combining multiple grayscale textures into one RGB color texture.

| Input | Description |
| --- | --- |
| **A** | Takes in the value(s) to append to. |
| **B** | Takes in the value(s) to be appended. |

**Examples:** Append of 0.2 and 0.4 is (0.2,0.4); Append of (0.2,0.4) and (1.0) is (0.2,0.4,1.0).

![AppendVector Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bf7e4e6-d253-4bf4-96be-443773d80408/appendvectorexample.png)

## Arccosine

The **Arccosine** expression outputs the inverse cosine function.

This is an expensive operation that is not reflected by the instruction count. Use [ArccosineFast](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arccosinefast) for a faster but less accurate alternative.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b308526-e300-4fad-8b0a-aefdd4c7df96/men_arccosine.png)

The image above shows two different visualizations of the result of applying this expression:

-   The top bar shows the result as an output color. The left end of the bar shows the color that results from using this expression on an input value of -1, and the right end of the bar shows the results for a value of 1.
    
-   In the graph, the X axis represents input values ranging from -1 to 1. The Y axis shows the results of using this expression on those input values, again ranging from -1 to 1.
    

## ArccosineFast

The **ArccosineFast** expression outputs an approximation of the inverse cosine function that is faster to calculate than the more accurate [Arccosine](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arccosine) expression. Input must be between -1 and 1.

See the **Arccosine** expression above for a visualization of the output values.

## Arcsine

The **Arcsine** expression outputs the inverse sine function.

This is an expensive operation that is not reflected by the instruction count. Use [ArcsineFast](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arcsinefast) for a faster but less accurate alternative.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc205984-6046-4c7d-8eec-74deef90e9ed/men_arcsine.png)

The image above shows two different visualizations of the result of applying this expression:

-   The top bar shows the result as an output color. The left end of the bar shows the color that results from using this expression on an input value of -1, and the right end of the bar shows the results for a value of 1.
    
-   In the graph, the X axis represents input values ranging from -1 to 1. The Y axis shows the results of using this expression on those input values, again ranging from -1 to 1.
    

## ArcsineFast

The **ArcsineFast** expression outputs an approximation of the inverse sine function that is faster to calculate than the more accurate [Arcsine](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arcsine) expression. Input must be between -1 and 1.

See the **Arcsine** expression above for a visualization of the output values.

## Arctangent

The **Arctangent** expression outputs the inverse tangent function.

This is an expensive operation that is not reflected by the instruction count. Use [ArctangentFast](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arctangentfast) for a faster but less accurate alternative.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76afd95b-b07b-46c7-893c-2b70a746e664/men_arctangent.png)

The image above shows two different visualizations of the result of applying this expression:

-   The top bar shows the result as an output color. The left end of the bar shows the color that results from using this expression on an input value of -1, and the right end of the bar shows the results for a value of 1.
    
-   In the graph, the X axis represents input values ranging from -1 to 1. The Y axis shows the results of using this expression on those input values, again ranging from -1 to 1.
    

## Arctangent2

The **Arctangent2** expression outputs the inverse tangent of x / y where input signs are used to determine quadrant.

This is an expensive operation that is not reflected by the instruction count. Use Arctangent2Fast for a faster but less accurate alternative.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95b2dc8b-e039-458b-9a73-18e247e2b9b8/men_arctangent2.png)

The image above shows two different visualizations of the result of applying this expression:

-   The top bar shows the result as an output color. The left end of the bar shows the color that results from using this expression on an input value of -1, and the right end of the bar shows the results for a value of 1.
    
-   In the graph, the X axis represents input values ranging from -1 to 1. The Y axis shows the results of using this expression on those input values, again ranging from -1 to 1.
    

## Arctangent2Fast

The **Arctangent2Fast** expression outputs an approximation of the inverse tangent of X / Y where input signs are used to determine quadrant. It is faster to calculate but less accurate than the [Arctangent2](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arctangent2) expression.

See the **Arctangent2** expression above for a visualization of the output values.

## ArctangentFast

The **ArctangentFast** expression outputs an approximation of the inverse tangent function that is faster to calculate than the more accurate [Arctangent](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#arctangent) expression.

See the **Arctangent** expression above for a visualization of the output values.

## Ceil

The **Ceil** expression takes in value(s), rounds them **up** to the next integer, and outputs the result. See also [Floor](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#floor) and [Frac](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#frac).

**Examples:** Ceil of 0.2 is 1.0; Ceil of (0.2,1.6) is (1.0,2.0).

![Ceil Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0754a053-8f53-49c0-941c-fe48dd327e49/ceil.png)

## Clamp

The **Clamp** expression takes in value(s) and constrains them to a specified range, defined by a minimum and maximum value. A minimum value of 0.0 and maximum value of 0.5 means that the resulting value(s) will never be less than 0.0 and never greater than 0.5.

  

| Property | Description |
| --- | --- |
| **Clamp Mode** | Selects the type of clamp to be used. CMODE\_Clamp will clamp both ends of the range. CMODE\_ClampMin and CMODE\_ClampMax will only clamp their respective ends of the range. |
| **Min Default** | Takes in the value to use as the minimum when clamping. Only used when the Min input is unused. |
| **Max Default** | Takes in the value to use as the maximum when clamping. Only used when the Max input is unused. |
| Inputs |   |
| **Min** | Takes in the value to use as the minimum when clamping. |
| **Max** | Takes in the value to use as the maximum when clamping. |

**Examples:** Clamping an input range of (0.0) to (1.0) 0.3 with Min 0.0 and Max 1.0 yields 0.3; Clamping 1.3 with Min 0.0 and Max 1.0 yields 1.0.

![Clamp Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7911cce4-15df-4876-8865-b70536e64890/clamp.png)

## ComponentMask

The **ComponentMask** expression enables you to select a specific subset of channels (R, G, B, and/or A) from the input to pass through to the output. Attempting to pass a channel through that does not exist in the input will cause an error, unless the input is a single constant value. In that case, the single value is passed through to each channel. The current channels selected to be passed through are displayed in the title bar of the expression.

| Property | Description |
| --- | --- |
| **R** | If checked, the red (first) channel of the input value will be passed through to the output. |
| **G** | If checked, the green (second) channel of the input value will be passed through to the output. |
| **B** | If checked, the blue (third) channel of the input value will be passed through to the output. |
| **A** | If checked, the alpha (fourth) channel of the input value will be passed through to the output. |

**Examples:** ComponentMask with an input of (0.2,0.4,1.0) and the G channel will produce an output of (0.4), which appears as a 40% bright grayscale value when used as a color vector.

![Component Mask Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/421e0807-bafe-454a-9136-350936fd47c0/componentmaskexample.png)

## Cosine

The **Cosine** expression outputs the value of a cosine wave over the input range of \[0, 1\] and the output range of \[-1, 1\], both repeating. Most commonly, this is used to output a continuous oscillating waveform by connecting a **Time** expression to its input, but it can also be used to create ripples in worldspace or screenspace, or any other application where a continuous, smooth cycle is needed. A visual representation of the wave is shown below, scaled to the \[0, 1\] output range:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dad69dc5-cedf-41ee-859f-97acde92685b/cosinewave.png)  

| Property | Description |
| --- | --- |
| **Period** | Specifies the period of the resultant wave. In other words, this is how long one full oscillation takes to occur, or the time between each successive crest or each successive trough in the waveform. For example, in the image above, the period is one second. |

**Example Usage:** This expression is useful anytime an oscillating effect is needed. The speed and amplitude of the oscillation can easily be controlled dynamically by multiplying the time input (speed) or the output (amplitude).

In the example above, the color would oscillate with co-sinusoidal frequency.

## CrossProduct

The **CrossProduct** expression computes the cross product of two three-channel vector value inputs and outputs the resulting three-channel vector value. Given two vectors in space, the cross product is a vector that is perpendicular to both of the inputs.

  

| Input | Description |
| --- | --- |
| **A** | Takes in a three-channel vector value. |
| **B** | Takes in a three-channel vector value. |

**Example Usage:** CrossProduct is often used to compute directions which are perpendicular to two other directions.

![Cross product example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/996db38d-0956-4f5c-8084-64358d5631e9/cross-product.png)

## Divide

The **Divide** expression takes two inputs, divides the first input by the second, and outputs the result.

If you pass values with multiple channels, each channel is divided separately. For example, if you pass RGB color values to each input, the R channel of the first input is divided by the R channel of the second input and the result is stored in the R channel of the output; the G channel of the first input is divided by the G channel of the second input and the result is stored in the G channel of the output, and so on.

Both inputs must have the same number of values, unless one of the values is a single float value. In that case, each channel of the multi-channeled input is divided by the single float value, and the result is stored in a separate channel of the output value.

If the divisor is between 0 and 0.00001 in any channel, it is raised to 0.00001. If the divisor is between 0 and -0.00001 in any channel, it is lowered to -0.00001. This avoids the possibility of division by zero errors. However, it also means that the output value for the channel may be very large.

  

| Property | Description |
| --- | --- |
| **Const A** | Takes in the value(s) to be divided, the dividend. Only used if the A input is unused. |
| **Const B** | Takes in the value(s) to divide by, the divisor. Only used if the B input is unused. |
| Inputs |   |
| **A** | Takes in the value(s) to be divided, the dividend. |
| **B** | Takes in the value(s) to divide by, the divisor. |

**Examples:** Using Divide with A=(1.0) and B=(5.0) outputs (0.2), which appears as a dark gray.

![Divide Material Expression example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffc4a396-138d-4819-82a6-b3b852d51e2a/divide.png)

## DotProduct

The **DotProduct** expression computes the dot product, which can be described as the length of one vector projected onto the other, or as the cosine between the two vectors multiplied by their magnitudes. This calculation is used by many techniques for computing falloff. DotProduct requires both vector inputs to have the same number of channels.

  

| Input | Description |
| --- | --- |
| **A** | Takes in a value or vector of any length. |
| **B** | Takes in a value or vector of the same length as **A**. |

![Dot product Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cb43f82-db9d-428c-8aef-15d7a06ef4e0/dot-product.png)

## Floor

The **Floor** expression takes in value(s), rounds them **down** to the previous integer, and outputs the result. See also [Ceil](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#ceil) and [Frac](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#frac).

**Examples:** Floor of 0.2 is 0.0; Floor of (0.2,1.6) is (0.0, 1.0).

![Floor Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f5cb52e-c713-473e-8a8a-fd600a8f49cd/floor.png)

## Fmod

The **Fmod** expression returns the floating-point remainder of the division operation of the two inputs. The Dividend (input "A") can be any value, but negative Dividends will result in negative results. The Divisor (second input) should not be zero as this implies a division by zero, but whether the Divisor is negative or positive will not affect the result. A common use case is to make a material that brightens up to a maximum value, then immediately drops back to the minimum value on the next frame, only to begin climbing toward the maximum again.

In this example, FMod takes a zero-to-one UV progression and converts it into a repeating cycle every 0.2 UV units on the X axis in the green channel.

## Frac

The **Frac** expression takes in values and outputs the fractional portion of those values. In other words, for an input value "X", the result is "X minus Floor of X". The output value will range from zero to one, inclusive on the low end, but not the high end. See also [Ceil](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#ceil) and [Floor](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#floor).

**Examples:** Frac of (0.2) is (0.2). Frac of (-0.2) is (0.8). Frac of (0.0,1.6,1.0) is (0.0,0.6,0.0).

![Frac Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc763392-904b-43d0-b235-4b233fdec4ae/frac.png)

In this example, the Frac node is converting time into a series of repeating 0 - 1 progressions, causing the color to fade (via the Lerp) from green to red, then snap back to green, repeating indefinitely.

## If

The **If** expression compares two inputs and then passes through one of three other input values based on the result of the comparison. Both compared inputs must be single float values.

  

| Input | Description |
| --- | --- |
| **A** | Takes in a single float value. |
| **B** | Takes in a single float value. |
| **A > B** | Takes in the value(s) to output if the value of A is greater than the value of B. |
| **A = B** | Takes in the value(s) to output if the value of A is equal to the value of B. |
| **A < B** | Takes in the value(s) to output if the value of A is less than the value of B. |

![If Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f72f8a-3785-478b-81cd-a5f1dd9b98c8/if.png)

In this example, the If expression takes in a heightmap and outputs either red or green based on whether the height falls under or over a value of 0.45.

## LinearInterpolate

The **LinearInterpolate** expression blends between two input value(s) based on a third input value used as a mask. This can be thought of as a mask to define transitions between two textures, like a layer mask in Photoshop. The intensity of the mask Alpha determines the ratio of color to take from the two input values. If Alpha is 0.0, the first input is used. If Alpha is 1.0, the second input is used. If Alpha is between 0.0 and 1.0, the output is a blend between the two inputs. Keep in mind that the blend happens per channel. So, if Alpha is an RGB color, Alpha's red channel value defines the blend between A and B's red channels **independently** of Alpha's green channel, which defines the blend between A and B's green channels.

| Property | Description |
| --- | --- |
| **Const A** | The value mapped to 0.0. Only used if the A input is unconnected. |
| **Const B** | The value mapped to 1.0. Only used if the B input is unconnected. |
| **Const Alpha** | Takes in the value to use as the mask alpha. Only used if the Alpha input is unconnected. |
| Inputs |   |
| **A** | Takes in the value(s) mapped to 0.0. |
| **B** | Takes in the value(s) mapped to 1.0. |
| **Alpha** | Takes in the value to use as the mask alpha. |

**Programmers:** LinearInterpolate does a per-channel lerp between A and B based on the parametric value Alpha.

![Linear Interpolate example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f34194c-db62-479c-b6cb-53773e046d90/lerpexample.png)

## Logarithm10

The **Logarithm10** node returns the base-10 logarithm, also called the common logarithm, of the input value. That is, if you take a base value of 10 and raise it to the power of the number returned by this expression, you would get the input value.

Only use positive input values for this expression.

## Logarithm2

The Logarithm2 node returns the base-2 logarithm of the input value. That is, if you take a base value of 2 and raise it to the power of the number returned by this expression, you would get the input value.

Only use positive input values for this expression.

## Max

The **Max** expression takes in two inputs and outputs the higher of the two.

When you use this node with color inputs, the result is similar to the **Lighten** layer blending mode in Photoshop.

![Max Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d540a746-5a79-4295-9903-8ee8978f1430/max.png)

In the example above, A is "0" and B is "1"; therefore, "1" (white) is the resulting base color.

  

| Property | Description |
| --- | --- |
| **Const A** | Takes in the first value(s). Used only if the A input is unused. |
| **Const B** | Takes in the second value(s). Used only if the B input is unused. |
| Inputs |   |
| **A** | Takes in the first value(s) to compare. |
| **B** | Takes in the second value(s) to compare. |

## Min

The **Min** expression takes in two inputs and outputs the lower of the two.

When you use this node with color inputs, the result is similar to using the **Darken** layer blending mode in Photoshop.

![Min Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/434928bc-4e4b-44f4-afa0-fef6118be6d9/min.png)

In the example above, A is "0" and B is "1"; therefore, "0" (black) is the resulting base color.

  

| Property | Description |
| --- | --- |
| **Const A** | Takes in the first value(s). Used only if the A input is unused. |
| **Const B** | Takes in the second value(s). Used only if the B input is unused. |
| Inputs |   |
| **A** | Takes in the first value(s) to compare. |
| **B** | Takes in the second value(s) to compare. |

## Multiply

The **Multiply** expression takes two inputs, multiplies them together, and outputs the result. When you pass color values as input, the results are similar to the results of the **Multiply** layer blending mode in Photoshop.

If you pass values with multiple channels, each channel is multiplied separately. For example, if you pass RGB color values to each input, the R channel of the first input is multiplied by the R channel of the second input and the result is stored in the R channel of the output; the G channel of the first input is multiplied by the G channel of the second input and the result is stored in the G channel of the output, and so on.

Both inputs must have the same number of values, unless one of the values is a single float value. In that case, each channel of the multi-channeled input is multiplied by the single float value, and stored in a separate channel of the output value.

  

| Property | Description |
| --- | --- |
| **Const A** | Takes in the first value(s) to multiply. Used only if the A input is unused. |
| **Const B** | Takes in the second value(s) to multiply. Used only if the B input is unused. |
| Inputs |   |
| **A** | Takes in the first value(s) to multiply. |
| **B** | Takes in the second value(s) to multiply. |

Do not forget that Materials in Unreal Engine are not limited to \[0,1\]. If colors/values are greater than 1, Multiply will actually brighten colors.

**Examples:** Multiply of 0.4 and 0.5 is 0.2; Multiply of (0.2,-0.4,0.6) and (0.0,2.0,1.0) is (0.0,-0.8,0.6); Multiply of (0.2,-0.4,0.6) and 0.5 is (0.1,-0.2,0.3).

**Example Usage:** Multiply is often used to brighten or darken colors/textures, or manipulate the UVs of a texture.

 ![Multiply example start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2b60421-a26c-4214-918b-5ce7930ad405/mult-01.png) ![Multiply example end](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7956d6a-afb0-4fef-8b4b-819214050a8a/mult-02.png)

**Note how texture scale changes when the UVs are multiplied by one and then two.**

## Normalize

The **Normalize** expression calculates and outputs the normalized value of its input. Normalized vectors (also called "unit vectors") have an overall length of 1.0. This means each component of the input is divided by the total magnitude (length) of the vector.

**Examples:** Passing either (0,2,0) or (0,0.2,0) through Normalize will output (0,1,0). Passing (0,1,-1) through Normalize will output (0, 0.707, -0.707). The only special case is an all-zero vector, which will be unchanged.

![Normalized Input Vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3305de08-965f-49d6-b823-a1bc1fa01622/normalizeexample.png)

![Non-Normalized Input Vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b592d1a-e274-4883-a552-394e7e50b2e9/normalizeexample2.png)

It is not necessary to normalize an expression that plugs into the Normal material output.

## OneMinus

The **OneMinus** expression takes an input value "X" and outputs "One Minus X". This operation is performed per channel.

**Examples:** OneMinus of 0.4 is 0.6; OneMinus of (0.2,0.5,1.0) is (0.8,0.5,0.0); OneMinus of (0.0,-0.4,1.6) is (1.0,1.4,-0.6).

**Example Usage:** When the input colors are in the range \[0,1\], OneMinus has the same effect as what is commonly called "invert" -- that is, OneMinus returns the complementary color that when added to the input will produce white.

 ![OneMinus Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa44e5a0-1edc-44fe-b7d6-809c67bddd6b/oneminus-01.png) ![OneMinus End](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40d4b7b2-0637-44c7-b913-7bf905c7d3a5/oneminus-02.png)

**Adding a OneMinus node inverts the values in the Texture Sample.**

## Power

The **Power** expression takes two inputs: a base value (**Base**) and an exponent (**Exp**). It raises the base value to the power of the exponent and outputs the result. In other words, it returns **Base** multiplied by itself **Exp** times.

  

| Property | Description |
| --- | --- |
| **Const Exponent** | Takes in the exponent value. Used only if the Exp input is unused. |
| Inputs |   |
| **Base** | Takes in the base value. |
| **Exp** | Takes in the exponent value. |

**Examples:** Power of Base 0.5, Exp 2.0 is 0.25.

**Example Usage:** If the colors you pass to Power are in \[0,1\], Power can behave as a sort of contrast adjustment, where very bright values are dimmed slightly, but darker values are decreased drastically.

 ![Power Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad30ab6a-5d6f-4fd9-8bf3-a3430e8ca91a/power-01.png) ![Power End](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/470cc89b-48dd-4648-a449-f1723dd29a46/power-02.png)

**Adding a Power node increases the contrast in the Texture Sample.**

## Round

The **Round** expression rounds the input value to the nearest whole number. If the fractional part of the input value is 0.5 or greater, then the output value is rounded up. Otherwise, the output value is rounded down.

![Before Round](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bafd71b9-42ae-4a36-ba7d-e28ccfff55f9/roundexample_00.png)

![After Round](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f7a5638-8e57-48da-b037-c1d4d37a04e9/roundexample_01.png)

**Examples:**

-   A value of 1.1 will be rounded down to a value of 1.
-   A value of 1.4 will be rounded down to a value of 1.
-   A value of 1.5 will be rounded up to a value of 2.
-   A value of 1.85 will be rounded up to a value of 2.

## Saturate

The **Saturate** node clamps the value between 0 and 1. Values less than 0 are raised to 0; values greater than 1 are lowered to 1; values between 0 and 1 inclusive remain unchanged. The instruction cost of Saturate is almost free on most modern graphics hardware, so you can use this node any time you need to clamp an input or output value between 0 and 1 without effect on your material's performance.

![Saturate Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b81a6bf-c344-493e-8b6a-cf85bc45ccd1/saturate.png)

**Example Usage:** This node should be used whenever you need to clamp an output or input value between 0 and 1.

## Step

The Step Material Expression returns 0 or 1 for every value of X, depending on whether it is greater than or less than the reference value in Y.

Below, a linear gradient (0 to 1) is plugged into the X input. The value in Y (0.25) acts as the reference value. Every value on the gradient below 0.25 on the returns a 0 (black), every value greater than or equal to 0.25 returns a 1 (white).

  ![Step example 01](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/551162d1-695b-4b51-9e25-607c2af91c68/step-01.png) ![Step example 01](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42d580e4-ed20-4b50-b478-9449229650be/step-02.png) ![Step example 01](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4817ddb-305d-41b0-be31-1bc8952ea001/step-03.png)

**Note that the threshold between black and white moves when you increase the value in Y .**

The Step expression is useful when an abrupt on/off effect is needed. For example, you could also use a Step expression to simplify a grayscale texture into a black and white mask.

## SmoothStep

SmoothStep lets you interpolate between 0 and 1 for values between a Min and Max threshold. SmoothStep takes three arguments:

-   **Min** defines the lower edge of the interpolation. SmoothStep returns 0 (black) for values less than or equal to Min.
-   **Max** defines the upper edge of the interpolation. Smoothstep returns 1 (white) for values greater than or equal to Max.
-   **Value** defines the source value(s) for interpolation. For example, a gradient or a grayscale texture map.

This expression is useful for transitions where you want the edge to have some degree of smoothness.

Below a LinearGradient is passed into the Value input, and the Min and Max values are set at 0.1 and 0.9. This results in a relatively smooth gradient where 0.1 is black and 0.9 is white.

 ![SmoothStep example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ac6bc6b-94f8-4cb2-a70b-38f51979e7c2/smoothstep-01.png) ![SmoothStep Example 02](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c511dd5-e10b-4b7a-9c31-8faf2d63ef36/smoothstep-02.png)

**The Min and Max values control where interpolation begins and ends.**

On the second slide, the Min and Max are set to 0.6 and 0.8, resulting in a much more abrupt transition. Everything below 0.6 is black, everything above 0.8 is white, with a smooth gradient in between.

## Sign

The **Sign** node indicates whether a numeric input is negative, positive, or exactly 0.

-   If the input is negative, this node outputs -1.
-   If the input is exactly 0, this node outputs 0.
-   If the input is positive, this node outputs 1.

## Sine

The **Sine** expression outputs the value of a Sine wave over the input range of \[0, 1\] and the output range of \[-1, 1\], both repeating. The difference between this and the output of the [Cosine](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#cosine) expression is the output waveform is offset by one-quarter of the period, meaning that `Cos(X)` is equal to `Sin(X + 0.25)`. Most commonly, this is used to output a continuous oscillating waveform by connecting a **Time**expression to its input, but it can also be used to create ripples in worldspace or screenspace, or any other application where a continuous, smooth cycle is needed. A visual representation of the wave is shown below, scaled to the \[0, 1\] output range:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b243c13f-a20e-4817-8198-b662018d5d0b/sinewave.png)  

| Property | Description |
| --- | --- |
| **Period** | Specifies the period of the resultant wave. In other words, this is how long one full oscillation takes to occur, or the time between each successive crest or each successive trough in the waveform. For example, in the image above, the period is one second. |

**Example Usage:** This expression is useful anytime an oscillating effect is needed. The speed and amplitude of the oscillation can easily be controlled dynamically by multiplying the time input (speed) or the output (amplitude).

## SquareRoot

The **SquareRoot** expression outputs the square root of the input value. If applied to a vector, each component will be handled individually.

For textures in the 0 to 1 range, this reduces the apparent contrast of the image. For example, on the calibration texture below, dark values become brighter and white values shift toward gray.

![Square Root Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0534c87e-9081-4214-96f4-0b3469c5a29b/square-root.png)

## Subtract

The **Subtract** node takes in two inputs, subtracts the second input from the first, and outputs the difference.

If you pass values with multiple channels, each channel is subtracted separately. For example, if you pass RGB color values to each input, the R channel of the second input is subtracted from the R channel of the first input and the result is stored in the R channel of the output; the G channel of the second input is subtracted from the G channel of the first input and the result is stored in the G channel of the output, and so on.

Both inputs must have the same number of values, unless one of the values is a single Constant value. In that case, each channel of the multi-channel input has the Constant value subtracted from it, and the result stored in a separate channel of the output value.

  

| Property | Description |
| --- | --- |
| **Const A** | Takes in the value(s) of the minuend. Used only if the A input is unused. |
| **Const B** | Takes in the value(s) of the subtrahend. Used only if the B input is unused. |
| Inputs |   |
| **A** | Takes in the value(s) of the minuend. |
| **B** | Takes in the value(s) of the subtrahend. |

**Examples:** Subtract of 0.5 and 0.2 is 0.3; Subtract of (0.2,-0.4,0.6) and (0.1,0.1,1.0) is (0.1,-0.5,-0.4); Subtract of (0.2,0.4,1.0) and 0.2 is (0.0,0.2,0.8).

**Example Usage:** Subtract can be used to darken colors and offset UVs.

![Subtract Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/caea5a63-2fc6-450a-865e-b4cb2d03d124/subtract.png)

## Tangent

The **Tangent** node outputs the tangent of the specified value.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aeace5f-b20a-49f3-8c79-5477f698a715/men_tangent.png)

The image above shows two different visualizations of the result of applying this expression:

-   The top bar shows the result as an output color. The left end of the bar shows the color that results from using this expression on an input value of -1, and the right end of the bar shows the results for a value of 1.
-   In the graph, the X axis represents input values ranging from -1 to 1. The Y axis shows the results of using this expression on those input values, again ranging from -1 to 1.

## Truncate

![Before Truncate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc897c1e-d0c1-4b23-9fc5-ee26768ee6ba/truncateexample_00.png)

![After Truncate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/109020d2-a7e1-4785-83ad-8054da4fcce0/truncateexample_01.png)

The **Truncate** node truncates a value by discarding the fractional part while leaving the whole number untouched.

**Examples:**

-   An input value of 1.1 will be truncated to 1.
-   An input value of 1.4 will be truncated to 1.
-   An input value of 2.5 will be truncated to 2.
-   An input value of 3.1 will be truncated to 3.