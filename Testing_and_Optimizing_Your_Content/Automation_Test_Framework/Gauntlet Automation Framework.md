# Gauntlet Automation Framework

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gauntlet-automation-framework-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/gauntlet-automation-framework-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:14

---

**Gauntlet** is a framework to run sessions of projects in **Unreal Engine** that perform tests and validate results. It is specifically designed for, but not limited to, running Unreal sessions on a variety of platforms. An Unreal **session** is all of the processes needed to execute a game with the Unreal engine. For example, a multiplayer game may require four clients and a server.

Gauntlet does not require any specific game-side automation code or test framework — how your game performs tests is entirely up to you. There is however a Gauntlet Plugin that provides a useful `TestController` class to assist with puppeteering and monitoring a game instance. It is well suited to smoke tests that require several steps to execute, but it is entirely optional.