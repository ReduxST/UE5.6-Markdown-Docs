# State Tree Selectors Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/state-tree-selectors-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/state-tree-selectors-overview)  
**Processed:** 2025-06-14 16:52:09

---

## State Tree Selectors Overview

A StateTree contains states arranged in a tree structure, with parent and child states. As the StateTree runs, it starts at the root state and moves down, selecting child states based on their **selection behavior** and enter conditions. This document provides an overview of the selection behaviors available for each state.

StateTree come with the following state selection behaviors for their child states:

![State Tree state selection behaviors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38d2feea-20f1-4c11-8af2-f1a937b55714/state-tree-selectors-overview-1.png)

| Selection Behavior | Description |
| --- | --- |
| Try Enter | A state is selected even if it has child states. |
| Try Select Children in Order | Try to select the first child state in the order they appear in the child list. If no child states are present, it behaves like Try Enter. |
| Try Select Children at Random | Shuffle the order of the child states and try to select the first child state whose Enter Conditions are met. If no child states are present, it behaves like Try Enter. |
| Try Select Children with Highest Utility | Try to select the child state with the highest utility score. If two or more states have the same score, select the first state on the list. |
| Try Select Children at Random Weighted by Utility | Randomly pick a child state by using each state’s utility score. The probability of selecting each state is the normalized utility score. |
| Try Follow Transitions | When a state is considered for transition, try to trigger the transitions instead. |

## State Tree Utility Selectors

These selectors are based on the child states’ utility scores. Each child state outputs a score when the parent state starts selecting the child state to enter. The parent selects the state with the highest utility among all the child states.

![Utility selector components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dc66b61-d58f-4885-bd55-822ea9942d67/state-tree-selectors-overview-2.png)

The utility selectors have the following components:

-   (1) Consideration
-   (2) Logical operators (AND, OR)
-   (3) Indent
-   (4) Weight

**Consideration** is a new type of StateTree node that represents an aspect the user wants to consider when scoring the state. Considerations output a normalized score between 0 and 1.

For instance, you might have an Enemy Low Health Consideration that outputs a score that increases as the health value decreases. You could also have a Consideration that outputs a fixed score based on certain conditions, such as whether the enemy is nearby the player.

Multiple Considerations are combined together using **Logical Operators**. There are two types of operators currently available: **AND** and **OR**.

The AND operator outputs the lower of the two Consideration input scores. While the OR operator outputs the higher of the two Consideration input scores. All the Consideration scores are combined and turned into a normalized score (0 -1).

In the case of multiple Considerations, the **indent** is used to control the operator precedence. In the example above, the AND operator will be calculated before the OR operator.

The combined normalized score of the Considerations will then be scaled (multiplied) by the **Weight** to give the final score of this state. By default, the Weight value is 1, in which case the final score will be the same as the combined normalized score. The user can modify the Weight value to give additional bias towards or against a child state on top of its Considerations. The final score scaled by Weight won’t be normalized.

In the example image above, suppose Distance2Med outputs a score of 0.6, Health outputs a score of 0.4, and SearchForMed outputs a score of 0.2, and a Weight of 1. The final utility score for that state is as follows:

Weight *Max(Distance2Med , Min(Health , SearchForMed )) 1* Max(0.6, Min(0.4, 0.2)) = 0.6

### Consideration Types

#### Float Input Consideration

![Float Input Consideration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2ea46a8-5542-4496-adab-5c34afd64cb5/state-tree-selectors-overview-3.png)

The **Float Input Consideration** uses a **Response Curve** to output the score. The curve can be edited directly in the **Details** panel, or you can input an **external Float Curve** asset.

The **Input** can be bound to a variable and is normalized by the Input Range. This normalized value is used by the Response Curve to obtain a normalized value. Any portion of the curve outside of the 0 to 1 values will have no effect on the value.

#### Enum Input Consideration

![The Enum Input Consideration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d5a81b0-d215-46fe-83fa-6f38c4eed709/state-tree-selectors-overview-4.png)

The **Enum Input Consideration** uses an Enumeration-Score lookup table to output its score. The **Input** is bound to an external Blueprint Enumeration asset type and the user can configure the enum values and their scores. Any missing value in the table will output a score of 0.

#### Constant Input Consideration

![The Constant Input Consideration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f3ab789-4545-48ba-8798-d55a4e9f07e0/state-tree-selectors-overview-5.png)

The **Constant Input Consideration** outputs a constant score. This Consideration can be used with the **Try Select Children At Random Weighted by Utility** to mimic a weighted random selection behavior.

### State Tree Utility Selection Behaviors

#### Try Select Children With Highest Utility

![Try Select Children With Highest Utility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/775ebd95-03a6-472f-af6a-1c2f21b402c3/state-tree-selectors-overview-6.png)

The **Try Select Children With Highest Utility** Selection Behavior selects the child state where its Enter Conditions are met and has the highest utility score among all child states.

#### Try Select Children At Random Weighted by Utility

![Try Select Children At Random Weighted by Utility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a63ab79-ba93-4b16-ba57-12952a2de3b8/state-tree-selectors-overview-7.png)

The **Try Select Children At Random Weighted by Utility** Selection Behavior selects a random child state where its Enter Conditions are met. The probability of each child state being selected is weighted by their utility score.