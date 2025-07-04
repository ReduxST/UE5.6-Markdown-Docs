# Audio Volume Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-volume-actor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-volume-actor-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:02

---

Several properties can be adjusted from the **Details** panel on this volume to allow for more control over its effects as seen below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27a57d29-946c-4210-9ff9-9062419139eb/audiovolume.png)

| Property | Description |
| --- | --- |
| **Priority** | In the event of overlapping volumes, the highest priority volume will be used. The order is undefined if two or more overlapping volumes have the same priority. |
| **Apply Reverb** | Determines if the reverb settings should be used. |
| **Reverb Effect** | This is the reverb asset to use for the volume. |
| **Volume** | This is the overall volume level of the reverb effect. |
| **Fade Time** | This is the time (in seconds) to fade from the current reverb settings into the volumes setting. |
| **Enabled** | Determines whether the volume is currently enabled and is able to affect sounds. |

**Ambient Zone Settings** define how Sound Actors located inside the associated Audio Volume will be altered by the Player's location. The Ambient Zone Settings can be adjusted from the **Details** panel.

| Property | Description |
| --- | --- |
| **Exterior Volume** | The final volume of exterior sounds when the player is inside the volume. |
| **Exterior Time** | Time to fade to new exterior volume in seconds. |
| **Exterior LPF** | Lowpass Filter multiplier applied to exterior sounds when inside (1.0 to apply the maximum LPF). |
| **Exterior LPFTime** | Time to fade to new Lowpass Filter level in seconds. |
| **Interior Volume** | The final volume of interior sounds when the player is outside the volume. |
| **Interior Time** | Time to fade to new interior volume in seconds. |
| **Interior LPF** | Lowpass Filter multiplier applied to interior sounds when outside (1.0 to apply the maximum LPF). |
| **Interior LPFTime** | Time to fade to new Lowpass Filter level in seconds. |