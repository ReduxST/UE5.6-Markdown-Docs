# Basic Scripting with Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/basic-scripting-with-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/basic-scripting-with-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:43

---

Blueprints provide a visual approach to a scripting language. As such, the system shares many of the nuances of a standard written scripting language, such as data typed variables, arrays, structs, etc. Execution flow also works as it does in a typical scripting language, although Blueprints require explicit linear execution for each node. Each of the pages below go into more detail about different variable types, working with those variables, and execution of nodes within the graph.

## Variables

Variables can be created in a variety of different types, including data types such as Boolean, integer, and float. They are color-coded for easy identification within your Blueprint. Blueprint variables can also be reference types for holding things like Objects, Actors, and Classes.

## Execution Flow

In Blueprints, the first node to execute is an event, and then execution flows through the white execution wire from left to right. You can visualize the execution flow while your game is running in the editor, which can help with debugging. Data also flows through wires colored to match the variable types. Input pins are evaluated when the node executes, tracing the data wires back from right to left until the final result is calculated and supplied to the node.

Nodes with execution pins (impure nodes) store the values of their output pins when they execute, while nodes without execution pins (pure nodes) reevaluate their outputs every time a node connected to their outputs executes.