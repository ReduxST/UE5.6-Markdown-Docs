# Using a Static Camera

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-static-camera-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-static-camera-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:10

---

Programming Language

×C++

Select an option from the dropdown to see content relevant to it.

In this How-to tutorial you will create a static (or fixed) camera angle that is used for the player's perspective during gameplay in a third person example map, and then you will create a trigger volume which will transition your viewpoint to the new static camera once your character overlaps the volume. Upon completing this tutorial, you can take the process used here and apply it to your own game to set up a fixed perspective for a player.

## Creating The Static Camera Actor

1.  Begin by creating a **New > Games > Third Person > C++** project named **StaticCameras**.
    
2.  Launch the **C++ Class Wizard**, enable the checkbox for **Show All Classes**, then type **CameraActor** within the search field to select and create your new **Camera Actor** class named **ExampleCameraActor**.
    
    [![New C++ Camera Actor class](https://dev.epicgames.com/community/api/documentation/image/fd83b67a-a0c9-42b5-8059-ee8a02d8ebf9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fd83b67a-a0c9-42b5-8059-ee8a02d8ebf9?resizing_type=fit)
    
3.  From the **C++ Class** panel, right click on your **ExampleCamera** and from the dropdown **C++ Class** actions menu select **Create a Blueprint class based on ExampleCameraActor**. Then drag an instance of **BP\_ExampleCameraActor** into the level.
    
    [![Place Actor in level](https://dev.epicgames.com/community/api/documentation/image/41cb576c-8114-408e-9a5a-359c4ff9dd80?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/41cb576c-8114-408e-9a5a-359c4ff9dd80?resizing_type=fit)
    
    Click image to expand.
    

## Level Setup

In order to demonstrate the transition of perspectives between the player's camera and the static camera Actor, you will need to set up the scene. You can accomplish this by modifying some of the static mesh geometry from the third person template level.

1.  Begin by navigating to the world outliner panel, and shift select the **Floor** and the four **Wall** Static Mesh Actors from the **ArenaGeometry > Arena** folder.
    
    [![selecting-floors-and-walls-in-the-world-outliner](https://dev.epicgames.com/community/api/documentation/image/0ecebac2-5c25-46e9-b88c-fc6d87a6e6dd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ecebac2-5c25-46e9-b88c-fc6d87a6e6dd?resizing_type=fit)
    
    In the example image above, the four Wall Static Mesh Actors are listed as **Wall6**, **Wall7**, **Wall8**, and **Wall9**.
    
2.  **Alt-click** and drag the **Transform** gizmo to create a duplicate floor and wall setup.
    
3.  This will result in the creation of a second **Floor**, and four additional **Wall** Static Mesh Actors.
    
    [![Duplicated walls and floors](https://dev.epicgames.com/community/api/documentation/image/ce5fa026-0299-4984-a901-d1b54d9d88f4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce5fa026-0299-4984-a901-d1b54d9d88f4?resizing_type=fit)
    
    In the example image above, the duplicated floor is labeled Floor2, and the duplicated walls are named **Wall10**, **Wall11**, **Wall12**, and **Wall13**.
    
4.  Move the newly duplicated static meshes to resemble the layout below, a new room duplicating the first but without any contents.
    
    [![Overhead view of new room](https://dev.epicgames.com/community/api/documentation/image/1f752c52-ec8e-49d3-a01b-93e7a8251cd2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1f752c52-ec8e-49d3-a01b-93e7a8251cd2?resizing_type=fit)
    
    Click image to expand.
    
      
    
5.  From the world outliner, select the two walls that connect the two rooms, and set their **X Scale** values to 14.
    
    In the example image above, these two walls are labeled **Wall9** and **Wall12**.
    
    [![x-scale-value-in-details-panel](https://dev.epicgames.com/community/api/documentation/image/c66e7f67-687f-45a0-90ec-2d1dde3c5428?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c66e7f67-687f-45a0-90ec-2d1dde3c5428?resizing_type=fit)
    
6.  Select both the connecting walls, then move them using the **Transform** gizmo so that they form a partition between rooms with a gap as shown in the gif below.
    
    In the example image above, these two walls are labeled **Wall9** and **Wall10**
    
7.  Your completed level setup should look similar to the image below, with a second room connected to the first by an opening in the wall.
    
    [![Connected rooms](https://dev.epicgames.com/community/api/documentation/image/722667bc-ee28-47e9-b846-ef1468cd1381?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/722667bc-ee28-47e9-b846-ef1468cd1381?resizing_type=fit)
    
    Click image to expand.
    

## Camera Perspective Setup

Now that you have completed the level setup, you can place the **BP\_ExampleCameraActor** in the level to get a better idea of the view the player will have once they overlap the trigger volume. You can take a First Person perspective from the Camera's Point of View by locking the **Viewport** to the Camera Actor and entering **Pilot** mode.

1.  With the Camera selected in the level, right-click on it, then from the context menu select **Pilot CameraActor**.
    
    [![Context menu Pilot CameraActor](https://dev.epicgames.com/community/api/documentation/image/d726af6d-e9d8-4d47-a3d5-e6e98796a186?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d726af6d-e9d8-4d47-a3d5-e6e98796a186?resizing_type=fit)
    
2.  You can now move around the Viewport using the **WASD** keys while holding the **Left** or **Right Mouse Button** down. While you fly around the level, the Camera's position will move along with your movement allowing you to get an idea of the perspective the camera will take during gameplay.
    
3.  To unlock the Camera, click the **Unlock** button.
    
    [![Unlock button](https://dev.epicgames.com/community/api/documentation/image/1c93c882-69f1-4ef9-a5a5-8ae509ddd0e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1c93c882-69f1-4ef9-a5a5-8ae509ddd0e0?resizing_type=fit)
    
    The camera will remain where it was positioned when you unlocked it. The icon next to the Unlock button allows you to toggle between showing the in-game camera view or the level editor view.
    
4.  Pilot the Camera into a position looking down on the second room similar to the gif below.
    
5.  Your completed camera scene setup should look similar to the image below, with a static camera looking down on the new room along with the original camera following the third-person actor.
    
    [![Completed Camera setup](https://dev.epicgames.com/community/api/documentation/image/379516ab-9569-4edc-8f6e-d84afd290289?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/379516ab-9569-4edc-8f6e-d84afd290289?resizing_type=fit)
    
    Click image to expand.
    

## Creating the Overlap Trigger Actor

In this example, the trigger Actor functions as the transition manager between the player's camera view point and the static camera view point, once the player overlaps its box component volume bounds, a transitional blend will occur between the perspectives.

1.  Using the **C++ Class Wizard**, create a new Actor class named BlendTriggerVolume.
    
    [![New C++ Blend Trigger Volume class](https://dev.epicgames.com/community/api/documentation/image/b0b57448-ca13-417b-aaae-ab111b793d33?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b0b57448-ca13-417b-aaae-ab111b793d33?resizing_type=fit)
    
2.  Navigate to your `BlendTriggerVolume.h` file, and declare the following code in your **class definition**.
    
    C++
    
    ```code
    `protected: 		          //Collision Bounds of the Actor Volume          UPROPERTY(EditAnywhere, BlueprintReadWrite)              class UBoxComponent* OverlapVolume; 		              //Camera Actor which the Actor Volume blends to              UPROPERTY(EditAnywhere, BlueprintReadWrite)              TSubclassOf<ACameraActor> CameraToFind;`
    		
    
    ```
    
    Expand codeCopy full snippet(18 lines long)
    
3.  Next, navigate to your `BlendTriggerVolume.cpp` file to set up your constructor and box component overlap methods. Declare the following include class libraries.
    
    C++
    
    `` `#include "Components/BoxComponent.h"` 		          `#include "StaticCamerasCharacter.h"` 		          `#include "Camera/CameraActor.h"` 		          `#include "Runtime/Engine/Classes/Kismet/GameplayStatics.h"` ``
    
    \`#include &quot;Components/BoxComponent.h&quot;\` \`#include &quot;StaticCamerasCharacter.h&quot;\` \`#include &quot;Camera/CameraActor.h&quot;\` \`#include &quot;Runtime/Engine/Classes/Kismet/GameplayStatics.h&quot;\`
    
    Copy full snippet(7 lines long)
    
4.  In the constructor **ABlendTriggerVolume::ABlendTriggerVolume**, declare the following code.
    
    C++
    
    `ABlendTriggerVolume::ABlendTriggerVolume()          {          //Create box component default components          OverlapVolume = CreateDefaultSubobject<UBoxComponent>(TEXT("CameraProximityVolume"));          //Set the box component attachment to the root component.          OverlapVolume->SetupAttachment(RootComponent);          }`
    
    ABlendTriggerVolume::ABlendTriggerVolume() { //Create box component default components OverlapVolume = CreateDefaultSubobject&lt;UBoxComponent&gt;(TEXT(&quot;CameraProximityVolume&quot;)); //Set the box component attachment to the root component. OverlapVolume-&gt;SetupAttachment(RootComponent); }
    
    Copy full snippet(7 lines long)
    
5.  Next, implement your `NotifyActorBeginOverlap` and `NotifyActorEndOverlap` class methods:
    
    C++
    
    ```code
    `void ABlendTriggerVolume::NotifyActorBeginOverlap(AActor* OtherActor){          //Cast check to see if overlapped Actor is Third Person Player Character 		          if (AStaticCamerasCharacter* PlayerCharacterCheck = Cast<AStaticCamerasCharacter>(OtherActor))              { 		          //Cast to Player Character's PlayerController 		          if (APlayerController* PlayerCharacterController = Cast<APlayerController>(PlayerCharacterCheck->GetController()))                  {`
    
    ```
    
    Expand codeCopy full snippet(35 lines long)
    
6.  **Compile** your code.
    

## Finished Code

### BlendTriggerVolume.h

C++

```code
`#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "BlendTriggerVolume.generated.h"  	UCLASS() 	class STATICCAMERAS_API ABlendTriggerVolume : public AActor 	{ 		GENERATED_BODY()`

```

Expand codeCopy full snippet(35 lines long)

### BlendTriggerVolume.cpp

C++

```code
`#include "BlendTriggerVolume.h" 	#include "Components/BoxComponent.h" 	#include "StaticCamerasCharacter.h" 	#include "Camera/CameraActor.h" 	#include "Runtime/Engine/Classes/Kismet/GameplayStatics.h"  	// Sets default values 	ABlendTriggerVolume::ABlendTriggerVolume() 	{`


```

Expand codeCopy full snippet(66 lines long)

## Setting up the Overlap Trigger Actor

Now that you have created your overlap Actor, you will need to place it into the level and set up its bounds.

1.  Begin by navigating to your **C++ Classes** folder, right-click on your **BlendTriggerVolume** class, select **Create Blueprint Class based on BlendTriggerVolume**, then name your **Blueprint Actor** **BP\_BlendTriggerVolume**.
    
    [![Create Blueprint class](https://dev.epicgames.com/community/api/documentation/image/7ae1d43b-9e30-4821-a019-4ba4f5463dba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ae1d43b-9e30-4821-a019-4ba4f5463dba?resizing_type=fit)
    
2.  From the class defaults, navigate to **Camera To Find** in the **Details** panel, open the drop down menu, then select **BP\_ExampleCameraActor**.
    
    [![Finding the camera](https://dev.epicgames.com/community/api/documentation/image/4c4cc794-8fe1-4f20-8404-278eeb8de8ec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4c4cc794-8fe1-4f20-8404-278eeb8de8ec?resizing_type=fit)
    
3.  Optionally, you can change the default blend time for this Blueprint without having to go back into the source code, or affecting other Blueprints with the same inherited parent class.
    
    [![Change default Blend time](https://dev.epicgames.com/community/api/documentation/image/d3e00370-39f3-4996-9280-13c8d97170c1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d3e00370-39f3-4996-9280-13c8d97170c1?resizing_type=fit)
    
4.  **Compile** and **Save**.
    
    [![Compile button](https://dev.epicgames.com/community/api/documentation/image/8bcedc39-47eb-4505-ab26-27407e4c8a6c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8bcedc39-47eb-4505-ab26-27407e4c8a6c?resizing_type=fit)
    
5.  From the **Content Browser**, drag an instance of **BP\_BlendTriggerVolume** into the level.
    
    [![Place Volume actor](https://dev.epicgames.com/community/api/documentation/image/b86cec6a-0061-4a92-bf7c-d48e26cc1236?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b86cec6a-0061-4a92-bf7c-d48e26cc1236?resizing_type=fit)
    
    Click image to expand.
    
6.  Move the **BP\_BlendTriggerVolume** into the room with your **BP\_ExampleCameraActor**, and from the **Details** panel select the box component. Navigate to the **Shape** category and modify the **Box Extent** X, Y, and Z values so the volume will fit your room.
    
    [![Adjust Volume actor to fit room](https://dev.epicgames.com/community/api/documentation/image/55f3e960-a289-404d-8943-ed813a1a349f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/55f3e960-a289-404d-8943-ed813a1a349f?resizing_type=fit)
    
    Click image to expand.
    
7.  From the **Main Editor View**, click the **Play** button to play in the Editor.
    

## End Result

When the game starts, the player controls their character's movement using **WASD**. Upon overlapping the **BP\_BlendTriggerVolume** the camera view is assigned to the **Camera Actor** that you have created and placed in your level, and the view will switch to an overhead shot of the player-controlled character.

You may have noticed that the view is Widescreen; you can disable this by un-checking the **Constrain Aspect Ratio** option inside the **Details** panel for the Camera Actor.

[![Constrain Aspect Ratio checkbox](https://dev.epicgames.com/community/api/documentation/image/cbdeeda9-acff-481e-a05f-17e80f7e8912?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cbdeeda9-acff-481e-a05f-17e80f7e8912?resizing_type=fit)