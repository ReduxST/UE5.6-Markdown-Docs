# Mover

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mover-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mover-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:11

---

**Mover** is an Unreal Engine plugin that supports modular actor movement with rollback networking using the **Network Prediction Plugin** or **Chaos’ Networked Physics** system. The plugin empowers gameplay developers to craft motion without requiring networking expertise.

In addition to the documentation in this section, you can watch [An Introduction to the Mover Plugin | Unreal Fest 2024](https://www.youtube.com/watch?v=P4IKS5k47Wg) to learn more about the Mover plugin. You can also find additional information in the `README.md` file in your Unreal Engine directory under `\Engine\Plugins\Experimental\Mover\`.

We intend for the Mover plugin to become the next-generation approach to character movement and eventually replace the **Character Movement Component (CMC)** system. However, the Mover plugin is currently experimental, so many features still need to be completed, and the APIs, properties, and data formats are subject to change.

Even after Mover is production-ready, we intend to support the CMC system for the foreseeable future and will give plenty of notice to any potential deprecation plans.

## Topics