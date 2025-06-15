# Using the OnHit Event

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-onhit-event](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-onhit-event)  
**Processed:** 2025-06-14 17:01:40

---

Programming Language

×C++

Select an option from the dropdown to see content relevant to it.

Imagine you are creating a game that involves any kind of damage to a player, enemy, or object. In that case, chances are you will encounter a situation where you need to determine if those objects were hit by something and if so, what hit them, where the impact point was, or other information regarding the hit detected. The **OnHit Event** provides this information when the collision occurs, then you can use the data to drive changes in your game. Whether it affects health, destroys an object, or causes other gameplay-related actions.

In this tutorial, you will use the **OnComponentHit** and **Function** [Events](https://dev.epicgames.com/documentation/en-us/unreal-engine/events-in-unreal-engine) to apply damage to an Actor that will be represented by changing the Actor's mesh material. The Events will also apply an impulse at the hit location to push the Actor, simulating the effects of being hit by a projectile and applying force at the hit location.

## Project Setup

1.  Begin by creating a new **Games** > **First Person** > **C++** Project named **OnHit**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/7c805698-097e-4788-90d6-76379192efb3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7c805698-097e-4788-90d6-76379192efb3?resizing_type=fit)
    

## Creating the Mesh Material

1.  Navigate to the **Content Browser**, and find the **LevelPrototyping/Materials** folder.
    
2.  Select **MI\_SolidBlue**, then duplicate (**CTRL+ D**) and rename the newly duplicated asset **MI\_Solid\_Red**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/6108d51a-563f-42f3-a250-5f7127e9251d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6108d51a-563f-42f3-a250-5f7127e9251d?resizing_type=fit)
    
3.  Double-click to open the asset, then select and edit the **Base Color** to the color red.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/bdbc8637-a17e-47cd-8d76-2a7e194aadf7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bdbc8637-a17e-47cd-8d76-2a7e194aadf7?resizing_type=fit)
    
4.  **Save** the Asset.
    

## Creating the Cube Actor

1.  In the **Editor**, click **Add(+)** > **New C++ Class**, then choose **Actor** as your parent class and name your class **Cube**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f13ec163-adbc-4059-878d-a9b31c62643e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f13ec163-adbc-4059-878d-a9b31c62643e?resizing_type=fit)
    
2.  Declare the following class defaults in your `cube.h` file
    
    C++
    
    ```code
    `UPROPERTY(EditDefaultsOnly, BlueprintReadWrite)          class UStaticMeshComponent* CubeMesh; 		          UPROPERTY(EditDefaultsOnly, BlueprintReadWrite)          UMaterialInstance* CubeMaterial; 		          UPROPERTY(EditDefaultsOnly, BlueprintReadWrite)          UMaterialInstance* DamagedCubeMaterial; 		          FTimerHandle DamageTimer;`
    
    ```
    
    Expand codeCopy full snippet(14 lines long)
    
3.  Next, in your `cube.cpp` file, declare the following class libraries.
    
    C++
    
    `#include "Kismet/GameplayStatics.h"      #include "OnHitProjectile.h"`
    
    #include &quot;Kismet/GameplayStatics.h&quot; #include &quot;OnHitProjectile.h&quot;
    
    Copy full snippet(2 lines long)
    
4.  Navigate to the cube constructor and implement the following functionality.
    
    C++
    
    `ACube::ACube()      {          CubeMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("CubeMesh"));          DamagedCubeMaterial = CreateDefaultSubobject<UMaterialInstance>(TEXT("DamageMaterial"));          CubeMaterial = CreateDefaultSubobject<UMaterialInstance>(TEXT("CubeMaterial")); 		          CubeMesh->SetSimulatePhysics(true);      }`
    
    ACube::ACube() { CubeMesh = CreateDefaultSubobject&lt;UStaticMeshComponent&gt;(TEXT(&quot;CubeMesh&quot;)); DamagedCubeMaterial = CreateDefaultSubobject&lt;UMaterialInstance&gt;(TEXT(&quot;DamageMaterial&quot;)); CubeMaterial = CreateDefaultSubobject&lt;UMaterialInstance&gt;(TEXT(&quot;CubeMaterial&quot;)); CubeMesh-&gt;SetSimulatePhysics(true); }
    
    Copy full snippet(8 lines long)
    

### Implementing the Damage functionality

Now that you created a cube, you need to implement a function that sets the mesh's material when it receives damage, then after a delay resets the mesh back to its original material.

1.  Declare the following code in your `cube.h` file.
    
    C++
    
    `void OnTakeDamage(); 		          void ResetDamage();`
    
    void OnTakeDamage(); void ResetDamage();
    
    Copy full snippet(3 lines long)
    
2.  Navigate to the `cube.cpp` file and implement the following for the `ACube::BeginPlay` function.
    
    C++
    
    `void ACube::BeginPlay()      {         CubeMesh->OnComponentHit.AddDynamic(this, &ACube::OnComponentHit);      }`
    
    void ACube::BeginPlay() { CubeMesh-&gt;OnComponentHit.AddDynamic(this, &amp;ACube::OnComponentHit); }
    
    Copy full snippet(4 lines long)
    
3.  Implement the `ACube::OnTakeDamage` function.
    
    C++
    
    `void ACube::OnTakeDamage()      { 		          CubeMesh->SetMaterial(0, DamagedCubeMaterial);          GetWorld()->GetTimerManager().SetTimer(DamageTimer, this, &ACube::ResetDamage, 1.5f, false);      }`
    
    void ACube::OnTakeDamage() { CubeMesh-&gt;SetMaterial(0, DamagedCubeMaterial); GetWorld()-&gt;GetTimerManager().SetTimer(DamageTimer, this, &amp;ACube::ResetDamage, 1.5f, false); }
    
    Copy full snippet(6 lines long)
    
4.  Next, implement the `ACube::ResetDamage` function.
    
    C++
    
    `void ACube::ResetDamage()      {          CubeMesh->SetMaterial(0,CubeMaterial);      }`
    
    void ACube::ResetDamage() { CubeMesh-&gt;SetMaterial(0,CubeMaterial); }
    
    Copy full snippet(4 lines long)
    
5.  Finally, navigate to the `ACube::OnComponentHit` function and implement the following code.
    
    C++
    
    `void ACube::OnComponentHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit)      {      if (AOnHitProjectile* HitActor = Cast<AOnHitProjectile>(OtherActor))      { 		          UGameplayStatics::ApplyDamage(this, 20.0f, nullptr, OtherActor, UDamageType::StaticClass());          OnTakeDamage(); 		      }      }`
    
    void ACube::OnComponentHit(UPrimitiveComponent\* HitComp, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult&amp; Hit) { if (AOnHitProjectile\* HitActor = Cast&lt;AOnHitProjectile&gt;(OtherActor)) { UGameplayStatics::ApplyDamage(this, 20.0f, nullptr, OtherActor, UDamageType::StaticClass()); OnTakeDamage(); } }
    
    Copy full snippet(10 lines long)
    
6.  Compile your code.
    
7.  In the editor, navigate to **C++ Classes** \> **Cube** then right-click on the **Cube Actor** and select **Create Blueprint class based on Cube**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f0fc33e0-0e5e-44b0-b741-89ca6e3c5967?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0fc33e0-0e5e-44b0-b741-89ca6e3c5967?resizing_type=fit)
    
8.  From the Components tab, select the **Cube Mesh**, then navigate to **Details** > **Static Mesh** and select the **SM\_ChamferCube** asset.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2b2431eb-7189-4b0a-aede-d368a95e6bd0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2b2431eb-7189-4b0a-aede-d368a95e6bd0?resizing_type=fit)
    
9.  In the class defaults of the **BP\_Cube**, set the **Cube Material** to the **MI\_Solid\_Blue** asset, and the **Damaged Cube Material** to the **MI\_Solid\_Red** asset.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4fe8516e-6f76-4da7-ad1a-a9fc51cf804b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4fe8516e-6f76-4da7-ad1a-a9fc51cf804b?resizing_type=fit)
    
10.  **Compile** and **Save**.
    

### CubeActor.h

C++

```code
`#pragma once  		#include "CoreMinimal.h" 		#include "GameFramework/Actor.h" 		#include "Cube.generated.h"  		UCLASS() 		class ONHIT_API ACube : public AActor 		{ 			GENERATED_BODY()`

```

Expand codeCopy full snippet(42 lines long)

### CubeActor.cpp

C++

```code
`#include "Cube.h" 		#include "Kismet/GameplayStatics.h" 		#include "OnHitProjectile.h"  		// Sets default values 		ACube::ACube() 		{ 			// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 			PrimaryActorTick.bCanEverTick = true;`


```

Expand codeCopy full snippet(52 lines long)

## Setting up the Level

1.  Drag the **BP\_Cube** into the level from the **Content Browser**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2b7197ef-8b44-4537-a03f-6a18a18bd3a1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2b7197ef-8b44-4537-a03f-6a18a18bd3a1?resizing_type=fit)
    
2.  Navigate to the **Outliner** > **Simulated Cubes**, select all **SM\_ChauferCubes** then right-click and select **Replace Selected Actors with** > **BP\_Cube**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/386f981d-6b3b-43f8-b8a3-fab1539cfed1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/386f981d-6b3b-43f8-b8a3-fab1539cfed1?resizing_type=fit)
    
3.  Click **Play** to play in the editor and use the left-mouse button to fire a projectile at the cube.
    
4.  When you play in the editor, you will see that when you hit the cube with the projectile fired it causes the cube to take damage and change its mesh material, and applies an impulse at the location where it was hit causing it to move opposite the direction of the projectile.
    
    ![](https://dev.epicgames.com/community/api/documentation/image/8bb51b60-081a-4245-a5bd-dfb1ab1a325c?resizing_type=fit)
    
5.  The amount of force applied is defined inside the `OnHitProjectile.cpp` file which uses the **OnHit** function to determine when the projectile actually hits something.
    
    C++
    
    ```code
    `void AOnHitCPPProjectile::OnHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit)      { 		          // Only add impulse and destroy projectile if we hit a physics          if ((OtherActor != nullptr) && (OtherActor != this) && (OtherComp != nullptr) && OtherComp->IsSimulatingPhysics())          {              OtherComp->AddImpulseAtLocation(GetVelocity() * 100.0f, GetActorLocation()); 		              Destroy();          }`
    
    ```
    
    Expand codeCopy full snippet(12 lines long)