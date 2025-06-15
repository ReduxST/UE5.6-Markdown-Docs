# In-Game Analytics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-game-analytics-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-game-analytics-for-unreal-engine)  
**Processed:** 2025-06-14 16:30:53

---

In order to get data on how your game is performing, you must use an analytics provider to capture and process the data. For those without a homegrown solution, there are plenty of options available, from free services to paid ones. Unreal Engine provides an abstract interface for communicating with one or more analytics providers. Your game uses the interface, and analytics providers offer a backing implementation. In some cases, Epic has built the backing provider already. Previously, Epic Games provided an implementation to multicast analytics events, relaying them to multiple providers. For providers, there is support of providers that support [Swrve](http://www.swrve.com), a paid service, and support for Flurry.

More provider plugins will become available over time, and it is also feasible to add your own provider if needed.

## Implementing Game Analytics

## Providers