# Loading and Unloading Levels using C++

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/loading-and-unloading-levels-using-cplusplus-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/loading-and-unloading-levels-using-cplusplus-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:06

---

We want to start streaming in the patio level here, so that by the time the player rounds the corner and begins approaching the patio, the streaming level will be loaded and visible.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73c4efc5-feb4-41f3-b7f1-2221ae8d1767/streaminglevelvisible.png)

As part of the setup, we have two levels, **SunTemple\_Persistent** and **SunTemple\_Streaming**. Our **Player Start** is in **SunTemple\_Persistent**, and our player in the game is represented by a *Character*.

1.  Open **SunTemple\_Persistent** in the **Content Browser**.
    
2.  Move the **Player Start** to the very beginning of the temple.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0022d220-1260-4344-b42c-0b7c36d2279f/playerstart.png)
3.  Click on **Windows**, then select **Levels**.
    
4.  Click on the **Levels** dropdown menu, then select **Add Existing...** to add a new sublevel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c10338e1-6fa4-4e57-87bc-989d05e1e990/addexisting.png)
5.  Select **SunTemple\_Streaming** to add in the **Open Level** dialog, then click on **Open**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b76c3a4-3d42-4723-9aab-e470df90b05d/suntemplestreaming_select.png)
6.  **Right-click** on **Persistent Level** and select **Make Current** from the dropdown menu.
    

## Streaming In Levels with C++

1.  Open the **Content Browser** and create a new **C++ Class**. This class is going to be based on **Actor**, so select **Actor** and click **Next**.
    
2.  Name the new **C++ Class** "LevelStreamerActor", then click on **Create Class**. The new class will now open in Visual Studio or XCode.
    

For this scenario, we want to stream the second level in once the **Character** overlaps a BoxComponent called OverlapVolume in our LevelStreamerActor.

1.  In `LevelStreamerActor.h`, declare an OverlapVolume that is VisibleAnywhere, BlueprintReadOnly, and has the AllowPrivateAccess meta flag.
    
    ```
             `private:          // Overlap volume to trigger level streaming          UPROPERTY(VisibleAnywhere, BlueprintReadOnly, meta = (AllowPrivateAccess = "true"))          UBoxComponent* OverlapVolume;`
    Copy full snippet
    ```
    private: // Overlap volume to trigger level streaming UPROPERTY(VisibleAnywhere, BlueprintReadOnly, meta = (AllowPrivateAccess = "true")) UBoxComponent\* OverlapVolume;
2.  In `LevelStreamerActor.cpp`, in the LevelStreamerActor constructor, create the OverlapVolume and make it the RootComponent.
    
    ```
             `OverlapVolume = CreateDefaultSubobject<UBoxComponent>(TEXT("OverlapVolume"));          RootComponent = OverlapVolume;`
    Copy full snippet
    ```
    OverlapVolume = CreateDefaultSubobject<UBoxComponent>(TEXT("OverlapVolume")); RootComponent = OverlapVolume;
3.  Back in `LevelStreamerActor.h`, declare a protected OverlapBegins function, which will be bound to the BoxComponent's OnComponentBeginOverlap function. This binding means that OverlapBegins must be tagged with a UFUNCTION macro, and must have the same signature as OnComponentBeginOverlap.
    
    ```
         `protected:       UFUNCTION()      void OverlapBegins(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult);`
    Copy full snippet
    ```
    protected: UFUNCTION() void OverlapBegins(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult);
4.  Also in `LevelStreamerActor.h`, create a protected FName variable that is EditAnywhere called LevelToLoad. This will enable you to change the LevelToLoad on a per-instance basis.
    
    ```
             `UPROPERTY(EditAnywhere)          FName LevelToLoad;`
    		
    Copy full snippet
    ```
    UPROPERTY(EditAnywhere) FName LevelToLoad;
5.  We are going to use a few functions from the GameplayStatics library, so include it at the top of `LevelStreamerActor.cpp`.
    
    ```
             `#include "Kismet/GameplayStatics.h"`
    		
    Copy full snippet
    ```
    #include "Kismet/GameplayStatics.h"
6.  Now you are ready to create your OverlapBegins functionality. In `LevelStreamerActor.cpp`, begin defining the function. You can use the GameplayStatics function `GetPlayerCharacter` to get the Character at index 0.
    
    ```
             `void ALevelStreamerActor::OverlapBegins(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult)          {                  ACharacter* MyCharacter = UGameplayStatics::GetPlayerCharacter(this, 0);          }`
    Copy full snippet
    ```
    void ALevelStreamerActor::OverlapBegins(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult) { ACharacter\* MyCharacter = UGameplayStatics::GetPlayerCharacter(this, 0); }
7.  After getting MyCharacter, check it against the OtherActor overlapping your BoxComponent. Also, verify that LevelToLoad is not empty, then call LoadStreamLevel.
    
    ```
             `if (OtherActor == MyCharacter && LevelToLoad != "")          {              FLatentActionInfo LatentInfo;              UGameplayStatics::LoadStreamLevel(this, LevelToLoad, true, true, LatentInfo);          }`
    Copy full snippet
    ```
    if (OtherActor == MyCharacter && LevelToLoad != "") { FLatentActionInfo LatentInfo; UGameplayStatics::LoadStreamLevel(this, LevelToLoad, true, true, LatentInfo); }
8.  In your LevelStreamerActor constructor, bind OverlapBegins to your BoxComponent's OnComponentBeginOverlap.
    
    ```
             `OverlapVolume->OnComponentBeginOverlap.AddUniqueDynamic(this, &ALevelStreamerActor::OverlapBegins);`
    Copy full snippet
    ```
    OverlapVolume->OnComponentBeginOverlap.AddUniqueDynamic(this, &ALevelStreamerActor::OverlapBegins);
    
    Your final `LevelStreamerActor.h` should look like:
    
    ```
         `#pragma once       #include "GameFramework/Actor.h"      #include "LevelStreamerActor.generated.h"       UCLASS()      class LEVELS_API ALevelStreamerActor : public AActor      {          GENERATED_BODY()       public:          // Sets default values for this actor's properties          ALevelStreamerActor();           // Called every frame          virtual void Tick( float DeltaSeconds ) override;       protected:           // Called when the game starts or when spawned          virtual void BeginPlay() override;           UFUNCTION()          void OverlapBegins(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult);           UPROPERTY(EditAnywhere)          FName LevelToLoad;       private:          // Overlap volume to trigger level streaming          UPROPERTY(VisibleAnywhere, BlueprintReadOnly, meta = (AllowPrivateAccess = "true"))          UBoxComponent* OverlapVolume;       };`
    Copy full snippet
    ```
    #pragma once #include "GameFramework/Actor.h" #include "LevelStreamerActor.generated.h" UCLASS() class LEVELS\_API ALevelStreamerActor : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties ALevelStreamerActor(); // Called every frame virtual void Tick( float DeltaSeconds ) override; protected: // Called when the game starts or when spawned virtual void BeginPlay() override; UFUNCTION() void OverlapBegins(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult); UPROPERTY(EditAnywhere) FName LevelToLoad; private: // Overlap volume to trigger level streaming UPROPERTY(VisibleAnywhere, BlueprintReadOnly, meta = (AllowPrivateAccess = "true")) UBoxComponent\* OverlapVolume; };
    
    Your final `LevelStreamerActor.cpp` should look like:
    
    ```
         `#include "Levels.h"      #include "Kismet/GameplayStatics.h"      #include "LevelStreamerActor.h"       // Sets default values      ALevelStreamerActor::ALevelStreamerActor()      {          // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.          PrimaryActorTick.bCanEverTick = true;           OverlapVolume = CreateDefaultSubobject<UBoxComponent>(TEXT("OverlapVolume"));          RootComponent = OverlapVolume;           OverlapVolume->OnComponentBeginOverlap.AddUniqueDynamic(this, &ALevelStreamerActor::OverlapBegins);      }      // Called when the game starts or when spawned      void ALevelStreamerActor::BeginPlay()      {          Super::BeginPlay();       }       // Called every frame      void ALevelStreamerActor::Tick( float DeltaTime )      {          Super::Tick( DeltaTime );       }       void ALevelStreamerActor::OverlapBegins(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult)      {              ACharacter* MyCharacter = UGameplayStatics::GetPlayerCharacter(this, 0);              if (OtherActor == MyCharacter && LevelToLoad != "")              {                  FLatentActionInfo LatentInfo;                  UGameplayStatics::LoadStreamLevel(this, LevelToLoad, true, true, LatentInfo);              }      }`
    Copy full snippet
    ```
    #include "Levels.h" #include "Kismet/GameplayStatics.h" #include "LevelStreamerActor.h" // Sets default values ALevelStreamerActor::ALevelStreamerActor() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; OverlapVolume = CreateDefaultSubobject<UBoxComponent>(TEXT("OverlapVolume")); RootComponent = OverlapVolume; OverlapVolume->OnComponentBeginOverlap.AddUniqueDynamic(this, &ALevelStreamerActor::OverlapBegins); } // Called when the game starts or when spawned void ALevelStreamerActor::BeginPlay() { Super::BeginPlay(); } // Called every frame void ALevelStreamerActor::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } void ALevelStreamerActor::OverlapBegins(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult) { ACharacter\* MyCharacter = UGameplayStatics::GetPlayerCharacter(this, 0); if (OtherActor == MyCharacter && LevelToLoad != "") { FLatentActionInfo LatentInfo; UGameplayStatics::LoadStreamLevel(this, LevelToLoad, true, true, LatentInfo); } }
9.  Compile your code, then switch back to the editor.
    
10.  Place your **LevelStreamer** Actor into your level, and adjust the placement and scale until it encompasses the part of the persistent world you want your **Character** to be in to begin streaming, as well as the entire walkable volume where the streaming level will be.
    
11.  Enter **SunTemple\_Streaming** as the **Level to Stream**.
    
12.  Use Play In Editor to test out your streaming level.
    

## Unloading Levels With C++

To unload the level as your *Character* exits the BoxComponent, you will create an `OverlapEnds` function that calls `UGameplayStatics::UnloadStreamLevel` and bind it to `OnComponentEndOverlap`. Add the following code snippets to your LevelStreamerActor:

In LevelStreamerActor.h:

```
	`UFUNCTION() 	void OverlapEnds(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);`
Copy full snippet
```
UFUNCTION() void OverlapEnds(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex);

In LevelStreamerActor.cpp:

```
	`void ALevelStreamerActor::OverlapEnds(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex) 	{ 			ACharacter* MyCharacter = UGameplayStatics::GetPlayerCharacter(this, 0); 			if (OtherActor == MyCharacter && LevelToLoad != "") 			{ 				FLatentActionInfo LatentInfo; 				UGameplayStatics::UnloadStreamLevel(this, LevelToLoad, LatentInfo); 			} 	}`
Copy full snippet
```
void ALevelStreamerActor::OverlapEnds(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex) { ACharacter\* MyCharacter = UGameplayStatics::GetPlayerCharacter(this, 0); if (OtherActor == MyCharacter && LevelToLoad != "") { FLatentActionInfo LatentInfo; UGameplayStatics::UnloadStreamLevel(this, LevelToLoad, LatentInfo); } }

In the constructor:

```
	`OverlapVolume->OnComponentEndOverlap.AddUniqueDynamic(this, &ALevelStreamerActor::OverlapEnds);`
Copy full snippet
```
OverlapVolume->OnComponentEndOverlap.AddUniqueDynamic(this, &ALevelStreamerActor::OverlapEnds);