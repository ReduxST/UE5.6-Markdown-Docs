# Actor Component Replication

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/replicating-actor-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/replicating-actor-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:07

---

An actor component extends an actor's behavior. An actor component is a special type of object that you can attach to an actor as a subobject. Actor components do not replicate by default, but you can configure any actor component to replicate as part of its owning actor. Actor components can replicate their own properties and subobjects, as well as call actor component class-defined remote procedure calls (RPCs) in the same way actors can.

To replicate an actor component as part of your actor, you must make sure that:

-   The actor that owns your actor component is set to replicate.
-   The actor component is set to replicate.

## Types of Actor Components

### Static Actor Components

A *static actor component* is an actor component spawned when the owning actor is spawned. Static components are created in an actor's C++ constructor as a default subobject or in the Blueprint Editor's [Component Mode](/documentation/en-us/unreal-engine/components-window-in-unreal-engine).

#### Replicate a Static Actor Component

To replicate an actor component created in your actor constructor, follow these steps:

1.  In your actor constructor:
    -   Set your actor to replicate with `bReplicates = true;`.
    -   Create your actor component in your actor constructor with `CreateDefaultSubobject<T>`:
        
        ```
                  `AMyActor::AMyActor()           {               bReplicates = true;               MyActorComponent = CreateDefaultSubobject<UMyActorComponent>(TEXT("MyActorComponent"));           }`
        Copy full snippet
        ```
        AMyActor::AMyActor() { bReplicates = true; MyActorComponent = CreateDefaultSubobject<UMyActorComponent>(TEXT("MyActorComponent")); }
2.  In you actor component constructor:
    -   Set your actor component to replicate with `UActorComponent::SetIsReplicatedByDefault`:
        
        ```
                  `UMyActorComponent::UMyActorComponent()           {               SetIsReplicatedByDefault(true);           }`
        Copy full snippet
        ```
        UMyActorComponent::UMyActorComponent() { SetIsReplicatedByDefault(true); }

### Dynamic Actor Components

A *dynamic actor component* is an actor component spawned on the server at runtime. The creation or deletion of a dynamic actor component replicates to connected clients. Dynamic actor components work similarly to actors.

Clients can spawn their own, local, non-replicating dynamic actor components.

#### Replicate a Dynamic Actor Component

To replicate an actor component created dynamically at runtime, follow these steps:

1.  In your actor constructor:
    -   Set your actor to replicate with `bReplicates = true;`.
    -   Create your actor component in your gameplay code with `NewObject<T>`:
        
        ```
                  `MyActorComponent = NewObject<UMyActorComponent>();`
        Copy full snippet
        ```
        MyActorComponent = NewObject<UMyActorComponent>();
2.  When you want to replicate your new actor component:
    -   Set your actor component to replicate with `UActorComponent::SetIsReplicated`:
        
        ```
                  `if (MyActorComponent)           {               MyActorComponent->SetIsReplicated(true);           }`
        Copy full snippet
        ```
        if (MyActorComponent) { MyActorComponent->SetIsReplicated(true); }

### Blueprint Actor Components

You can spawn both static and dynamic actor components in Blueprint.

#### Replicate a Static Blueprint Actor Component

To replicate a static actor component in Blueprint, toggle the **Replicates** boolean field in your actor component's **Details Panel**. You only need to replicate an actor component if the component has properties or events that you need to replicate.

You can set an actor component to replicate by default in the Component Replication section of the Details Panel.

The **Component Replication** section only appears on components that support some form of replication.

#### Replicate a Dynamic Blueprint Actor Component

To replicate a dynamic actor component in Blueprint, call the **Set Is Replicated** function with the **Should Replicate** field toggled on.

Begin Object Class=/Script/BlueprintGraph.K2Node\_CustomEvent Name="K2Node\_CustomEvent\_0" ExportPath="/Script/BlueprintGraph.K2Node\_CustomEvent'/Game/MyBlueprints/BP\_MyActor.BP\_MyActor:EventGraph.K2Node\_CustomEvent\_0'" CustomFunctionName="Event ReplicateComponent" NodePosY=681 NodeGuid=818B4FBA4AB8D2434CFAECA23B4FA1A1 CustomProperties Pin (PinId=421A30E3469187EF6B5740AE931D3780,PinName="OutputDelegate",Direction="EGPD\_Output",PinType.PinCategory="delegate",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(MemberParent="/Script/Engine.BlueprintGeneratedClass'/Game/MyBlueprints/BP\_MyActor.BP\_MyActor\_C'",MemberName="Event ReplicateComponent",MemberGuid=818B4FBA4AB8D2434CFAECA23B4FA1A1),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=62D2FC444CA20DB5E9B3A8955CAC3E2E,PinName="then",Direction="EGPD\_Output",PinType.PinCategory="exec",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(K2Node\_CallFunction\_0 06F6405B4C0EAC380F0686AAB61C9142,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/BlueprintGraph.K2Node\_CallFunction Name="K2Node\_CallFunction\_0" ExportPath="/Script/BlueprintGraph.K2Node\_CallFunction'/Game/MyBlueprints/BP\_MyActor.BP\_MyActor:EventGraph.K2Node\_CallFunction\_0'" FunctionReference=(MemberParent="/Script/CoreUObject.Class'/Script/Engine.ActorComponent'",MemberName="SetIsReplicated") NodePosX=416 NodePosY=681 NodeGuid=BF0399784595F2FE6960EB96EC2720C3 CustomProperties Pin (PinId=06F6405B4C0EAC380F0686AAB61C9142,PinName="execute",PinToolTip="\\nExec",PinType.PinCategory="exec",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(K2Node\_CustomEvent\_0 62D2FC444CA20DB5E9B3A8955CAC3E2E,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=B9CD644C4D6D4BA1C0974A9E6587E6C6,PinName="then",PinToolTip="\\nExec",Direction="EGPD\_Output",PinType.PinCategory="exec",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=B3041B214B81F199F983ACB72C6313B4,PinName="self",PinFriendlyName=NSLOCTEXT("K2Node", "Target", "Target"),PinToolTip="Target\\nActor Component Object Reference",PinType.PinCategory="object",PinType.PinSubCategory="",PinType.PinSubCategoryObject="/Script/CoreUObject.Class'/Script/Engine.ActorComponent'",PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(K2Node\_VariableGet\_0 148F62B441C32524EE4B75A258C6EDA3,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=63B137774CD10EC982E1EB9977EDDB2A,PinName="ShouldReplicate",PinToolTip="Should Replicate\\nBoolean",PinType.PinCategory="bool",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="true",AutogeneratedDefaultValue="false",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/BlueprintGraph.K2Node\_VariableGet Name="K2Node\_VariableGet\_0" ExportPath="/Script/BlueprintGraph.K2Node\_VariableGet'/Game/MyBlueprints/BP\_MyActor.BP\_MyActor:EventGraph.K2Node\_VariableGet\_0'" VariableReference=(MemberName="BP\_MyActorComponent",bSelfContext=True) NodePosX=128 NodePosY=784 NodeGuid=77ABE40B46D72F9B9E5F3CAF2525B65C CustomProperties Pin (PinId=148F62B441C32524EE4B75A258C6EDA3,PinName="BP\_MyActorComponent",Direction="EGPD\_Output",PinType.PinCategory="object",PinType.PinSubCategory="",PinType.PinSubCategoryObject="/Script/Engine.BlueprintGeneratedClass'/Game/MyBlueprints/BP\_MyActorComponent.BP\_MyActorComponent\_C'",PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(K2Node\_CallFunction\_0 B3041B214B81F199F983ACB72C6313B4,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=2E0192B34CCBEC99A1F485B839A7E62D,PinName="self",PinFriendlyName=NSLOCTEXT("K2Node", "Target", "Target"),PinType.PinCategory="object",PinType.PinSubCategory="",PinType.PinSubCategoryObject="/Script/Engine.BlueprintGeneratedClass'/Game/MyBlueprints/BP\_MyActor.BP\_MyActor\_C'",PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=True,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object

## Replicate Actor Component Properties

You can replicate actor component properties the same way that you replicate actor properties. For more information about how to replicate actor properties, see the [Replicate Actor Properties](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine) documentation.

## Actor Component Remote Procedure Calls

You can define remote procedure calls (RPCs) within your actor component class and call them the same way that you call actor RPCs. For more information about how to define, implement, and call RPCs, see the [Remote Procedure Calls](/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine) documentation.

## Replicate Actor Component Subobjects

Actor Components can have their own replicated subobjects list in the same way as actors. They use the same API as actors for registering and unregistering their subobjects. Subobjects within an actor component can have replication conditions as well.

The owning component must be replicated to a connection before the conditions of its replicated subobjects are checked. For example, if a subobject has the `COND_OwnerOnly` condition, but is registered to a component that uses the `COND_SkipOwner` condition, the subobject never replicates, because the owner is skipped..

For more information on how to replicate subobjects, see the [Replicate Actor Subobjects](/documentation/en-us/unreal-engine/replicating-uobjects-in-unreal-engine) documentation.

## Bandwidth Overhead

Each replicating actor component within an actor adds:

-   A Network Globally Unique Identifier (NetGUID) header consisting of 4 bytes.
-   All replicated properties and the space required.
-   A footer consisting of approximately 1 byte.

When considering bandwidth overhead, there are three areas to be aware of:

-   *Replication*: Compared to replicating an entire actor, the impact of replicating a property on an actor component is relatively low.
-   *Calling an RPC*: Calling an RPC from an actor component has more overhead than calling from directly within an actor. To mitigate this, consider routing your actor component RPCs through your actor. For an example of this, see the [character movement component](/documentation/en-us/unreal-engine/understanding-networked-movement-in-the-character-movement-component-for-unreal-engine).
-   *Amount of actor components*: Actor components are relatively small. However, if you use a high number of components and component subobjects, your performance might be lower.