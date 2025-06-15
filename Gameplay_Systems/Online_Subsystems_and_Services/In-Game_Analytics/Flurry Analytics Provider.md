# Flurry Analytics Provider

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/flurry-analytics-provider-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/flurry-analytics-provider-for-unreal-engine)  
**Processed:** 2025-06-14 16:24:02

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e04d1249-b8c1-4d37-a7d8-535d844ea304/flurry.png)

[Flurry](http://www.flurry.com) is a widely used free analytics service. Because it is so widely used, it can compare your app's data to other applications in the same category. This lets you quickly get a feeling of how your game is doing and areas you might need to do some work. To use their service, you must register at their site, get an application key that uniquely identifies your app, and download the libraries which get compiled into the Flurry plugin. See the plugin's corresponding `<PlatformAndName>.Build.cs` file to see where the libraries and headers are expected to be placed.

## Configuration

Once you have done the prerequisites and have successfully built the plugin for the target platform, you can configure the plugin for your game. As of 4.8, there is only one configuration property to set: the key that uniquely identifies your game. The snippet below shows a theoretical configuration for Flurry. As with all analytics providers, the configuration data goes in your `DefaultEngine.ini` file.

```
	`[Analytics] 	FlurryApiKey=RANDOM34LETTERS4511`
Copy full snippet
```
\[Analytics\] FlurryApiKey=RANDOM34LETTERS4511