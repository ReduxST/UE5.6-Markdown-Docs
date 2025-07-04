# Applying 2D Physics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-physics-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-physics-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:51

---

This page provides an example of applying physics to sprites in 2D games.

*For this example we are using a 2D Side Scroller Game, however you can apply the same concepts to any 2D game.*

When using physics in any 2D style game, typically you'll want to apply some constraints to your sprite when physics are applied to prevent the sprite from moving or rotating in such a way that the card becomes visible to the player, or even worse, falls out of your game world as seen in the example below.

Above, we have applied physics to a sprite but have not applied any constraints to those physics so our object that falls and applies physics actually tumbles outside of our game world and off screen which is not what we want. We want our physics object to react to the world and player interaction, however we want to keep it inside our level and prevent it from rotating on certain axis so that the sprite is always fully visible.

For our sprite, we can apply constraints from the **Details** panel in addition to applying physics.

1.  Select the Sprite in your level that you want to apply physics to.
    
2.  In the **Details** panel, click the **Simulate Physics** option under *Physics*.
    
3.  Expand *Constraints* and choose the **Lock Position** (typically to the **Y** axis for side scrolling games).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54984eb7-d257-486d-81b4-760b57b8a26d/constraints1.png)
    
    While this will apply physics and lock it to only the Y axis, there are additional issues that may occur with just this setting.
    
    Our sprite is now locked to the Y axis, however you can see that it can still rotate freely which may not be what we want.
    
4.  Also in the *Constraints* section, choose a **Lock Rotation** (typically to the **X** axis for side scrolling games).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6577944-079a-4a8f-a710-c7fa2a38b1c5/constraints3.png)
    
    Now when physics is applied to the sprite its position is locked to the Y and its rotation is locked at the X.
    
    You can also use the **Mode** option to constrain movement along a specified axis (in this case **XZPlane** to achieve the same effect).
    

Depending upon the type of 2D game you are making, varying settings can be used to restrict how physics are applied to your object.