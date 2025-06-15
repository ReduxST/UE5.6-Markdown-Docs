# Environment Query System Node Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-node-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-node-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:14

---

An **Environment Query** is made up of many different pieces. You must call an Environment Query from a [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine), and then the actual Environment Query will use its **Generator**, reference its **Contexts**, and use its **Tests** to give the Behavior Tree the highest weighted result.

| Node Type | Description |
| --- | --- |
| **Generator** | Produces the locations or Actors, referred to as **Items**, that will be tested and weighted. |
| **Contexts** | Provides a frame of reference for the various Tests and Generators. |
| **Tests** | Establishes how the Environment Query decides which Item from the Generator is the best option. |

Please refer to the links below for additional information on each subject.