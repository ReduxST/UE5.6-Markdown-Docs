# Dataflow Graph

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataflow-graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataflow-graph)  
**Processed:** 2025-06-14 16:18:38

---

The **Dataflow Graph** system is a **node-based procedural asset generation environment** inside the Unreal Engine editor.

Dataflow was created to **improve iteration times** when creating certain asset types in the engine. The same Dataflow graph can be **used by multiple assets** and the graph itself can produce different results depending on the inputs given by the source asset.

Dataflow is a **general-purpose system** that can be adapted to various physics asset types, such as **Chaos Cloth**, **Chaos Flesh**, and **Geometry Collection fracturing**. The system is **designed to be extensible** by developers using C++. Developers can further adapt the system to accommodate their specific needs.

You can learn more about Dataflow by reading the documentation: