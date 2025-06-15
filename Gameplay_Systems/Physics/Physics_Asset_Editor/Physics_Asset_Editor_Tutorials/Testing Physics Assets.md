# Testing Physics Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-physics-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-physics-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:52

---

This page covers the basics of testing a **Physics Asset** in the **Physics Asset Tool**.

## Testing

![Testing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a3d1ba6-e983-4fdf-8805-9bc38de91d60/simulate-options.png)

Selecting **Simulation** from the dropdown menu under the toolbar **arrow icon** will allow you to test your Physics Asset.

![Selecting Simulation from the dropdown menu under the toolbar arrow icon will allow you to test your Physics Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a8d59bc-894f-4b9a-a92c-3fd942607027/simulation-physics-asset.png)

-   When the **No Gravity** option is enabled, the entire Physics Asset is simulated but gravity is not turned on, enabling you to ctrl+click to poke the **Physics Bodies** in a zero gravity environment. This is useful for finding any interpenetrating Physics Bodies or **Limited Physics Constraints** already outside of their limits.
    
-   You can also simulate a chain of joints by toggling on **Selected Simulation**. This option only simulates the Physics Bodies you have selected (you can select more than one) and those down the hierarchy from the selected Physics Bodies. For example, if you select the shoulder, the entire arm will be simulated.