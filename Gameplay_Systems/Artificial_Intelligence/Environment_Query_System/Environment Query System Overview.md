# Environment Query System Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:16

---

The **Environment Query System** (or EQS for short) is a feature within the AI Tools in Unreal Engine 5 (Unreal Engine) that can be used for collecting data about the environment. Then, through the use of a [Generator](/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine), the system can ask questions about that data through a variety of user-defined [Tests](/documentation/en-us/unreal-engine/eqs-node-reference-tests-in-unreal-engine), returning the best **Item** that fits the types of questions being asked. Some example use-cases for EQS could be to find the closest health pickup or ammo, figure out which enemy is the highest threat, or find a line of sight to the Player (an example of which is shown below). 

![Find line of sight to the Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7a7a0c6-a948-4e84-9d7e-134920c0d468/environment-query-system-overview-find-player.png)

The conceptual idea and theory behind EQS come from Unreal Engine 3's **Environment Tactical Query** (ETQ) system which you can read more about in the following article, [Asking the Environment Smart Questions](https://epicgames.box.com/s/b5vbufy1pp58k638wkrdp6xeht53k1zb).

## EQS Basics

EQS Query assets can be created in the **Content Drawer** and can be edited inside a special **Environmental Query Editor**. The Environmental Query Editor is a node-based editor where you can add a Generator node to produce Items, add your desired Tests to run on those Items and the [Context](/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine) in which to run them. Unreal Engine supplies many Generator types by default, however, you can create your custom Generators through Blueprint (or C++ for even faster execution). 

![Add a Distance Test to our existing Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b14198a3-8c15-4b5c-bc04-2de8778a15aa/environment-query-system-adding-a-test.png)

*Above, we add a **Distance** Test to our existing Generator.*

Similar to Generators, there are several different types of Tests you can run to filter and (or) score the Items returned. Unlike Generators, custom Tests can only be created through C++. Multiple Tests can be added to a Generator and is a common practice to narrow down the Item results that are returned. The order in which you add Tests to a Generator does not matter as filter Tests are done before scoring Tests. This is done so that fewer Items are returned and need to be scored. Refer to the table below for the type of tests. 

| Node Type | Description |
| --- | --- |
| **Generator** | This produces the locations or Actors, referred to as **Items**, that will be tested and weighted. |
| **Contexts** | These are a frame of reference for the various Tests and Generators. |
| **Tests** | These are how the Environment Query decides which Item from the Generator is the "best" option. |

Please refer to the [EQS Node Reference](/documentation/en-us/unreal-engine/environment-query-system-node-reference-in-unreal-engine) page for more information on each type.

Once you have set up your EQS Query, you can run it through a [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) using the **Run EQS Query** Task node. 

![Run EQS Query Task node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2e461a5-0b8e-4960-afee-c518f88e9af1/environment-query-system-overview-run-environment-query-system-1.png)

For a full walk-through of creating and using an EQS Query, please see the [EQS Quick Start Guide](/documentation/en-us/unreal-engine/environment-query-system-quick-start-in-unreal-engine).

## Enabling EQS

Before you can start working with EQS, you will need to enable it from the **Project Settings** menu.

-   Under the **Settings > Plugins** section, enable the **Environment Query Editor** option if necessary.
    
    ![Enable the Environment Query Editor option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bd06f0b-9164-4ac2-b296-38def1c2809a/environment-query-system-user-guide-enable-environment-query-system.png)

## Previewing an EQS Query

You can preview the results of an EQS Query inside the Editor, where weighted/filtered results will be represented by debugging spheres. 

![Debug Spheres](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80fcfcce-3fb8-4b8d-8ed2-9fc5c2689f8f/environment-query-system-user-guide-preview.png)

In the image above, we debug an EQS Query that returns a location that provides a line of sight to the Player Character in the Level. 

Please see [AI Debugging](/documentation/en-us/unreal-engine/ai-debugging-in-unreal-engine) or [EQS Testing Pawn](/documentation/en-us/unreal-engine/environment-query-testing-pawn-in-unreal-engine) for more information.