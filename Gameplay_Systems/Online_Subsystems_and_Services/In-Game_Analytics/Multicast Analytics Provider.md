# Multicast Analytics Provider

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-analytics-provider-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-analytics-provider-for-unreal-engine)  
**Processed:** 2025-06-14 16:37:34

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d5b2369-8384-40e6-8097-9d10a69e74be/image00.png)

The multicast provider sends analytics events to multiple providers. This allows you to use multiple analytics providers easily, since it will take the calls and hand them to each registered analytics providers in turn without you having to manually do this dispatching work. Having multiple analytics providers is desirable since each provider has different strengths and weaknesses. By using multiple providers, you can get all of the features that you need to run your app business.

## Configuration

Configuring the provider is straightforward. It just needs to know the list of providers that you want data sent to. This list is provided as a comma-delimited list of the module names for the providers. In the example below, the AnalyticsMulticast provider is specified as the default provider for the application. Then, the list of providers that it sends the data to is specified using a comma-delimited list as mentioned before. As with all analytics providers, the configuration data goes in your `DefaultEngine.ini` file.

\[Analytics\] ProviderModuleName=AnalyticsMulticast ProviderModuleNames=FileLogging,IOSFlurry,IOSApsalar