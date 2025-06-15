# Flipbook Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/flipbook-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/flipbook-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:53

---

**Flipbook Components** are regular primitive components, and can be posed arbitrarily in 3D, attached to other components, or have other components attached to them. Each Flipbook Component instance can specify a custom color that will be passed down to the Flipbook Material as a Vertex Color. They can also have a custom Material specified that will override the default Material defined in the Flipbook.

You can change the current Flipbook asset by calling **SetFlipbook**, but note that this will only work if the **Mobility** property is set to **Moveable** (or if it is called during the construction of the Actor). You can also control play rate, play direction, looping, etc. with various other methods on the component.

While C++ documentation for working with Flipbook Components is still in development, you can refer to [UPaperFlipbookComponent](/documentation/404) for more information on using them in your code until more detailed documentation comes online.

## Setup

To learn more about Flipbook Components using Blueprints, follow the link below:

-   [Paper 2D Flipbooks](/documentation/en-us/unreal-engine/paper-2d-flipbooks-in-unreal-engine)