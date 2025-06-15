# Audio Gameplay Volumes Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-gameplay-volumes-quick-start](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-gameplay-volumes-quick-start)  
**Processed:** 2025-06-14 16:08:42

---

Using **Audio Gameplay Volumes** you can define physical regions that apply effects to sounds, relative to the listener's position.

In this guide, you'll learn how to set up a basic Audio Gameplay Volume with a **Reverb** component to simulate sound waves bouncing within the space.

## Prerequisites

-   A brand new project created using the [First Person Template](/documentation/en-us/unreal-engine/unreal-engine-templates-reference).
    
    ![Project Template](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ded5c4a-4063-4ace-816f-a0e726c954c1/project_template.png)
-   The Audio Gameplay Volumes plugin is disabled by default. To enable it, open the **Plugin** panel by selecting **Edit > Plugins**, use the search bar to find the plugin, and then click the corresponding checkbox.
    
    ![Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/330a1e72-070a-412e-b73c-4525f43aba3c/plugin.png)

## 1 - Set Up the Sound Class

Audio Gameplay Volumes require **Sound Wave** assets as part of a properly set up **Sound Class** in order to function.

For more information on Sound Classes, see [Sound Classes](/documentation/en-us/unreal-engine/sound-classes-in-unreal-engine).

1.  The First Person Template has a single Sound Wave asset which plays when you fire the weapon. Using the **Content Browser**, go to **Content/FPWeapon/Audio**.
2.  Double-click the **FirstPersonTemplateWeaponFire02** Sound Wave to open the **Sound Wave Details** panel.
    
    ![Sound Wave in Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46496425-c638-4ee6-9545-ba1d55d0a55c/sound_wave_in_browser.png)
3.  Click the dropdown for **Sound > Class**.
    
    ![Sound Wave Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/071d698d-6e79-49de-9537-7defdaf50ab8/sound_wave_details0.png)
4.  Select **Sound Class** in the context menu to create a new asset.
    
    ![Create New Sound Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d6bd760-5b78-4595-9360-0329d8a1ef6e/create_new_sound_class.png)
5.  Enter a name for the new Sound Class and save it to your **Content** folder.
6.  Double-click on your new **Sound Class** to open the **Sound Class Details** panel.
    
    ![Sound Wave Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15317af5-e6df-4f11-927e-f537b106ff02/sound_wave_details1.png)
7.  Enable **Routing > Apply Ambient Volumes** to allow sounds associated with this Sound Class to be used with Audio Gameplay Volumes.
8.  Input 1.0 for the **Submix > Default 2DReverb Send Amount** to send 100% of the sound in the Sound Class to the **Master Reverb Submix**.
    
    ![Sound Class Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a36ac2a8-970b-4b3c-af0a-849d74c7a082/sound_class_details.png)
9.  Save the Sound Class and Sound Wave assets.

## 2 - Place the Audio Gameplay Volume

1.  Place an **AudioGameplayVolume** in your level by using the **Place Actors** panel or by clicking **Quick Add** in the **Level Editor Toolbar** and selecting **Volumes > AudioGameplayVolume**.
    
    ![Place Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/060a3a2a-3eaf-4415-bdb9-888795ad77de/place_actor.png)
2.  Position the volume in the level so that your character can move into and out of it, such as directly over the `BP_Pickup_Rifle`.
    
    ![Volume In Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca5dd41f-7021-42f9-8065-0c659befbf0b/volume_in_level.png)

## 3 - Add the Reverb Component

Audio Gameplay Volume functionality is driven by components. Each volume may have any number of these components which affect the sounds that happen inside or outside of the volume, relative to the listener. For this example, add a Reverb component to your volume to make the weapon fire sound reverberate while the player is inside it.

1.  With the **Audio Gameplay Volume** selected, click the **Add Component** button in the **Details** panel.
    
    ![New Volume Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7dea19f-f5be-4936-ba1b-ae854a182441/volume_details.png)
2.  Select the **Reverb** component under the **Audio Gameplay Volume** section of the context menu.
    
    ![Add Reverb Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5ec773a-f202-4819-bd3b-e5354a09f8fd/add_reverb_component.png)
3.  Input 1.0 for **Reverb > Volume** to increase the loudness of the effect.
4.  Input 0.0 for **Reverb > Fade Time** to apply the effect immediately when entering the volume.
    
    ![Reverb Component Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edc1f2da-aa83-4c96-8590-14c895e43b56/reverb_component_details0.png)

## 4 - Set Up the Reverb Effect

The Reverb component applies its effect using a **Reverb Effect** asset, so you'll need to create one.

1.  With the new **Reverb** component selected, click the dropdown for **Reverb > Reverb Effect**.
    
    ![Reverb Component Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6596a5f-1d81-4e40-9b75-ce7b6337cd7f/reverb_component_details1.png)
2.  Select **Reverb Effect** in the context menu to create a new asset.
    
    ![Create New Reverb Effect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd9c0c33-8fdb-4772-9d81-ae7f2843c930/create_new_reverb_effect.png)
3.  Enter a name for the new Reverb Effect and save it to your **Content** folder.
4.  Double-click on your new **Reverb Effect** to open the **Reverb Effect Details** panel.
    
    ![Reverb Component Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1e530e8-e1f3-473f-afce-03bfe9e3aa52/reverb_component_details2.png)
5.  Input 1.0 for **Late Reflections > Gain** to amplify the signal and make the effect easier to hear.
    
    ![Reverb Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eafde20b-2280-4309-8df5-05302589cf8c/reverb_details.png)
6.  Save the Reverb Effect asset.

## 5 - Play

1.  Click the **Play Level** button in the **Level Editor Toolbar**.
2.  Move your character into the `BP_Pickup_Rifle` to pick up the weapon.
3.  Left-click to fire while inside or outside of the volume and listen to the difference in the sound.

## 6 - On Your Own!

Now that you've finished creating a basic Audio Gameplay Volume, consider taking it even further.

Try adding these other Audio Gameplay Volume component types to a new or existing volume:

-   **Submix Override**: Adds a **Submix Effect Chain** to a **Sound Submix**. When the listener enters the volume, this effect applies to all sounds regardless of whether they are inside or outside of the volume.
-   **Submix Send**: Sends the audio to a **Sound Submix**. This effect applies to sounds inside of the volume, and can be configured to apply while the listener is either outside or inside.
-   **Attenuation**: Interpolates the audio's current volume (loudness) to a target volume (loudness). You can configure the effect to apply to sounds inside of the volume while the listener is outside, or the other way around.
-   **Filter**: Applies a low pass filter to the audio. You can configure the effect to apply to sounds inside of the volume while the listener is outside, or the other way around.

You will need at least one sound positioned away from the player to hear the effects of some of the component types, such as **Attenuation** and **Filter**. The First Person Template doesn't come with any sounds set up this way by default, so some additional work is required.

There are a lot of ways to do this, but for a simple option, try importing an ambient sound file as a **Sound Wave** asset and then place it either inside or outside of the volume within the level. See [Importing Audio Files](/documentation/en-us/unreal-engine/importing-audio-files) for information on how to import audio files.