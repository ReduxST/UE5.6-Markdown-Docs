# Pain-Causing Volume Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pain-causing-volume-actor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pain-causing-volume-actor-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:27

---

In addition to the properties that can be assigned from a Physics Volume, the Pain Causing Volume also has its own set of specific properties outlined below.

| Property | Description |
| --- | --- |
| **Pain Causing** | Whether the volume currently causes damage or not. |
| **Damage Per Sec** | Damage done per second to the Actors in the volume when Pain Causing is enabled. |
| **Damage Type** | This determines the type of damage done to the Actor. |
| **Pain Interval** | This is the amount of time, in seconds, between applied damage when Pain Causing is enabled. |
| **Entry Pain** | Determines whether or not damage will be applied immediately upon entering the volume, assuming that **Pain Causing** is enabled. This damage is in addition to the recurring damage applied based on the **Pain Interval**. |