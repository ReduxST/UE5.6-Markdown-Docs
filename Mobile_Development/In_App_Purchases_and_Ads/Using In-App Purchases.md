# Using In-App Purchases

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-in-app-purchases-in-unreal-engine-projects-for-mobile-devices](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-in-app-purchases-in-unreal-engine-projects-for-mobile-devices)  
**Processed:** 2025-06-14 16:59:23

---

In-app purchases enable you to offer additional content and features to players. This can be used as a means of monetizing a free-to-play game or providing additional paid content for your game.

## Configuration

See the apropriate platform-specific page below for details on configuring in-app purchases for each platform:

-   [Using In-App Purchases on Android](/documentation/en-us/unreal-engine/how-to-use-in-app-purchases-in-unreal-engine-projects-on-android)

## Reading Purchase Information

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5a9e2f0-87fa-4f22-9c57-bc28ffc81abd/image_3.png)

You can read the in-app purchase information using the **Read In-App Purchase Information** Blueprint node (or associated C++ function call). Like most other online subsystems functions, it takes a Player Controller as input, as well as an array of your product identifiers. Note that Make In-App Purchase below takes a single identifier, while Read can process an array of information. The function returns an array of In App Purchase structs, and each element of the array can be broken out to get the name, description, price, and other data to display in your UI or use in your gameplay logic.

## Completing a Purchase

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ef98ff4-6261-4f11-ba1c-e6f8cd0b9505/image_4.png)

To make an in-app purchase, use the **Make an In-App Purchase** Blueprint node (or associated C++ function call). It takes the Player Controller as input, as well as a Product Request struct. A Product Request is just the product identifier from iTunes Connect or the Google Play Developer console (in this case, match3theme\_night), as well as whether or not the product is consumable.

The **Make an In-App Purchase** node is latent, so any gameplay behavior you want to have rely on whether the purchase succeeds or fails should use those two execution pins. They will only execute after a response has come back from the online service. The node also returns the completion status of the purchase (such as Success, Failed, Restored) and the detailed In App Purchase Information struct.

There is a non-latent version of this function (the Blueprint node will display without the clock). The exit execution pin here does not wait for a response from the online service, and you will generally want to use the latent version.

## Restoring Purchases

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e734fff5-8605-44f4-9b09-efe7be05d310/image_5.png)

To restore purchases, use the **Restore In-App Purchases** Blueprint node (or associated C++ function call). It only takes in the Player Controller, and returns an array of all the purchase information associated with that Player Controller. You can then process that array to compare against the particular Identifier (or Identifiers) that your gameplay logic needs.