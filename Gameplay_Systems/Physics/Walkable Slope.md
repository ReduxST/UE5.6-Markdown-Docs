# Walkable Slope

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/walkable-slope-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/walkable-slope-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:55

---

The **Walkable Slope Override** on **Physics Bodies** enables you to tweak what surfaces **Characters** can walk up. Perhaps a staircase is too steep or maybe you want to enforce the "no walking on the grass" signs, these settings will enable you to do so.

## Usage

The **Character Movement Component** has a property called **Walkable Floor Angle**. It defaults to around 45 degrees. So, when the Character attempts to move across a surface that is angled higher than this, the Character will not be able to climb the incline or will lose their footing and slide down it.

Depending on the editor you are in, or if you are looking at an Actor in the level, you will find a property, or expandable grouping of properties, prefixed with **Override Walkable Slope**. Here you can set the **Walkable Slope Behavior** and **Walkable Slope Angle**.

![Override Walkable Slope](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b035d1c-a93f-4ee9-a86b-a49ea6bbc696/walkable-properties.png)

### Increase Walkable Slope

This setting will increase the walkable slope of a **Physics Body** up to the value listed in the **Walkable Slope Angle** property. If **Walkable Slope Angle** is set to 75, and the angle of the surface of the **Physics Body** is 65, the Character will be able to walk up to it, regardless of the Character's **Walkable Floor Angle**.

While **Walkable Slope Behavior** is set to "Increase Walkable Slope":

-   A value of 0.0 in the **Walkable Slope Angle** is essentially the same as **No Change** in the **Walkable Slope Behavior** property.
-   A value of 90.0 in the **Walkable Slope Angle** will allow the character to traverse any angle on the Physics Body up to (but not including) 90 degrees.

### Decrease Walkable Slope

This setting will "cap" the walkable slope of a **Physics Body** to the value listed in the **Walkable Slope Angle** property. If **Walkable Slope Angle** is set to 25, and the angle of the surface of the **Physics Body** is 35 degrees, the Character will be unable to walk up to it regardless of the Character's **Walkable Floor Angle**.

While **Walkable Slope Behavior** is set to "Decrease Walkable Slope":

-   A value of 0.0 in the **Walkable Slope Angle** will result in the Character being unable to walk across the **Physics Body** surface. This can result in some odd behavior for mostly flat surfaces, as the character will skate across them but will not be able to change direction.
-   A value of 90.0 in the **Walkable Slope Angle** is essentially the same as **No Change** in the **Walkable Slope Behavior** property.

## Examples

|   |   |
| --- | --- |
| ![The blue angle is the default Character Movement Component Walkable Floor Angle and the green represents the new Increased Walkable Slope angle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3469afe0-3166-4771-8e45-e784f945176f/increased-1.png) | ![The blue angle is the default Character Movement Component Walkable Floor Angle and the red represents the new Decreased Walkable Slope angle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbb83cac-5ff7-4855-b298-34845ae107aa/decreased-1.png) |
| The blue angle is the default **Character Movement Component Walkable Floor Angle**, while the green represents the new **Increased Walkable Slope** angle. | The blue angle is the default **Character Movement Component Walkable Floor Angle**, while the red represents the new **Decreased Walkable Slope** angle. |