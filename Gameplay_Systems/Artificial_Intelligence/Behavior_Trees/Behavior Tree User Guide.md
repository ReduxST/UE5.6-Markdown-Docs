# Behavior Tree User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-tree-in-unreal-engine---user-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-tree-in-unreal-engine---user-guide)  
**Processed:** 2025-06-14 16:09:52

---

## Creating Behavior Tree Assets

This section illustrates how to create the various **Behavior Tree** assets within Unreal Engine 5. 

### Creating a Behavior Tree

**Behavior Trees** are essentially the AI's processor and can make decisions and execute various branches based on the outcome of those decisions. **Behavior Trees** are created inside the **Content Drawer** in the following manner: 

Click the **+Add** button, then under **Create Advanced Asset** select **Artificial Intelligence** and **Behavior Tree**.

![Click the Add button then under Create Advanced Asset select Artificial Intelligence and Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/279a2d54-57bb-4a8b-9078-3c284db631ba/behavior-tree-user-guide-01.png)

The new **Behavior Tree** asset will be added to the **Content Drawer** where you can define its name.

![The new Behavior Tree asset will be added to the Content Drawer where you can define its name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/738c8c69-7624-4380-9f0b-a5ca40b1b917/behavior-tree-user-guide-02.png)You can also use the right-click context menu and select **+Add > Artificial Intelligence > Behavior Tree.** 

### Creating a Blackboard

The **Blackboard** asset can be considered as the "brain" of the AI and stores **Key** values that the **Behavior Tree** uses to make its decisions.  **Blackboard** assets can be created using the following methods:

Click the **+Add** button, then under **Create Advanced Asset** select **Artificial Intelligence** and **Blackboard**.

![Click the Add button, then under Create Advanced Asset select Artificial Intelligence and Blackboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffa9ffb2-4127-49f6-9fe0-3cbd5791fe0e/behavior-tree-user-guide-03.png)

The new **Blackboard** asset will be added to the **Content Drawer** which you can rename to your desired name.

![The new Blackboard asset will be added to the Content Drawer which you can rename to your desired name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33ff5856-6de6-46d1-90b9-30bc939df2eb/behavior-tree-user-guide-04-1.png)

Another method in which you can create a Blackboard is inside a Behavior Tree: 

Inside the **Behavior Tree Editor** from the Toolbar by clicking the **New Blackboard** button. 

![Inside the Behavior Tree Editor from the Toolbar by clicking the New Blackboard button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2f059be-7c80-43cc-9fa8-23be5995ede9/behavior-tree-user-guide-05.png)

This will also create a new **Blackboard** asset inside the **Content Drawer**. 

### Creating a Behavior Tree Task

A **Task** is an "action" you want the AI to perform, such as move to a location or rotate to face something. 

If optimization is a concern, you may want to consider switching Blueprint Behavior Tree Tasks to native Behavior Tree Tasks.

In addition to the existing **Tasks** available, you can create custom **Tasks** with your own logic: 

Click the **New Task** button from the Toolbar inside the **Behavior Tree Editor**. 

![Click the New Task button from the Toolbar inside the Behavior Tree Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5c0295a-bac3-4c94-87ef-fb3fa90c2f76/behavior-tree-user-guide-task.png)

This will open a new **Blueprint** of the **BTTask\_BlueprintBase** class where you can provide your **Task** logic. 

![This will open a new Blueprint of the BTTask_BlueprintBase class where you can provide your Task logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ea88ed8-cd0d-4b23-b528-0b04ab46e70c/behavior-tree-user-guide-task-2.png)

The **Task Blueprint** will be created inside the **Content Drawer** in the same location as your **Behavior Tree** asset. 

Whenever you create a new **Task** from the **Behavior Tree Editor**, it's a good practice to go into the **Content Drawer** and rename the asset instead of using the default name.

When creating a new **Task**, you can use an existing **Behavior Tree Task** as the **Parent Class** to inherit functionality by selecting it from the drop-down menu. 

![You can use an existing Behavior Tree Task as the Parent Class to inherit functionality  by selecting it from the drop-down menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/323c8524-37eb-4579-819a-a72fc18015ba/behavior-tree-user-guide-task-3.png)

### Creating a Behavior Tree Decorator

**Decorators** (also known as conditionals) attach to nodes inside **Behavior Trees** and can be used to make decisions on whether a branch (or even a single node) in the tree can be executed. There are several default **Decorators** that you can use in your **Behavior Trees**, however, you can also create custom ones:

Click the **New Decorator** button from the Toolbar inside the **Behavior Tree Editor**. 

![Click the New Decorator button from the Toolbar inside the Behavior Tree Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17916fe9-90c3-4e48-996a-c0b1970507ed/behavior-tree-user-guide-decorator.png)

This will open a new **BTDecorator\_BlueprintBase** class where you can provide your **Decorator** logic. 

![This will open a new BTDecorator_BlueprintBase class where you can provide your Decorator logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/159b9035-9a52-4ba6-909a-ec9c5eba5c93/behavior-tree-user-guide-decorator-2.png)

The **Decorator Blueprint** will be created inside the **Content Drawer** in the same location as your **Behavior Tree** asset. 

Whenever you create a new **Decorator** from the **Behavior Tree Editor**, it's a good practice to go into the **Content Drawer** and rename the asset instead of using the default name.

When creating a new **Decorator**, you can use an existing **Behavior Tree Decorator** as the **Parent Class** to inherit functionality from by selecting it from the drop-down menu. 

![You can use an existing Behavior Tree Decorator as the Parent Class to inherit functionality from by selecting it from the drop-down menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c3f4c73-f636-49e1-8199-beca8750d13b/behavior-tree-user-guide-decorator-3.png)

### Creating a Behavior Tree Service

**Services** attach to **Composite** nodes and will execute at their defined frequency as long as their branch is being executed. These are often used to make checks and to update the **Blackboard** and take the place of traditional Parallel nodes in other Behavior Tree systems. While there are a few **Services** available by default, you will more than likely want to create your own custom **Services** that assist in determining how your **Behavior Tree** is executed. 

If optimization is a concern, you may want to consider switching Blueprint Behavior Tree Services to native Behavior Tree Services.

Click the **New Service** button from the Toolbar inside the **Behavior Tree Editor**. 

![Click the New Service button from the Toolbar inside the Behavior Tree Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9683c9e-9372-4aa7-831d-fdec83cfc4ae/behavior-tree-user-guide-service.png)

This will open a new **BTService\_BlueprintBase** class where you can provide your **Service** logic. 

![This will open a new BTService_BlueprintBase class where you can provide your Service logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd92c6f2-59c6-45fd-8bb5-a1409dbbe589/behavior-tree-user-guide-service-2.png)

The **Service** **Blueprint** will be created inside the **Content Drawer** in the same location as your **Behavior Tree** asset. 

Whenever you create a new **Service** from the **Behavior Tree Editor**, it's a good practice to go into the **Content Drawer** and rename the asset instead of using the default name.

When creating a new **Service**, you can use an existing **Behavior Tree Service** as the **Parent Class** to inherit functionality by selecting it from the drop-down menu. 

![You can use an existing Behavior Tree Service as the Parent Class to inherit functionality from by selecting it from the drop-down menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5db7c055-4b9b-4b20-b332-2e3aa5a9b7c0/behavior-tree-user-guide-service-3.png)

## Editing a Blackboard

Usually, you'll create a **Blackboard** before your **Behavior Tree** as the **Behavior Tree** references the **Blackboard** in its decision-making process (you can always add **Keys** later as you need them). You can edit a **Blackboard** asset by double-clicking on the asset in the **Content Drawer** to open it up in the **Blackboard Editor**.

![You can edit a Blackboard asset by double-clicking on the asset in the Content Drawer to open it up in the Blackboard Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c63be00-4e63-405a-8508-1299f4643c51/behavior-tree-user-guide-blackboard-01.png)

If you are editing a **Behavior Tree** that has an assigned **Blackboard**, you can switch to the **Blackboard** by clicking the tab in the upper-right corner of the window.

![You can switch to the Blackboard by clicking the tab in the upper-right corner of the window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9c42b5e-9acf-4137-8e2d-568b7541db93/behavior-tree-user-guide-blackboard-02.png)

In the **Blackboard Details** panel, you can assign a different **Blackboard** as the **Parent**, inheriting **Keys** from it.

![In the Blackboard Details panel you can assign a different Blackboard as the Parent, inheriting Keys from it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e6df430-7e23-4da9-9b8d-49effe778fc4/behavior-tree-user-guide-blackboard-parent-1.png)

You can add **Keys** by clicking the **New Key** button in the **Blackboard** window.

![You can add Keys by clicking the New Key button in the Blackboard window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5eb13f1-0449-4405-8290-5fe163160a40/behavior-tree-user-guide-blackboard-03.png)

Please see **Blueprint Variables** for a breakdown of variable types that can be stored as **Keys**.

When a **Key** has been created, you can define properties associated with the **Key** in the **Blackboard Details** panel.

![You can define properties associated with the Key in the Blackboard Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/264701a7-03e4-4bec-a5cb-9871d71cbd8c/behavior-tree-user-guide-blackboard-04.png)

| Property | Description |
| --- | --- |
| **Entry Name** | The user defined name of the Key. |
| **Entry Description** | Optional description to explain what this Blackboard Key does. |
| **Key Type** | 
Defined when you create the Key, however ,**Object** and **Class** Keys provide the additional option of defining a specific **Class**. This enables you to store any type of data that inherits from Object (such as Actors) in them.



 |
| **Instance Synced** | This is used to determine if the Key will be synchronized across all instances of the Blackboard. |

To **Rename** or **Delete** Key, right-click a **Key** to bring up the context menu, or press **F2** or **Delete** on a **Key**.

![To Rename or Delete Key right-click a Key to bring up the context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e9226ad-d277-4a07-885c-2a7ef6eb5eba/behavior-tree-user-guide-blackboard-05.png)

For **Class** and **Object** Keys, you can click the little triangle beside **Key Type** which enables you to define the Base Actor Class to use.

![For Class and Object Keys you can click the little triangle beside Key Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fcbf302-d959-424b-9dba-c671b9676253/behavior-tree-user-guide-base-class.png)

For **Enum** Keys, there are additional properties that can be set by clicking the little triangle beside **Key Type**.

![For Enum Keys there are additional properties that can be set by clicking the little triangle beside Key Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f9dc946-f48f-4b59-9385-5ad00bb07272/behavior-tree-user-guide-advanced-enum.png)

| Property | Description |
| --- | --- |
| **Enum Type** | The assigned Enumeration to use. |
| **Enum Name** | The name of the enum defined in C++ code will take priority over the asset assigned under **Enum Type**. |
| **Is Enum Name Valid** | Set when **Enum Name** override is valid and active. |

## Editing a Behavior Tree

To edit a **Behavior Tree**, you will need to open a **Behavior Tree** asset: 

Double-click a **Behavior Tree** asset in the **Content Drawer** to enter **Behavior Tree Mode**. 

![Double-click a Behavior Tree asset in the Content Drawer to enter Behavior Tree Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ec4cfce-007c-4918-825e-136059bc3ede/behavior-tree-user-guide-behavior-tree-01-1.png)

Or by switching over to **Behavior Tree Mode**:

Click the **Behavior Tree** tab in the upper-right corner of the **Behavior Tree Editor**. 

![Click the Behavior Tree tab in the upper-right corner of the Behavior Tree Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46cb03fe-fd49-40b4-979e-f0e94ed1c99e/behavior-tree-user-guide-behavior-tree-02-1.png)

To switch over to **Behavior Tree Mode**, you will need to have a currently opened **Behavior Tree** asset and are switching from **Blackboard Mode**. 

### Assigning a Blackboard

In order for the **Behavior Tree** to access a **Blackboard**, you must assign a **Blackboard** asset: 

Select the **Root** node in the graph (or deselect all nodes), then in the **Details** panel, set your desired **Blackboard Asset**. 

![In the Details panel set your desired Blackboard Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ddf1e7c-b16f-4cda-9590-96d19d915b11/behavior-tree-user-guide-behavior-tree-03-1.png)

After assigning a **Blackboard**, the **Blackboard** panel will update with its associated **Blackboard Keys**.

![The Blackboard panel will update with its associated Blackboard Keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e440b4e9-4999-41f5-850d-83c3acbba239/behavior-tree-user-guide-behavior-tree-03b-1.png)

### Working with Nodes

To add **Composites** or **Tasks** to the graph of your **Behavior Tree**, right-click the graph to bring up the context menu and select your desired node. 

![Right-click the graph to bring up the context menu and select your desired node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28ba62ce-9a5a-4f86-aec4-62209aac45f2/behavior-tree-user-guide-behavior-tree-nodes.png)

Only **Composite** nodes can be connected to the **Root** node of a **Behavior Tree**.

You can also drag off a node and select a node to add from the context menu. 

![You can also drag off a node and select a node to add from the context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89ee8753-3935-43d8-9267-dfd88f911b43/behavior-tree-user-guide-behavior-tree-drag-add.png)

To remove nodes from the graph, select a node (or nodes) and press **Delete** (or right-click and select **Delete**). 

![To remove nodes from the graph select a node or nodes and press Delete or right-click and select Delete](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/106ae953-ff8d-49e3-85b4-bbe1acd5c175/behavior-tree-user-guide-behavior-delete.png)

To connect nodes together, left-click and drag from the output pin, to input pin on another node. 

![To connect nodes together left-click and drag from the output pin, to an input pin on another node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51740ede-4ab1-449d-b9f3-bb9c2eb26be7/behavior-tree-user-guide-behavior-tree-connect-nodes.png)

Connecting nodes in **Behavior Trees** only work by connecting an output to an input (you cannot connect from an input to an output).

To disconnect nodes, right-click a node (or define a selection of nodes) and select your desired **Break All Pin Link(s)** method. 

![To disconnect nodes right-click a node or define a selection of nodes and select your desired Break Link(s) method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2793ba1b-a11f-4752-a80d-f4a1c74c915e/behavior-tree-user-guide-behavior-tree-break-links.png)

**Break All Pin Link(s)** can be used to break a single link or multiple nodes that are pinned. **Break link to**... will break the connection to the specified node. 

You can also press alt + left-click on an input or output pin to break the connection.

To edit a node, select a node, then in the **Details** panel, you can adjust its properties.

![Select a node and in the Details panel you can adjust its properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25eb218a-bf0d-49f8-aadc-57d4265f2fda/behavior-tree-user-guide-behavior-tree-node-details.png)

You can also copy and paste selected nodes and their settings. To do this, select a node (or drag a selection box around a selection of nodes) then press ctrl+c (to copy) and ctrl+v (to paste). 

![To copy or paste a node select a node  then press ctrl+c to copy and ctrl+v to paste](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e667e07-664b-4012-a562-19bf50d1ca0f/behavior-tree-user-guide-copy-paste-nodes.png)

### Node Decorators and Services

You can add **Decorators** or **Services** to a node in your **Behavior Tree** graphs from the node context menu.

To do this, right-click a **Composite** or **Task** node, then select the **Decorator** or **Service** you want to add to the node. 

![To do this right-click a Composite or Task node then select the Decorator or Service you want to add to the node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59bac722-f523-4294-8820-d7c37667edfd/behavior-tree-user-guide-right-click-context.png)

To remove a **Decorator** or **Service** from a node, select a **Decorator** or **Service** then press the **Delete** key or use the right-click context menu. 

![To remove a Decorator or Service from a node select a Decorator or Service then press the Delete key or use the right-click context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3efef34c-77b7-4450-afde-70dcbc70ae52/behavior-tree-user-guide-delete-context.png)

To edit a **Decorator** or **Service** attached to the node, first, select the **Decorator** or **Service**, then you can adjust your desired properties in the **Details** panel. 

![To edit a Decorator or Service attached to the node first select the Decorator or Service then you can adjust your desired properties in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b68ac0ec-9fdd-4e0c-a4e7-2b05be0c3c37/behavior-tree-user-guide-decorator-details.png)

**Composite** **Decorators** that are added to a node, can be opened up for editing. 

To open a Composite Decorator, double-click a **Composite Decorator** to open a graph that returns a Boolean (true or false) value. 

Click image for full view

Any **Task**, **Decorator**, or **Service** created from the toolbar, can be opened up in **Blueprint** for editing.

After creating a custom **Task**, **Decorator**, or **Service** and adding it to your graph, double-click it to open it for editing: 

![After creating a custom Task Decorator or Service and adding it to your graph double-click it to open it for editing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0dbbccd-7990-4154-b768-0f221680e6fc/behavior-tree-user-guide-user-generated.png)

You can also open any custom **Task**, **Decorator**, or **Service** in the **Content Drawer**.

Double-click a custom **Task**, **Decorator**, or **Service** in the **Content Drawer** to open it in **Blueprint** for editing. 

![Double-click a custom Task Decorator or Service in the Content Drawer to open it in Blueprint for editing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a124079-1af0-4e79-b28b-22a7750a5895/behavior-tree-user-guide-content-drawer.png)

You can also copy **Decorators** or **Services** and paste them onto other nodes.

Select a Decorator or Service and press ctrl+c (to copy) and ctrl+v (to paste) onto another node. 

![Select a Decorator or Service and press ctrl+c to copy and ctrl+v to paste onto another node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56bf7a47-cc6f-477d-ba1e-992dfc1b4609/behavior-tree-user-guide-decorators-services.png)