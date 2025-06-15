# Environment Query System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:13

---

The **Environment Query System (EQS)** is a feature within the Artificial Intelligence system in Unreal Engine 5 (Unreal Engine) that is used to collect data from the environment. Within EQS, you can ask questions about the data collected through a variety of different Tests which produces an Item that best fits the type of question asked. 

An EQS Query can be called from a [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) and used to make decisions on how to proceed based on the results of your Tests. EQS Queries are primarily made up of [Generators](/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine) (which are used to produce the locations or Actors that will be tested and weighted) and [Contexts](/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine) (which are used as a frame of reference for any Tests or Generators). EQS Queries can be used to instruct AI characters to find the best possible location that will provide a line of sight to a player to attack, the nearest health or ammo pickup, or where the closest cover point (among other possibilities). 

Once you have a general understanding of how Behavior Trees work in Unreal Engine and want to have your AI query the environment, you may want to start with the **Environment Query System Quick Start** guide which will walk you through an end-to-end example of having the AI find the best possible position to attack from a range against the player. Also refer to the Essentials section for an overview of EQS, a User Guide to working with EQS, and a node reference page that breaks down the available nodes and properties within EQS. 

## Starting Out

## Essentials