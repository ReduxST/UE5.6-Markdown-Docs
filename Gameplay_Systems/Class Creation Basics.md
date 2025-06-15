# Class Creation Basics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/class-creation-basics-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/class-creation-basics-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:35

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d54c61fa-60b4-4a9e-8426-ea6e476374c4/lightswitchactor.png)

These examples show how to create a new class using Blueprints only, C++ code only, and a combination of C++ code and Blueprints. The goal is to create new LightSwitch classes with the same properties and behavior using all three workflows, and then add an instance of each new class to the level, so there are three new LightSwitch Actors.

LightSwitch classes are based directly on the Actor class, since their primary requirement is that they can be placed within the level. They contain a PointLightComponent as the root component, and a SphereComponent that is a child of the PointLightComponent. Each LightSwitch class also has a variable called DesiredIntensity, which is used to set the intensity of the PointLightComponent. Finally, the default behavior of the classes is that when the player enters or leaves the SphereComponent, the PointLightComponent's visibility will be toggled.

## Examples