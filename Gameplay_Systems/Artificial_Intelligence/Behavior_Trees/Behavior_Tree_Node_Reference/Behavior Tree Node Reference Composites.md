# Behavior Tree Node Reference: Composites

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-composites](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-composites)  
**Processed:** 2025-06-14 16:56:21

---

**Composite** nodes define the root of a branch and the base rules for how that branch is executed. They can have [Decorators](/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-decorators) applied to them to modify entry into their branch, or even cancel out mid-execution. Also, they can have [Services](/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-services) attached to them that will only be active if the children of the Composite are being executed. 

Only Composite nodes can be attached to the Root node of a Behavior Tree.

## Selector

![Selector node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e93a9bf-e9bf-4c44-b02a-9e0288d1a5cd/selector-01.png)

**Selector** nodes execute their children from left to right. They stop executing when one of their children succeeds. If a Selector's child succeeds, the Selector succeeds. If all the Selector's children fail, the Selector fails.

| Property | Description |
| --- | --- |
| **Apply Decorator Scope** | If set, all Decorators in the branch below will be removed when execution flow leaves the branch (Decorators on this node are not affected). |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Sequence

![Sequence node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cf264f2-3ba1-438a-b669-b60b813d4591/sequence-01.png)

**Sequence** nodes execute their children from left to right. They stop executing when one of their children fails. If a child fails, then the Sequence fails. If all the Sequence's children succeed, then the Sequence succeeds.

| Property | Description |
| --- | --- |
| **Apply Decorator Scope** | If set, all Decorators in the branch below will be removed when execution flow leaves the branch (Decorators on this node are not affected). |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Simple Parallel

![The Simple Parallel node allows a single main Task node to be executed alongside of a full tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c436763d-10e8-46fa-a034-0e4ec945f353/simple-parallel-01.png)

The **Simple Parallel** node allows a single main Task node to be executed alongside of a full tree. When the main Task finishes, the setting in **Finish Mode** dictates if the node should finish immediately, aborting the secondary tree, or if it should delay for the secondary tree to finish.

| Property | Description |
| --- | --- |
| **Finish Mode** | 
-   **Immediate**: Once the main Task finishes, the background tree will be aborted.
-   **Delayed**: The background tree will be permitted to finish once the main Task has finished.



 |
| **Node Name** | The name the node should display in the Behavior Tree graph. |