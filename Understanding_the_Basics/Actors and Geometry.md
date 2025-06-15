# Actors and Geometry

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/actors-and-geometry-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/actors-and-geometry-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:41

---

An **Actor** is any object that can be placed into a Level, such as a camera, Static Mesh, or player start location. Actors support 3D transformations such as translation, rotation, and scaling. They can be created (spawned) and destroyed through gameplay code (C++ or Blueprints).

In C++, `AActor` is the base class of all Actors.

To create a Level, you place Actors into a Level (map), then move and scale them to create an environment, and add script to make them behave the way you want. This section covers the basic techniques of working with Actors, such as placing, selecting, and transforming Actors. It also covers some of the most commonly used Actor types.

## Working with Actors

## Common Actor Types

This is not a comprehensive list of every Actor type available in Unreal Engine. Some plugins and project templates add their own Actors, and certain Actors may not be available for all projects.