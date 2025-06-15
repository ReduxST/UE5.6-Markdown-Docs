# Remote Procedure Calls

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:40

---

**Remote Procedure Calls (RPCs)** are functions called locally that execute remotely on one or more connected machines. RPCs help clients and the server call functions on one another over a network connection. RPCs are unidirectional function calls, as such, they cannot specify a return value. The primary use case for RPCs is to perform unreliable gameplay events that are transient or cosmetic in nature. These could include events such as:

-   Playing sounds
-   Spawning particles
-   Performing Animations

RPCs are an important mechanism that supplement replicated properties that use the `Replicated` or `ReplicatedUsing` specifiers. To call an RPC, you must call the RPC from an actor or actor component and set the actor and relevant actor component to replicate.

It is important to first understand how ownership works with RPCs, since actor ownership determines where RPCs remotely execute. For more information about actor ownership, see the [Actor Owner and Owning Connection](/documentation/en-us/unreal-engine/actor-owner-and-owning-connection-in-unreal-engine) documentation.

## Types of RPC

There are four different types of RPCs as outlined in the following table:

| **Metadata Specifier** | **Description** |
| --- | --- |
| `Client` | The RPC is executed on the owning client connection for this actor. |
| `Server` | 
The RPC is executed on the server.

Must be called from the client that owns this actor.



 |
| `Remote` | 

The RPC is executed on the remote side of the connection.

The remote side of the connection can be either the server or the client, but the RPC must be called on an actor that is owned by a client. The RPC behaves like both a `Client` and a `Server` RPC, but is never executed on the local side of the connection, only the remote side.



 |
| `NetMulticast` | 

The RPC is executed on the server and all currently connected clients the actor is relevant for.

`NetMulticast` RPCs are designed to be called from the server, but can be called from clients. A `NetMulticast` RPC called from a client only executes locally.



 |

## Structure of an RPC

All RPCs consist of two pieces:

-   The base function defined in your header file.
    
    DerivedActor.h
    
    ```
          `UFUNCTION(Client)       void ClientRPC();`
    Copy full snippet
    ```
    UFUNCTION(Client) void ClientRPC();
-   The implementation function that contains the base function implementation in your source file.
    
    DerivedActor.cpp
    
    ```
          `#include "DerivedActor.h"        void ClientRPC_Implementation()       {	 			       }`
    Copy full snippet
    ```
    #include "DerivedActor.h" void ClientRPC\_Implementation() { }

Unreal Engine's reflection and replication systems manage the lower level details, but require that you define and implement these pieces. The following sections explain how to declare and implement an RPC.

## Create an RPC

To create an RPC for an actor, follow these steps:

1.  Choose one of the function metadata specifiers from the [Types of RPC](/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine#typesofrpc) section:
    
    DerivedActor.h
    
    ```
         `#pragma once       #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:           // Client RPC Function          UFUNCTION(Client)          void ClientRPC();           // Server RPC Function          UFUNCTION(Server)          void ServerRPC();           // Multicast RPC Function          UFUNCTION(NetMulticast)          void MulticastRPC();      }`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Client RPC Function UFUNCTION(Client) void ClientRPC(); // Server RPC Function UFUNCTION(Server) void ServerRPC(); // Multicast RPC Function UFUNCTION(NetMulticast) void MulticastRPC(); }
    
    It is a convention to prepend the names of RPC functions with the type of RPC: *`Client` for Client RPC functions.* `Server` for Server RPC functions. \* `Multicast` for Network Multicast RPC functions.
    
    This is useful to determine at a glance what machines this function call is intended for during a multiplayer session.
    
2.  Ensure that your `AActor`\-derived class is set to replicate within the derived actor's constructor:
    
    DerivedActor.cpp
    
    ```
         `ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }`
    Copy full snippet
    ```
    ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; }
3.  Implement your RPC’s `_Implementation` function:
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"       void ADerivedActor::ClientRPC_Implementation()      {          // This log will print on every machine that executes this function.          UE_LOG(LogTemp, Log, TEXT("ClientRPC executed."))      }       void ADerivedActor::ServerRPC_Implementation()      {	          // This function only executes if ServerRPC_Validate returns true.          // This log will print on every machine that executes this function.          UE_LOG(LogTemp, Log, TEXT("ServerRPC executed."))      }       void ADerivedActor::MulticastRPC_Implementation()      {          // This log will print on every machine that executes this function.          UE_LOG(LogTemp, Log, TEXT("MulticastRPC executed."))	      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" void ADerivedActor::ClientRPC\_Implementation() { // This log will print on every machine that executes this function. UE\_LOG(LogTemp, Log, TEXT("ClientRPC executed.")) } void ADerivedActor::ServerRPC\_Implementation() { // This function only executes if ServerRPC\_Validate returns true. // This log will print on every machine that executes this function. UE\_LOG(LogTemp, Log, TEXT("ServerRPC executed.")) } void ADerivedActor::MulticastRPC\_Implementation() { // This log will print on every machine that executes this function. UE\_LOG(LogTemp, Log, TEXT("MulticastRPC executed.")) }

## Execute an RPC

To execute an RPC, call the standard version of the RPC function:

```
	`// Call from client to run on server 	ADerivedClientActor* MyDerivedClientActor; 	MyDerivedClientActor->ServerRPC();  	// Call from server to run on client 	ADerivedServerActor* MyDerivedServerActor; 	MyDerivedServerActor->ClientRPC();  	// Call from server to run on server and all relevant clients 	ADerviedServerActor* MyDerivedServerActor; 	MyDerievedServerActor->MulticastRPC();`
Copy full snippet
```
// Call from client to run on server ADerivedClientActor\* MyDerivedClientActor; MyDerivedClientActor->ServerRPC(); // Call from server to run on client ADerivedServerActor\* MyDerivedServerActor; MyDerivedServerActor->ClientRPC(); // Call from server to run on server and all relevant clients ADerviedServerActor\* MyDerivedServerActor; MyDerievedServerActor->MulticastRPC();

## Unicast Versus Multicast

`Client`, `Server`, and `Remote` RPCs are unicast RPCs. *Unicast* RPCs are so named because they execute on a single machine. `NetMulticast` is a *multicast* RPC because it executes on multiple machines.

## Matrix of RPC Execution

The following table describes on which machine an RPC is executed depending on what type of RPC it is, what machine it is called from, and the owning connection for the actor calling the RPC. You can read the columns of the following tables as follows:

A \[*Type of RPC*\] called from a/the \[*Calling Machine*\] whose associated actor's owning connection is a/the \[*Owning Connection*\] is executed on the \[*Executing Machine*\].

For example, the first row in the Server RPC table reads:

-   A *Server RPC* called from the *Server* whose associated actor's owning connection is the *Client* is executed on the *Server*.

The last row in the Client RPC table reads:

-   A *Client RPC* called from the *Client* whose associated actor's owning connection is *None* is executed on the *Invoking Client*.

### Server RPC

| **Calling Machine** | **Owning Connection** | **Executing Machine** |
| --- | --- | --- |
| Server | Client | Server |
| Server | Server | Server |
| Server | None | Server |
| Client | Invoking Client | Server |
| Client | Different Client | Dropped |
| Client | Server | Dropped |
| Client | None | Dropped |

### Client RPC

| **Calling Machine** | **Owning Connection** | **Executing Machine** |
| --- | --- | --- |
| Server | Owning Client | Owning Client |
| Server | Server | Server |
| Server | None | Server |
| Client | Invoking Client | Invoking Client |
| Client | Different Client | Invoking Client |
| Client | Server | Invoking Client |
| Client | None | Invoking Client |

### Remote RPC

| **Calling Machine** | **Owning Connection** | **Executing Machine** |
| --- | --- | --- |
| Server | Owning Client | Owning Client |
| Server | Server | Dropped |
| Server | None | Dropped |
| Client | Invoking Client | Server |
| Client | Different Client | Dropped |
| Client | Server | Dropped |
| Client | None | Dropped |

### Net Multicast RPC

| **Calling Machine** | **Owning Connection** | **Executing Machine** |
| --- | --- | --- |
| Server | Client | Server and all Clients the invoking actor is relevant for |
| Server | Server | Server and all Clients the invoking actor is relevant for |
| Server | None | Server and all Clients the invoking actor is relevant for |
| Client | Invoking Client | Invoking Client |
| Client | Different Client | Invoking Client |
| Client | Server | Invoking Client |
| Client | None | Invoking Client |

## Reliability

RPCs in Unreal Engine are marked as either reliable or unreliable:

| **Metadata Specifier** | **Description** | **Order of Execution** |
| --- | --- | --- |
| `Reliable` | This RPC is re-sent until it is acknowledged by the receiver. All subsequent RPC executions are suspended until this RPC is acknowledged. | Guaranteed in order. |
| `Unreliable` | This RPC is not executed if the packet is dropped. | No order guarantee. |

RPCs are unreliable by default. Reliable RPCs require additional bandwidth, as such, use them sparingly.

For more information about order of execution guarantees for replication in Unreal Engine, see the [Replicated Object Execution Order](/documentation/en-us/unreal-engine/replicated-object-execution-order-in-unreal-engine) documentation.

### Specify RPC Reliability

To specify the reliability of an RPC, add the appropriate metadata specifier for your RPC:

DerivedActor.h

```
	`#pragma once  	#include "DerivedActor.generated.h"  	UCLASS() 	class ADerivedActor : public AActor 	{ 		GENERATED_BODY()  	public:	  		// Client Default Unreliable RPC Function 		UFUNCTION(Client) 		void ClientDefaultUnreliableRPC();  		// Client Unreliable RPC Function 		UFUNCTION(Client, Unreliable) 		void ClientUnreliableRPC();  		// Client Reliable RPC Function 		UFUNCTION(Client, Reliable) 		void ClientReliableRPC(); 	}`
Copy full snippet
```
#pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Client Default Unreliable RPC Function UFUNCTION(Client) void ClientDefaultUnreliableRPC(); // Client Unreliable RPC Function UFUNCTION(Client, Unreliable) void ClientUnreliableRPC(); // Client Reliable RPC Function UFUNCTION(Client, Reliable) void ClientReliableRPC(); }

## Send Policy

It is possible to assign RPCs an explicit send policy that affects the ordering of RPCs. This can be done by specifying an `ERemoteFunctionSendPolicy`:

| **Value** | **Description** |
| --- | --- |
| `Default` | The RPC is serialized in the [bunch](/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine#bunch) immediately and the bunch is sent in the next net update at the end of the frame. |
| `ForceSend` | 
If the RPC is triggered in `NetDriver::PostTickDispatch`, the RPC is serialized in the bunch immediately and sent over the network. If the RPC is triggered during the rest of the tick, the RPC is sent according to the `Default` behavior. This is a special RPC optimization that works under the following conditions:

-   Only supported by Replication Graph and Iris
-   Works on RPCs called in `NetWorldTickTime` where incoming packets are processed and RPCs sent from remote connections are executed.

This optimization reduces latency for important gameplay events by sending data at the beginning of the frame instead of at the end. This can reduce latency at the cost of more CPU usage and additional bandwidth.



 |
| `ForceQueue` | The RPC is serialized in the bunch at the end of the net update if there is any bandwidth left. |

To specify a send policy for RPCs in your project, see [`UNetDriver::ProcessRemoteFunctionForChannel`](/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/UNetDriver/ProcessRemoteFunctionForChannel). For more information about guarantees with respect to the order of execution for RPCs on remote machines, see the [Replicated Object Execution Order](/documentation/en-us/unreal-engine/replicated-object-execution-order-in-unreal-engine) documentation.

(#bunch) In Unreal Engine networking, a network packet is composed of several bunches. A *bunch* is a collection of property changes and RPCs for a particular replicated object, such as an actor.

## Server RPC Validation

Server RPC validation implements a *trust and verify* networking policy. The server trusts the information that the client communicates to it, but always verifies that this information follows the rules and constraints defined by the game on the server.

You can mark a server RPC with the `WithValidation` `UFUNCTION` metadata and define a corresponding server RPC validation function. The validation function has the same name as your RPC function, but with `_Validate` appended to the end of the function name. The return type is a boolean, and it takes the same parameters as the RPC function that it is associated with. The validation function helps the server determine whether an RPC should or should not run, depending on the validation logic you define. When a client makes a call to execute a server RPC, the validation function is called first on the server.

The following occurs based on the output of the validation function:

-   If the inputs pass validation, the implementation is called.
-   If the inputs fail validation, the invoking client is disconnected from the server.

### Add a Validation Implementation

To add a validation function for your RPC, follow these steps:

1.  Follow the steps to [Declare a Server RPC](/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine#declareanrpc) and add the `WithValidation` metadata specifier:
    
    DerivedActor.h
    
    ```
         `#pragma once       #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:           UPROPERTY(Replicated)          int32 Health;          int32 MAXHEALTH = 100;           // Server Unreliable RPC Function          UFUNCTION(Server, Unreliable, WithValidation)          void ServerUnreliableRPC(int32 RecoverHealth);       }`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: UPROPERTY(Replicated) int32 Health; int32 MAXHEALTH = 100; // Server Unreliable RPC Function UFUNCTION(Server, Unreliable, WithValidation) void ServerUnreliableRPC(int32 RecoverHealth); }
2.  Implement the validation function:
    
    DerivedActor.h
    
    ```
         `#include "DerivedActor.h"       // RPC Validation Implementation      bool ServerUnreliableRPC_Validate(int32 RecoverHealth)      {          if (Health + RecoverHealth > MAXHEALTH)          {              return false;          }      return true;      }       // RPC Implementation      void ServerUnreliableRPC_Implementation(int32 RecoverHealth)      {          Health += RecoverHealth;      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" // RPC Validation Implementation bool ServerUnreliableRPC\_Validate(int32 RecoverHealth) { if (Health + RecoverHealth > MAXHEALTH) { return false; } return true; } // RPC Implementation void ServerUnreliableRPC\_Implementation(int32 RecoverHealth) { Health += RecoverHealth; }

If a server RPC fails validation, the calling client is disconnected.

## RPCs in Blueprint

The same types of RPCs, reliability options, and execution logic that exist for RPCs in C++ also exist for RPCs in Blueprint.

### Create a Blueprint RPC

You can also create RPCs in Blueprint using replicated Blueprint events. To create a replicated Blueprint event, follow these steps:

1.  Create or open a Blueprint Actor or Actor-derived class.
    
2.  Ensure that your Blueprint is set to **Replicate** in your Blueprint's **Details Panel**.
    
    Click image to expand.
    
3.  Open your Blueprint's **Event Graph**.
    
    Click image to expand.
    
4.  Right-click and choose **Add Event > Add Custom Event…**
    
    Click image to expand.
    
5.  Click on your **CustomEvent** node to bring up the **Details Panel**.
    
    Click image to expand.
    
6.  You can choose whether your event replicates, which type of replication it uses, and whether it is reliable or unreliable under **Details Panel > Graph > Replicates**.
    
    Click image to expand.
    
7.  Once you have chosen your desired settings, define your RPC functionality in your Blueprint's Event Graph.
    
    Click image to expand.
    

### Execute a Blueprint RPC

You can execute a Blueprint RPC like any other Blueprint event, but the same rules apply as for RPCs defined in C++. An RPC can only be executed from a replicated actor or actor component with a valid owner and owning connection.

`Remote` RPCs are not currently exposed to Blueprints.