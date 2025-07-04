# BuildGraph Script Elements

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/buildgraph-script-elements-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/buildgraph-script-elements-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:11:23

---

**BuildGraph** scripts are written in XML. This document covers the types of data found within BuildGraph scripts, as well as their overall structure.

## Elements

**Elements** describe the data that they contain, making them one of the basic building blocks of BuildGraph scripts. The following tables contain items that are provided as metadata, which are exported when running on the build system. Although they are not used directly by BuildGraph when executing tasks locally, they are tagged with `[META]`.

## Graph Structure

A BuildGraph script is typically defined with the following elements:

-   `<Node>`
    
-   `<Aggregate>`
    
-   `<Agent>`
    
-   `<Trigger>`
    

### Node

`<Node>` is the smallest unit of execution in BuildGraph, with a set of inputs and outputs. Each `<Node>` consists of a sequence of tasks that are executed in order.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the node. |
| **Requires** | Target List | Optional | List of nodes, aggregates, or tagged file sets produced by other nodes that this node requires to execute, separated by semicolons. |
| **Produces** | Tag List | Optional | Tagged file sets that this node makes available to other nodes, separated by semicolons. |
| **After** | Target List | Optional | List of nodes that this node should run after, if they are part of the current target, separated by semicolons. These are ignored if they are not part of the current target. |
| **NotifyOnWarnings** | Boolean | Optional | If `false`, this node will not produce notifications on warnings. Only used by build systems. Defaults to `true`. `[META]` |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Aggregate

`<Aggregate>` declares a named aggregate that can be used as a synonym for either produced tag sets or a set of other nodes.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the aggregate. |
| **Requires** | Target List | Required | List of dependencies for this aggregate. These may be nodes, tagged file sets, or agent groups. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Agent

`<Agent>` defines requirements for an agent on nodes that will be executed in sequence (without cleaning intermediate directories). `<Agent>` requirements are ignored when building locally but must be specified.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the group. |
| **Type** | Identifier List | Optional | Type of agent to run on. The meaning of this string is inferred by the host build system, it does not have any intrinsic meaning. `[META]` |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Trigger

`<Trigger>` serves as a container for portions of the graph that should only be executed with explicit user intervention. To execute nodes behind a trigger, pass `-Trigger=<Name>` to the command line.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the trigger. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

## Property Manipulation

BuildGraph properties can be modified with the following elements:

-   `<Property>`
    
-   `<Option>`
    
-   `<EnvVar>`
    

### Property

`<Property>` sets the value of a property. If a property in an outer scope has already been declared with the same name, `<Property>` overwrites it. Otherwise, a new property is declared at the current scope.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the property to set. |
| **Value** | String | Required | New value for the property. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Option

`<Option>` defines a user option that can be set from the command line. `<Option>` may only appear at a global scope.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the option (and property) to initialize with the option's value. |
| **Description** | String | Required | Description for the option to display when running BuildGraph with the `-ListOnly` argument. |
| **Restrict** | Regex | Optional | Regex that matches valid values for this option (eg. `[a-zA-Z]+`, `true \| false`). |
| **DefaultValue** | String | Required | Default value for the option if the user does not set it explicitly. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### EnvVar

`<EnvVar>` declares a property to contain the contents of an environment variable (or an empty string if it is not set). `<EnvVar>` may only appear at a global scope.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Name of the environment variable to introduce as a property. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

## Flow Control

You can control the flow of your BuildGraph scripts with the following elements:

-   `<Include>`
    
-   `<Do>`
    
-   `<Switch>`
    
-   `<ForEach>`
    

### Include

`<Include>` processes the contents of another BuildGraph script as if it appeared within this file. `<Include>` may only appear at a global scope.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Script** | String | Required | Path to the script you want to include (relative to the current script). |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Do

`<Do>` groups a sequence of elements and only processes them if a condition evaluates as true.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Switch

`<Switch>` is similar to a [C](http://www.open-std.org/jtc1/sc22/wg14/www/standards) switch statement because it evaluates the conditions on a sequence of branches, processing the first statement with a condition that evaluates as true.

Example `<Switch>` statement:

```
	`<Switch> 		<Case If=X> 			<Elements go here if X is true> 		</Case> 		<Case If=Y> 			<Elements go here if X is false but Y is true> 		</Case> 		<Default> 			<Elements go here otherwise> 		</Default> 	</Switch>`
Copy full snippet
```
<Switch> <Case If=X> <Elements go here if X is true> </Case> <Case If=Y> <Elements go here if X is false but Y is true> </Case> <Default> <Elements go here otherwise> </Default> </Switch>

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### ForEach

`<ForEach>` expands the body of the element with a given property assigned to each item in a list that is separated by semicolons.

Example `<ForEach>` statement:

```
	`<ForEach Name="Counter" Values="1;2;3;4;5"> 		<Log Message="Counter=$(Counter)"/> 	</ForEach>`
Copy full snippet
```
<ForEach Name="Counter" Values="1;2;3;4;5"> <Log Message="Counter=$(Counter)"/> </ForEach>

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Name** | Name | Required | Property to assign to each value in the list. |
| **Values** | String List | Required | List of values that are separated by semicolons. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

## Diagnostics

You can perform diagnostics on your BuildGraph scripts with the following elements:

-   `<Warning>`
    
-   `<Error>`
    

### Warning

`<Warning>` outputs a warning message before executing the graph. `<Warning>` may be included in nodes, agents, triggers, or at global scope. `<Warning>` will only provide an output if it's still part of the graph after it has been trimmed down to the target being executed.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Message** | String | Required | Text to be printed to the log. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |

### Error

`<Error>` outputs an error message. `<Error>` may be included in nodes, agents, triggers, or at global scope. `<Error>` will only provide an output if it is still part of the graph after it has been trimmed down to the target being executed.

| Attribute | Type | Required? | Description |
| --- | --- | --- | --- |
| **Message** | String | Required | Text to be printed to the log. |
| **If** | Condition | Optional | Condition to be evaluated. The element is ignored unless the condition evaluates to `true`. |