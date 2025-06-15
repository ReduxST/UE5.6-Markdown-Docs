# File Logging Analytics Provider

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/file-logging-analytics-provider-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/file-logging-analytics-provider-for-unreal-engine)  
**Processed:** 2025-06-14 16:23:36

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a516355a-76ac-4d3c-8cba-1df99fe8f9b3/image00.png)

This provider is used to write analytics API calls to disk in JSON format. The reason to use this provider is for debugging the analytics process. It writes the data to the `Saved/Analytic`s folder giving each file a unique name that ends in `.analytics`. You can then compare the data saved in that file to the events on your analytics provider's dashboard to make sure all of the data is being processed. There aren't any special configuration settings for this provider.

This provider writes each session's data to disk which will cause ever-growing data in a released game or app. We recommend that you only use this provider for development and don't include it in your released product.

The image below shows files created when testing the 4.8 API additions.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be69b647-635a-437e-b95e-8a54ccde7608/image01.png)