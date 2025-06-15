# Build Configurations Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/build-configurations-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-configurations-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:11:14

---

Operating System

×Windows

Select an option from the dropdown to see content relevant to it.

Google has informed developers of a vulnerability in versions (earlier than M102) of WebRTC. Impacts, workarounds, and updates can be found [here](https://eoshelp.epicgames.com/s/news/eos-news-article-MCVDBTZSVM7VAJHF4ZGJVXZM52I4?language=en_US).

## Build Configuration Descriptions

**Unreal Engine (UE)** uses a custom building method via the **Unreal Build Tool (UBT)**. This tool processes the information necessary to build the engine's reflection system, integrating your C++ code with Blueprints, replication, serialization, and garbage collection.

### Build Configuration for UE Solution

When compiling a UE solution, you are compiling our engine's source code together with your project's source code. The following build configurations are available when building your project this way:

|   | Debug | DebugGame | Development | Shipping | Test |
| --- | --- | --- | --- | --- | --- |
| 
**Game**

 | 

✓

 | 

✓

 | 

✓

 | 

✓

 | 

✓

 |
| 

**Editor**

 | 

✓

 | 

✓

 | 

✓

 |  |  |
| 

**Client**

 | 

✓

 | 

✓

 | 

✓

 | 

✓

 | 

✓

 |
| 

**Server**

 | 

✓

 | 

✓

 | 

✓

 | 

✓

 | 

✓

 |

### Build Configuration for UE Project

When compiling a UE project, you are only compiling your project's source code. The following build configurations are available when building your project this way:

 |   | Debug | DebugGame | Development | Shipping | Test |
| --- | --- | --- | --- | --- | --- |
| 
**Game**

 |  | 

✓

 | 

✓

 | 

✓

 |  |
| 

**Editor**

 |  | 

✓

 | 

✓

 |  |  |
| 

**Client**

 |  |  |  |  |  |
| 

**Server**

 |  |  |  |  |  |