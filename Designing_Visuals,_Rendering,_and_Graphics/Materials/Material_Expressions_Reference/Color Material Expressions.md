# Color Material Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/color-material-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-material-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:13

---

## Desaturation

The **Desaturation** expression desaturates its input, or converts the colors of its input into shades of gray, based a certain percentage.

| Item | Description |
| --- | --- |
| Properties |   |
| **Luminance Factors** | Specifies the amount that each channel contributes to the desaturated color. This is what controls that green is brighter than red which is brighter than blue when desaturated. |
| Inputs |   |
| **Fraction** | Specifies the amount of desaturation to apply to the input. Percent can range from 0.0(full original color, no desaturation) to 1.0 (fully desaturated). |

![Desaturation Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ad1fbd4-8664-4433-a111-139b49d20aea/desaturation-expression.png)

**Programmers:** Define desaturated color `D`, input color `I` and luminance factor `L`. The output will be `O = (1 - Percent)*( D.dot( I )) + Percent * I`