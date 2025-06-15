# Environment Query Testing Pawn

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-testing-pawn-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-testing-pawn-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:20

---

In addition to the [AI Debugging](/documentation/en-us/unreal-engine/ai-debugging-in-unreal-engine) tools, the Environment Query System has a specialized type of **Pawn** class called the **Environment Query System Testing Pawn** (**EQSTestingPawn**) that enables you to check out what your Environment Queries are doing. The exact makeup of your Environment Query will define the size and shape of what is created, but it will always be represented as colored spheres. Spheres that are on the color scale from green to red, indicate some level of the match for the various tests your Environment Query ran. Blue spheres indicate a failure or a boolean-type test that returned false, such as the Trace test.

## Working with the EQS Testing Pawn

After [enabling EQS](/documentation/en-us/unreal-engine/environment-query-system-user-guide-in-unreal-engine#enablingeqs) and creating an [EQS Query](/documentation/en-us/unreal-engine/environment-query-system-user-guide-in-unreal-engine#creatinganeqsquery) you can test the data while in the Editor using the EQS Testing Pawn. 

1.  In the **Content Brawer**, create a new **Blueprint** of the **EQSTestingPawn** class and give it any name.
    
    ![Create a new Blueprint of the EQSTestingPawn class and give it any name in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e66b79ce-48ef-4ab5-800f-3a08bf4cb2af/environment-query-system-pawn-01.png)
2.  Place the **EQSTestingPawn** in the Level, then in the **Details** panel, assign the **EQS Query Template** to test.
    
    Click for full image.
    

Given the experimental nature of the Environment Query System, the EQSTestingPawn can be very processor intensive, and making changes to its active Query Template can cause your system to hang for extremely long times. It's best to clear the Query Template property while making edits to your Environment Query.

Depending upon the content of your query, when you have the EQSTestingPawn selected in the Level, debug spheres will appear in the Level that indicates the value of a match based on your conditions. Below we use the EQSTestingPawn and test a query that yields the best possible position in the Level that provides a line of sight to the Player Character. As we move the EQSTestingPawn around, the spheres update in color and value to indicate the new best match based on the position of the Player and EQSTestingPawn.

## Evaluating Results

When evaluating the results of a Test using the EQSTestingPawn, the colored spheres and values indicate the level of the match an item has at a given location.

-   **Blue Spheres**: These spheres indicate that a Test has failed at that item, so the item is completely un-weighted and culled from the results. This usually occurs when a value is filtered out, such as using a **Distance** Test and filtering out any Item over (or under) a range. If you don't want a value to be culled completely, you can use the **Clamp** options in the scoring section. Below, we have a query that is running to find the line of sight to the Player. We have used a **Visibility** to cull out items where the AI would not have a line of sight to the Player (represented by the blue spheres).

![Blue Spheres](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcf3c56e-41c7-4f89-9076-3a17b12485de/environment-query-system-breakdown-01.png)

-   **Green to Red Spheres**: Spheres range in color from green to red and indicate the desirability of the Item as the best match for the specified Test. Green is more desirable than red and the number shown is the weighted score of the Item. If previewing only one Debug Step, this value will be the final value from the selected Test. Below, we use a query to find the furthest point away from the player regardless of visibility.

![Green To Red Spheres](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3d46bd0-cc20-4834-8ee8-b69952089683/environment-query-system-breakdown-02.png)

## EQS Testing Pawn Properties

With an EQSTestingPawn selected in the Level, the following properties are available inside the **Details** panel. 

| Property | Description |
| --- | --- |
| **Query Template** | The Environment Query that the EQSTestingPawn should use. |
| **Query Config** | Enables you to pass named values into the Environment Query to quickly adjust its settings. |
| **Time Limit Per Step** | 
If this value is set to anything greater than 0.0, it will cause the EQSTestingPawn to stop calculating a step at the time this property is set to. Helps to mitigate making adjustments to the Environment Query while using the EQSTestingPawn. 

Note: This will not reduce the time it takes to calculate the locations for the **Generator**, such as using a large **Simple Grid** with a tight **Density**



 |
| **Step to Debug Draw** | Shows a single debug step. May not map to the order your steps appear in the Environment Query. |
| **Highlight Mode** | Determines if all spheres should be shown at the same size or if the best `5%` or `25%` of spheres should be shown (other spheres will be reduced in size). |
| **Draw Labels** | Enables drawing the weight or reason for failure on the debug spheres in the Viewport. |
| **Draw Failed Items** | Enables the culling of any failed tests, such as when a trace fails to find its target. |
| **Re Run Query Only on Finished Move** | Will only update the debug visualization in the Viewport when you stop moving the EQSTestingPawn. It's advised to keep this enabled unless you are working with a very quick Environment Query. |
| **Should be Visible in Game** | Makes the EQSTestingPawn, and its debug visualization, visible in the running game. |
| **Tick During Game** | Makes the EQSTestingPawn, and its debug visualization, tick during the running game. |
| **Querying Mode** | 

Changes what the debug view shows.

-   **Single Result**: Shows only the result for the item listed in the **Step to Debug Draw** property.
-   **All Matching**: Shows the final, filtered, and weighted score of the entire Environment Query.



 |
| **Nav Agent Properties** | 

Properties that determine how the Pawn navigates. 

-   **Nav  Agent Radius**: Radius of the capsule used for navigation/pathfinding.
-   **Nav Agent Height**: Total height of the capsule used for navigation/pathfinding.
-   **Nav Agent Step Height**: Step height to use, or -1 to use the default value from NavData's config settings.
-   **Nav Walking Search Height Scale**: Scale factor to apply to height of bounds when searching for NavMesh to project to when Nav Walking.
-   **Preferred Nav Data**: This property specifies the Navigation Data class type you want the Testing Pawn to perform its test against.
-   **Can Crouch**: If true, the Pawn is capable of crouching.
-   **Can Jump**: If true, the Pawn is capable of jumping.
-   **Can Walk**: If true, the Pawn is capable of walking or moving on the ground.
-   **Can Swim**: If true, the Pawn is capable of swimming or moving through fluid volumes.
-   **Can Fly**: If true, the Pawn is capable of flying.



 |