# Using Google Play Services Leaderboards

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-google-play-services-leaderboards-in-unreal-engine-projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-google-play-services-leaderboards-in-unreal-engine-projects)  
**Processed:** 2025-06-14 16:59:17

---

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75b16468-9d11-4f65-96c5-bc45554d7707/android-leaderboard-banner.png "Banner Image")

## Configuration

Please see [Leaderboards | Play Games Services | Google Developers](https://developers.google.com/games/services/common/concepts/leaderboards) for information on setting up the Google Play Game Services for your application.

For your Unreal Project:

1.  In the **Edit** menu in **Unreal Editor**, select **Project Settings** to view the configuration options for your project.
    
    ![Open Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39ade7f6-8b96-43c2-84be-8be33ce7846b/ue5_1-01-open-project-settings.png "Open Project Settings")
2.  On the left, Select the **Platforms: Android** tab. Navigate to the **Google Play Services** section and configure project for Google Play services platform.
    
    Click to full view
    
3.  In the **Google Play Services** section, check the **Enable Google Play Support** option.
    
4.  Enter the App ID for your game in the **Games App ID** field.
    
5.  Enter your Google Play License Key in the **Google Play License Key** field.
    
6.  Add an element to the **Leaderboard Map**.
    
7.  In the **Leaderboard Map** you'll need to enter a **Name** that is only used within your Unreal Project and the **Leaderboard ID** you set up in your Google Play Services.
    
    Click to full view
    
    All of these values are available in the Google Play Developer Console for your App and Game Services.
    

Since the **Name** value in the achievement map is only a mapping for the Google Play Services **Leaderboard ID**, and iOS is directly referred to by their **Leaderboard Reference**, and if you are releasing on both Android and iOS platforms, enter the Leaderboard Reference from your iOS Game Center settings as your **Name** so you only have to call one node regardless of platform.

## Reading from a Leaderboard

The **Read Leaderboard Integer** node will request from the platform's game service (currently iOS Game Center, or Google Play Services), the value stored on the given **Stat Name** for the provided **Player Controller**.

Note that it is a **latent** node, and thusly has a number of execution output pins. The top most is a "pass through," that works like any other execution output pin. The other two pins (**On Success**, and **On Failure**) will execute when the online service returns (or fails to return) a value. The value of **Leaderboard Value** before a successful return (or if the service fails to get a response) will be `0`.

**In Blueprints:**

The example below is from the **Global Game Instance** Blueprint in the Unreal Match 3 sample game. In these few nodes we're calling the **Read Leaderboard Integer** node for the Player Controller at Player Index 0 on the Stat Name (Leaderboard) "Match3HighScore":

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36c3ccc9-52e7-44fe-b2e6-4570fbb9e93f/readleaderboard.png)

## Writing to a Leaderboard

The **Write Leaderboard Integer** node will send the given integer **Stat Value** to the leaderboard specified in **Stat Name** for the provided **Player Controller**.

**In Blueprints:**

The example below is from the **VictoryScreen** Blueprint in the Unreal Match 3 sample game. When the victory (or defeat) screen is shown, it will check to see if on load Unreal Match 3 was able to retrieve a high score, then if it was able to it will submit the latest high score to the leaderboard. There is some additional checking before this to see if the new highscore is more than the one that was pulled during the app startup, but even if that wasn't there, the iOS and Android leaderboard systems will only accept values greater than what they currently store.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f937f4d5-9895-4020-850b-a66f06f1b995/writeleaderboard.png)

## Showing the Platform Specific Leadboard

The **Show Platform Specific Leaderboard Screen** will show the leaderboard specified by **Category Name** on the device.

**In Blueprints:**

The example below is from the **GameOverButtons** Blueprint Widget in the Unreal Match 3 sample game. When the **ShowScores** button is pressed, the game will attempt to show the leaderboard.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5219f88e-712f-402c-9cbf-963cd4c29efe/showleaderboard.png)