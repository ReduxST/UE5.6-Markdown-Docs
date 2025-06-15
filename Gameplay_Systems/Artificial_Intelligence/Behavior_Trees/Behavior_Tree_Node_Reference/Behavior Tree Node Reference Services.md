# Behavior Tree Node Reference: Services

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-services](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-services)  
**Processed:** 2025-06-14 16:56:24

---

**Services** attach to [Composite](/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-composites) or [Task](/documentation/en-us/unreal-engine/unreal-engine-behavior-tree-node-reference-tasks) nodes and will execute at their defined frequency as long as their branch is being executed. These are often used to make checks and to update the Blackboard. These take the place of traditional Parallel nodes in other Behavior Tree systems.

## Default Focus

![The Default Focus creates a shortcut to accessing an Actor in your Blueprints and Code by setting the focus of the AI Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dc4d65a-6683-4c14-83c1-8cbe6c4f628b/default-focus.png)

The **Default Focus** creates a shortcut to accessing an Actor in your **Blueprints** and Code by setting the focus of the AI Controller. By setting the focus of the AI Controller to an Actor, you can directly access it from the AI Controller instead of accessing a Blackboard key.

| Property | Description |
| --- | --- |
| **Blackboard Key** | This takes in an Actor Key (an Object Key with its base class set to Actor) to be quickly referenced by the AI Controller using `GetFocusActor`. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Run EQS

![The Run EQS Service node can be used to regularly execute an Environmental Query System (EQS) template at assigned intervals and can update a specified Blackboard Key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/509caf29-e42a-4284-841e-66c130985c09/run-eqs-image.png)

The **Run EQS** Service node can be used to regularly execute an [Environmental Query System (EQS)](/documentation/en-us/unreal-engine/environment-query-system-in-unreal-engine) template at assigned intervals and can update a specified Blackboard Key.

| Property | Description |
| --- | --- |
| **Query Template** | The EQS asset to run. |
| **Query Config** | Optional array of additional parameters to include in the query. |
| **EQSQuery Blackboard Key** | Option to use a Blackboard Key that stores an EQS Query Template instead of a specified EQS Query Template. |
| **Run Mode** | 
-   **Single Best Item**: Pick the first item with the best score.
-   **Single Random Item from Best 5%**: Pick a random item with a score `95%` to `100%` of max.
-   **Single Random Item from Best 25%**: Pick a random item with a score `75%` to `100%` of max.
-   **All Matching**: Get all items that match conditions.



 |
| **Update BBOn Fail** | Updates the Blackboard when the EQS query fails. |
| **Blackboard Key** | The Blackboard Key the Service will write results into - either an FVector or an Actor. |
| **Interval** | Defines the time span between subsequent ticks of the Service. |
| **Random Deviation** | Adds a random range value to the Service's **Interval** value. |
| **Call Tick on Search Start** | Call Tick Event when Task search enters this node (**Search Start** will be called as well). |
| **Restart Timer on Each Activation** | If set, the next Tick time will be always reset to Service's **Interval** value when the node is activated. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |

## Custom Services

![New Custom Service](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58c96e69-5582-4bd6-9455-76fa9e2d4a78/new-custom-service-01.png)

You can create **Services** by clicking the **New Service** button from the toolbar that contains Blueprint logic and (or) parameters.

![You can create Services by clicking the New Service button from the toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dd8eb50-a1ad-42aa-8d71-c10389119944/new-custom-service.png)

Blueprint Services are less performant than C++ Services. If optimization is a concern, you may want to use native Services.

The following properties are also available when creating a Service.

| Property | Description |
| --- | --- |
| **Show Property Details** | Shows detailed information about properties when enabled. |
| **Show Event Details** | Shows detailed information about implemented Events when enabled. |
| **Node Name** | The name the node should display in the Behavior Tree graph. |
| **Interval** | Defines the time span between subsequent ticks of the Service. |
| **Random Deviation** | Adds a random range value to the Service's **Interval** value. |
| **Call Tick on Search Start** | Call Tick Event when Task search enters this node (**Search Start** will be called as well). |
| **Restart Timer on Each Activation** | If set, the next Tick time will be always reset to Service's **Interval** value when the node is activated. |