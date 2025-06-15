# Behavior Tree Node Reference: Decorators

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-decorators](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-decorators)  
**Processed:** 2025-06-14 16:56:22

---

**Decorator**, also known as conditionals in other Behavior Tree systems, are attached to either a [Composite](/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-composites) or a [Task](/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-tasks) node and define whether or not a branch in the tree, or even a single node, can be executed.

## Blackboard

![Decorator also known as conditionals in other Behavior Tree systems are attached to either a Composite or a Task node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27926996-77c4-4ef4-b182-9b26dff4087a/decorators-01.png)

The **Blackboard** node will check to see if a value is set on the given **Blackboard Key**.

| Property | Description |
| --- | --- |
| **Notify Observer** | 
-   **On Result Change**: Reevaluate only when the condition has changed.
-   **On Value Change**: Reevaluate only when the observed Blackboard Key changes.



 |
| **Observer Aborts** | 

-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Blackboard Key** | 

The Blackboard Key the Decorator will work on. 



 |
| **Key Query** | 

-   **Is Set**: Is the value set?
-   **Is Not Set**: Is the value not set?



 |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Check Gameplay Tag Condition

![Gameplay Tag Condition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24d6bf65-5de6-4c10-91ea-56823532650b/decorators-02.png)

| Property | Description |
| --- | --- |
| **Actor to Check** | The Blackboard Key that contains the reference to the Actor to check. |
| **Tags to Match** | Should the Decorator match **Any** or **All** of the Tags listed in the property **Gameplay Tags**. |
| **Gameplay Tags** | Loads the **Gameplay Tag** editor to select the tags that should be used in this Decorator. |
| **Inverse Condition** | If the result of this Decorator be inversed where false becomes true and true becomes false. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Compare BBEntries

![The Compare BBEntries node will compare the values of two Blackboard Keys and will block or allow the execution of a node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7292b0f-d786-4f54-813e-49d219fbe883/decorators-03-1.png)

The **Compare BBEntries** (Blackboard Entries) node will compare the values of two **Blackboard Keys** and will block or allow the execution of a node based on if the result is equal to or not equal to.

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Operator** | 

-   **Is Equal To**: Are the two Keys equal to each other?
-   **Is Not Equal To**: Are the two Keys different from each other?



 |
| **Blackboard Key A** | The first Key to use in this comparison. |
| **Blackboard Key B** | The second Key to use in this comparison. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Composite

![The Composite Decorator node enables you to set up more advanced logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9d9b9f1-e203-4f57-9bb6-1b644d307c8b/decorators-04.png)

The **Composite Decorator** node enables you to set up more advanced logic than the built-in nodes but not as complex as a full Blueprint. Once you have added a Composite Decorator to a node, double-click the Composite Decorator to bring up the Composite's Graph. By right-clicking in the graph area you can add Decorator nodes as standalone nodes, then wire them together through **AND** nodes, **OR** nodes, and **NOT** nodes, to create more advanced logic:

Click image for full view.

| Property | Description |
| --- | --- |
| **Composite Name** | The name the node should display in the Behavior Tree graph. |
| **Show Operations** | This will cause the operations to be listed on the node in plain text. |

Using a Composite Decorator in this manner will impact memory and performance. It is possible to create a Decorator in C++ that will do the same custom behavior but in a more efficient way.

## Conditional Loop

As long as the **Key Query** condition is met, this Decorator will have the node it's attached to the loop.

![Decorator will have the node it's attached to loop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d0fe962-b58e-40d3-9be3-d45c1e08581a/decorators-05.png)

| Property | Description |
| --- | --- |
| **Blackboard Key** | 
The Blackboard Key the Decorator will work on. 



 |
| **Key Query** | 

-   **Is Set**: Is the value set?
-   **Is Not Set**: Is the value not set?



 |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Cone Check

![The Cone Check Decorator takes in three Vector Keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f7b2d63-7bd4-4dc1-98c7-46ebb8d94483/decorators-06-1.png)

The **Cone Check** Decorator takes in three Vector Keys: the first for the location to start the cone, the second to define the direction the cone points, and the third for the location to check if it is inside the cone. You define the angle of the cone by using the **Cone Half Angle** property.

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Cone Half Angle** | The half angle of the cone. For example, for a 90-degree cone, this value should be set to 45 degrees. |
| **Cone Origin** | The location where the cone should start (the tip of the cone). |
| **Cone Direction** | The direction in which the mouth of the cone should point. |
| **Observed** | The location or Actor that is being checked to see if it is in the cone. |
| **Inverse Condition** | 

If the result of this Decorator is inversed where false becomes true and true becomes false.



 |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Cooldown

![The Cooldown node will lock the execution of a node or branch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45af2c9b-9a5a-41fa-9c83-41c75b0b310c/decorators-07.png)

The **Cooldown** node will lock the execution of a node or branch until the cooldown time expires.

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Cooldown time** | The time, in seconds, the Cooldown Decorator should lock the execution of this node. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Custom Decorators

![Custom Decorator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c0187ca-cb2d-47c9-93d4-dc64fe88866f/custom-decorator.png)

You can create new **Decorators** with your own custom Blueprint logic and (or) parameters by clicking the **New Decorator** button. 

![You can create new Decorators by clicking the New Decorator button ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc73288a-d5ea-4b23-9b5f-8625ea0788b8/new-decorator-create.png)

The following parameters will also be included with your custom logic. 

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Show Property Details** | Show detailed information about properties on the node. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |
| **Inverse Condition** | 

If the result of this Decorator is inversed where false becomes true and true becomes false.



 |

## Does Path Exist

![The Does Path Exist node checks to see if a path can be made from the two vectors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc4d2bec-a1cf-445d-ad1b-3db6470b6c3b/decorators-08.png)

The **Does Path Exist** node checks to see if a path can be made from the two vectors: Blackboard Key A and Blackboard Key B.

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Blackboard Key A** | The first location in the path. |
| **Blackboard Key B** | The second location in the path. |
| **Path Query Type** | 

-   **NavMesh Raycast 2D**: Really Fast
-   **Hierarchical Query**: Fast
-   **Regular Path Finding**: Slow



 |
| **Inverse Condition** | 

If the result of this Decorator is inversed where false becomes true and true becomes false.



 |
| **Filter Class** | Which navigation data should be used? If set to **None** the default navigation data will be used. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Force Success

![The Force Success Decorator changes the node result to a success](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4474d8b-b3aa-4ecf-ba19-b55f911f33cf/decorators-09.png)

The **Force Success** Decorator changes the node result to success. 

| Property | Description |
| --- | --- |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Is At Location

![The Is At Location Decorator node checks if the AI controlled Pawn is at the given location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dec1d80c-3e7d-452d-a76a-fd2e22423849/decorators-10.png)

The **Is At Location** Decorator node checks if the AI-controlled Pawn is at the given location. 

| Property | Description |
| --- | --- |
| **Acceptable Radius** | The distance threshold to accept as being at location. |
| **Parametrized Acceptable Radius** | A parameter based Acceptable Radius (such as **Random Number**). |
| **Geometric Distance Type** | With **Path Finding Based Test** disabled, this enables you to set the distance type to 3D, 2D, or Z values. |
| **Use Nav Agent Goal Location** | 
If moving to an Actor and this Actor is a Nav Agent, then we will move to their Nav Agent Goal Location. 



 |
| **Path Finding Based Test** | If enabled, the result will be consistent with tests done while following paths. If disabled, use **Geometric Distance** as configured with **Distance Type**. |
| **Inverse Condition** | 

If the result of this Decorator is inversed where false becomes true and true becomes false.



 |
| **Blackboard Key** | The Blackboard Key value to test against. |
| **Node Name** | The user defined-name of the node. |

## Is BBEntry Of Class

![The Is BBEntry Of Class Decorator node is used to determine if the designated Blackboard Key is of a specified Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bef63abc-255f-4fd2-9e97-29f61570f55b/decorators-11.png)

The **Is BBEntry Of Class** Decorator node is used to determine if the designated Blackboard Key is of a specified Class. 

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Test Class** | The Class type that is tested against the Class of the Object of the Blackboard Key property. |
| **Blackboard Key** | The Blackboard Key that is tested. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Keep in Cone

![The Keep in Cone Decorator node that bases its condition on whether the observed position is still inside a cone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8c23d7c-0da2-4f26-8ff1-d2cb888a17e7/decorators-12.png)

The **Keep in Cone** Decorator node bases its condition on whether the observed position is still inside a cone. The cone's direction is calculated when the node first becomes relevant.

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Cone Half Angle** | The half angle of the cone. For example, for a 90-degree cone, this value should be set to 45 degrees. |
| **Cone Origin** | The location where the cone should start (the tip of the cone) |
| **Observed** | The location or Actor to keep in the cone. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Loop

![The Loop Decorator loops the node or branch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/749a7ffb-14c6-4c7c-a208-4046c52b1721/decorators-13.png)

The **Loop** Decorator loops the node or branch a number of times, or infinitely.

| Property | Description |
| --- | --- |
| **Num Loops** | The number of loops to run. |
| **Infinite Loop** | Should this loop run indefinitely? |
| **Infinite Loop Timeout Time** | Timeout value if **Infinite Loop** is enabled (a negative value will loop forever). |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Set Tag Cooldown

![A Decorator node that bases its condition on whether a cooldown timer from a Gameplay Tag has expired](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/591e32a0-27d8-4eb2-ab76-86f7a36ebf05/decorators-14.png)

The **Set Tag Cooldown** node enables you to set a cooldown duration for a Gameplay Tag. 

| Property | Description |
| --- | --- |
| **Cooldown Tag** | The GameplayTag that will be used for the Cooldown. |
| **Cooldown Duration** | How long the Cooldown is in seconds. |
| **Add to Existing Duration** | If there is an existing Cooldown on the given GameplayTag, should we add more? |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Tag Cooldown

![The Time Limit Decorator will give a branch or node a set amount of time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0ab31ab-51ff-448f-a3a6-4db73bb9c3b7/decorators-15.png)

A Decorator node that bases its condition on whether a cooldown timer from a Gameplay Tag has expired. 

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Cooldown Tag** | The GameplayTag that will be used for the Cooldown. |
| **Cooldown Duration** | How long the Cooldown is in seconds. |
| **Add to Existing Duration** | If there is an existing Cooldown on the given GameplayTag, should we add more? |
| **Adds/Sets Cooldown on Deactivation** | Whether or not we are adding/setting to the CooldownTag's value when the decorator deactivates. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Time Limit

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98defa86-5338-47a6-9676-9642fef8d6ba/decorators-16.png)

The **Time Limit** Decorator will give a branch or node a set amount of time to finish before stopping it and failing out. The timer is reset every time the node gains focus.

| Property | Description |
| --- | --- |
| **Observer Aborts** | 
-   **None**: Do not abort anything.
-   **Self**: Abort self and any subtrees running under this node.
-   **Lower Priority**: Abort any nodes to the right of this node.
-   **Both**: Abort self, any subtrees running under this node, and any nodes to the right of this node.



 |
| **Time Limit** | The time limit before the node fails out, in seconds. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |