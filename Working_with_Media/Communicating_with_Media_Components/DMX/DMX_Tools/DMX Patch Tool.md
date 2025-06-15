# DMX Patch Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-patch-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-patch-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:05

---

The **DMX Patch tool** provides you a way to quickly set the DMX library and patch of a given selection of actors within the **World Outliner**.

A DMX library is the main data structure that holds information in regards to:

-   Controllers
-   Fixture types
-   Fixture patches

A DMX patch tracks DMX addresses, and assigns the patching of DMX-enabled fixtures.

The DMX Patch tool offers 3 functionalities:

-   Address incremental
-   Address same
-   Address and rename

![The three options available for the patch tool.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfad63fd-1d28-44a3-bd27-c6c40fc691e2/quick-patch-options.png)

## Address incremental

-   Applies the selected DMX library to all selected actors.
-   Applies patches incrementally starting from the provided fixture patch.

![Using the address incremental option.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1d7293c-735c-46c2-a48f-d3ba4b40a175/address-incremental.png)

## Address same

-   Applies the selected DMX library to all selected actors.
-   Applies the same patch to all selected actors.

![Using the address same option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8e7cc19-6fc6-438e-81f6-8fff4a6cbf01/address-same.png)

## Address and rename

-   Applies the selected DMX library to all selected actors.
-   Applies the same patch to all selected actors.
-   Also renames the selected actors so they match the provided patch names.

For more information on DMX patches and libraries, see the [DMX Overview](/documentation/en-us/unreal-engine/dmx-overview).