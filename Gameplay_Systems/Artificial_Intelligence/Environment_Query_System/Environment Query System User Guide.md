# Environment Query System User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:19

---

This page covers the typical workflows for enabling, creating, and editing Environmental Query System (EQS) assets.

## Enabling EQS

Before you can start working with EQS, you will need to enable it from the **Project Settings** menu.

-   Under the **Settings > Plugins** section, enable the **Environment Query Editor** option if necessary.
    
    ![Enable the **Environment Query Editor** option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46b38539-f012-4633-94c6-98cc6eb1c7d3/environment-query-system-user-guide-enable-environment-query-system.png)

## Creating an EQS Query

To create an EQS Asset:

1.  Click the **+Add** button in the **Content Drawer**, then under **Artificial Intelligence**, select **Environment Query**.
    
    ![Click the +Add button in the Content Drawer, then under Artificial Intelligence, select Environment Query](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f0f9710-5fd1-496b-8040-3fe6225c1ad0/environment-query-system-user-guide-create-environment-query-system-asset.png)
2.  Enter in a name for your new EQS asset.
    
    ![Enter in a name for your new EQS asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5715a20e-d7e0-4e2b-93cc-b00d194b6085/environment-query-system-user-guide-enter-environment-query-system-name.png)

In addition to Environment Query, you can create custom [Generator](/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine#customgenerators) and [Context](/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine#envquerycontext_blueprintbase) Blueprint assets in the Content Drawer.

## Editing an EQS Query

Inside the EQS asset, you can use a [Generator](/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine) to produce the locations or Actors that will be tested and weighted, provide a [Context](/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine) or frame of reference, and [Tests](/documentation/en-us/unreal-engine/eqs-node-reference-tests-in-unreal-engine) to determine which item from the Generator is the best option. The following section will illustrate how to create each of these within the EQS asset.

To add a Generator:

-   Right-click in the EQS Graph and select your desired Generator type.
    
    ![Right-click in the EQS Graph and select your desired Generator type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/989f0500-8293-402b-9c96-68f69edc6832/environment-query-system-user-guide-add-generator.png)
    
    After adding a Generator, drag off the Root node and connect it to your Generator.
    
    ![Drag off the Root node and connect it to your Generator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd67cb7b-bad3-404e-a556-2098d2595d95/environment-query-system-user-guide-connect-generator.png)
    
    While you can have more than one Generator connected to the Root, only the left-most Generator is used in the Query.
    

To add a Test:

-   Right-click on a Generator and select a Test to add.
    
    ![Right-click on a Generator and select a Test to add](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/754b8e94-3001-4ef1-9e63-a89ba49fee26/environment-query-system-user-guide-add-test.png)
    
    After adding a Test, it will appear attached to the Generator. Select the Test to adjust properties in the **Details** panel.
    
    ![Select the Test to adjust properties in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bddc702b-b2ef-4703-9929-3b7502aba83e/environment-query-system-user-guide-add-test-details.png)

To define a Context:

-   In the **Details** panel for a Test, change the **EnvQueryContext** to your desired Context.
    
    ![Change the EnvQueryContext to your desired Context](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac7d5e8c-0e0d-4ccd-9fd8-d838fbbe1c4e/environment-query-system-user-guide-context.png)
    
    The property name may vary based on the type of Test. Please see [Tests](/documentation/en-us/unreal-engine/eqs-node-reference-tests-in-unreal-engine) for more information.
    

## Previewing an EQS Query

You can preview the results of an EQS Query inside the Editor, where weighted/filtered results will be represented by debugging spheres.

![You can preview the results of an EQS Query inside the Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f17712c6-410f-4349-a9ce-69190410d529/environment-query-system-user-guide-preview.png)

In the image above, we debug an EQS Query that returns a location that provides a line of sight to the Player Character in the Level.

Please see [AI Debugging](/documentation/en-us/unreal-engine/ai-debugging-in-unreal-engine) or [EQS Testing Pawn](/documentation/en-us/unreal-engine/environment-query-testing-pawn-in-unreal-engine) for more information.

## Using EQS with Behavior Trees

After creating EQS Query, you can run the query inside a [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) as part of a **Task.**

1.  Inside a Behavior Tree, right-click and add the **Run EQS Query** Task node.
    
    ![Right-click and add the Run EQS Query Task node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25201be1-0b2b-428c-b6ad-03943a3b007e/environment-query-system-user-guide-run-environment-query-system.png)
2.  For **Run EQS** **Query**, assign the **Query Template** (desired EQS asset) to execute, and the **Blackboard Key** it should return.
    
    ![Assign the Query Template to execute and the Blackboard Key it should return](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38f89b82-90c9-4045-9a27-a39746cf9886/environment-query-system-user-guide-edit-environment-query-system-behavior-tree.png)
    
    The Blackboard Key that is returned will be the highest weight result (Object or Vector). In the example above, we have an EQS Query that is used to locate the Player and provide that location back to a Blackboard Key called  **MoveToLocation.** 
    
    You can optionally add parameters to pass to the EQS asset through the **Query Config** option.
    

## Using EQS with Native Code

While EQS Queries generally run within Behavior Trees, you can also use them directly from native code. The following example shows a hypothetical query that finds a safe place for a character or item to spawn within a specific zone:

```
	`// These names must match the variable names used in the query 	static const FName SafeZoneIndexName = FName(TEXT("SafeZoneIndex")); 	static const FName SafeZoneRadiusName = FName(TEXT("SafeZoneRadius"));  	// Run a query to find a safe spawn point based on the zone's index and a safety radius 	bool AMyActor::RunPlacementQuery(const UEnvQuery* PlacementQuery) 	{ 		if (PlacementQuery) 		{ 			// Set up a query request 			FEnvQueryRequest QueryRequest(PlacementQuery, this);  			// Set query parameters 			QueryRequest.SetIntParam(SafeZoneIndexName, SafeZoneIndexValue); 			QueryRequest.SetFloatParam(SafeZoneRadiusName, SafeZoneRadius);  			// Execute the query 			QueryRequest.Execute(EEnvQueryRunMode::RandomBest25Pct, this, &AFortAthenaMutator_SpawningPolicyBase::OnEQSSpawnLocationFinished);  			// Return true to indicate that we started the query 			return true; 		}  		// Return false to indicate that we failed to start a query 		return false; 	}`
Copy full snippet
```
// These names must match the variable names used in the query static const FName SafeZoneIndexName = FName(TEXT("SafeZoneIndex")); static const FName SafeZoneRadiusName = FName(TEXT("SafeZoneRadius")); // Run a query to find a safe spawn point based on the zone's index and a safety radius bool AMyActor::RunPlacementQuery(const UEnvQuery\* PlacementQuery) { if (PlacementQuery) { // Set up a query request FEnvQueryRequest QueryRequest(PlacementQuery, this); // Set query parameters QueryRequest.SetIntParam(SafeZoneIndexName, SafeZoneIndexValue); QueryRequest.SetFloatParam(SafeZoneRadiusName, SafeZoneRadius); // Execute the query QueryRequest.Execute(EEnvQueryRunMode::RandomBest25Pct, this, &AFortAthenaMutator\_SpawningPolicyBase::OnEQSSpawnLocationFinished); // Return true to indicate that we started the query return true; } // Return false to indicate that we failed to start a query return false; }