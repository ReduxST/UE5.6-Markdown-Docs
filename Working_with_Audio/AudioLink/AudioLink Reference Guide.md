# AudioLink Reference Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audiolink-reference-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/audiolink-reference-guide)  
**Processed:** 2025-06-14 16:09:11

---

You can create a basic **AudioLink** implementation in just a few lines of code with just a `IAudioLinkFactory` definition and registration. However, other API types can help you further build out your implementation.

Below you'll find summaries of each of the core AudioLink C++ types and some code examples.

You can find the AudioLink source code at `Engine\Source\Runtime\AudioLink\`.

## IAudioLinkFactory

Every AudioLink implementation needs a factory class derived from `IAudioLinkFactory`, which has several pure virtual functions that define the implementation's entry points.

You must implement each function, as returning null results in an assert. Unreal Engine (UE) expects all calls dispatched to be thread-safe and ideally lockless to return efficiently.

You can use parameter structs instead of numerous individual parameters to simplify the extension of these function calls.

You can only register a single factory object; additional factories assert a fatal error on startup.

### Plugin Implementation

AudioLink uses the `IModularFeature` interface to extend UE. The `IAudioLinkFactory` constructor handles registration, so creating an instance of your factory is sufficient for recognition. Handle this in the `StartupModule()` of your implementation.

There are different ways to implement plugins in UE, but the `IModularFeature` interface is the most common for audio extensions.

### Example: Submix AudioLink Implementation

```
`// Parameters use when creating a Submix Audio Link  struct FAudioLinkSubmixCreateArgs { 	TWeakObjectPtr<const USoundSubmix> Submix; 	FAudioDevice* Device = nullptr; 	TWeakObjectPtr<const UAudioLinkSettingsAbstract> Settings; };  // Create a Submix Audio Link. // @param InCreateArgs Arguments used to create the AudioLink instance // @return The newly created Link instance (if successful). virtual TUniquePtr<IAudioLink> CreateSubmixAudioLink(const FAudioLinkSubmixCreateArgs& InCreateArgs) = 0;`
Copy full snippet
```
// Parameters use when creating a Submix Audio Link struct FAudioLinkSubmixCreateArgs { TWeakObjectPtr<const USoundSubmix> Submix; FAudioDevice\* Device = nullptr; TWeakObjectPtr<const UAudioLinkSettingsAbstract> Settings; }; // Create a Submix Audio Link. // @param InCreateArgs Arguments used to create the AudioLink instance // @return The newly created Link instance (if successful). virtual TUniquePtr<IAudioLink> CreateSubmixAudioLink(const FAudioLinkSubmixCreateArgs& InCreateArgs) = 0;
```
	`/** 	* Parameters use when creating a Submix Audio Link  	*/ 	struct FAudioLinkSubmixCreateArgs 	{ 		TWeakObjectPtr<const USoundSubmix> Submix; 		FAudioDevice* Device = nullptr; 		TWeakObjectPtr<const UAudioLinkSettingsAbstract> Settings; 	};  	/** 	* Create a Submix Audio Link. 	* @param InCreateArgs Arguments used to create the AudioLink instance 	* @return The newly created Link instance (if successful). 	*/ 	virtual TUniquePtr<IAudioLink> CreateSubmixAudioLink(const FAudioLinkSubmixCreateArgs& InCreateArgs) = 0;`
Copy full snippet
```
/\*\* \* Parameters use when creating a Submix Audio Link \*/ struct FAudioLinkSubmixCreateArgs { TWeakObjectPtr<const USoundSubmix> Submix; FAudioDevice\* Device = nullptr; TWeakObjectPtr<const UAudioLinkSettingsAbstract> Settings; }; /\*\* \* Create a Submix Audio Link. \* @param InCreateArgs Arguments used to create the AudioLink instance \* @return The newly created Link instance (if successful). \*/ virtual TUniquePtr<IAudioLink> CreateSubmixAudioLink(const FAudioLinkSubmixCreateArgs& InCreateArgs) = 0;

#### Example: Factory Implementation

```
	`class FAudioLinkExampleFactory : public IAudioLinkFactory 	{ 	public: 		FAudioLinkExampleFactory() = default; 		virtual ~FAudioLinkExampleFactory() = default;  		static FName GetFactoryNameStatic();  	protected: 		/** Begin IAudioLinkFactory */ 		FName GetFactoryName() const override; 		TSubclassOf<UAudioLinkSettingsAbstract> GetSettingsClass() const override; 		TUniquePtr<IAudioLink> CreateSubmixAudioLink(const FAudioLinkSubmixCreateArgs&) override; 		TUniquePtr<IAudioLink> CreateSourceAudioLink(const FAudioLinkSourceCreateArgs&) override; 		FAudioLinkSourcePushedSharedPtr CreateSourcePushedAudioLink(const FAudioLinkSourcePushedCreateArgs&) override; 		FAudioLinkSynchronizerSharedPtr CreateSynchronizerAudioLink() override; 		/** End IAudioLinkFactory */ 	};`
Copy full snippet
```
class FAudioLinkExampleFactory : public IAudioLinkFactory { public: FAudioLinkExampleFactory() = default; virtual ~FAudioLinkExampleFactory() = default; static FName GetFactoryNameStatic(); protected: /\*\* Begin IAudioLinkFactory \*/ FName GetFactoryName() const override; TSubclassOf<UAudioLinkSettingsAbstract> GetSettingsClass() const override; TUniquePtr<IAudioLink> CreateSubmixAudioLink(const FAudioLinkSubmixCreateArgs&) override; TUniquePtr<IAudioLink> CreateSourceAudioLink(const FAudioLinkSourceCreateArgs&) override; FAudioLinkSourcePushedSharedPtr CreateSourcePushedAudioLink(const FAudioLinkSourcePushedCreateArgs&) override; FAudioLinkSynchronizerSharedPtr CreateSynchronizerAudioLink() override; /\*\* End IAudioLinkFactory \*/ };

## UAudioLinkSettingsAbstract

Every AudioLink implementation needs a settings class derived from `UAudioLinkSettingsAbstract` to create links with associated data, like buffer sizes, handshakes, and UAsset references.

### Example: Settings Implementation

```
	`UCLASS(config = Engine, defaultconfig) 	class AUDIOLINKEXAMPLERUNTIME_API UAudioLinkSettingsExample : public UAudioLinkSettingsAbstract 	{ 		GENERATED_BODY()  		UPROPERTY(Config, EditAnywhere, Category = "Example|AudioLink") 		float MyBufferSize = 1.0f; 	};  	class FAudioLinkSettingsProxyExample : public IAudioLinkSettingsProxy 	{ 	public: 		FAudioLinkSettingsProxyExample(const UAudioLinkSettingsExample&); 		virtual ~FAudioLinkSettingsProxyExample() = default;  		float GetMyBufferSize() const { return MyBufferSize; }  	private: 	#if WITH_EDITOR 		void RefreshFromSettings(UAudioLinkSettingsAbstract* InSettings, FPropertyChangedEvent& InPropertyChangedEvent) override 		{	 			MyBufferSize = CastChecked<UAudioLinkSettingsExample>(InSettings)->MyBufferSize; 		} 	#endif //WITH_EDITOR  		float MyBufferSize = 0; 	};`
Copy full snippet
```
UCLASS(config = Engine, defaultconfig) class AUDIOLINKEXAMPLERUNTIME\_API UAudioLinkSettingsExample : public UAudioLinkSettingsAbstract { GENERATED\_BODY() UPROPERTY(Config, EditAnywhere, Category = "Example|AudioLink") float MyBufferSize = 1.0f; }; class FAudioLinkSettingsProxyExample : public IAudioLinkSettingsProxy { public: FAudioLinkSettingsProxyExample(const UAudioLinkSettingsExample&); virtual ~FAudioLinkSettingsProxyExample() = default; float GetMyBufferSize() const { return MyBufferSize; } private: #if WITH\_EDITOR void RefreshFromSettings(UAudioLinkSettingsAbstract\* InSettings, FPropertyChangedEvent& InPropertyChangedEvent) override { MyBufferSize = CastChecked<UAudioLinkSettingsExample>(InSettings)->MyBufferSize; } #endif //WITH\_EDITOR float MyBufferSize = 0; };

## IAudioLinkSettingsProxy

AudioLink Settings follow a proxy design pattern, so they can safely exist outside the game thread where audio typically executes. A thread-safe copy of the settings is created and attached as a shared pointer to the setting's `UObject`.

This approach has two primary benefits.

-   It provides garbage collection protection, as any threads that still have the shared pointer can continue to operate safely.
-   `PostEditChangedProperty` automatically ferries data to the proxy when changes are made in the editor so that settings can behave like a standard asset.

All AudioLink Settings assets must implement a proxy of themselves and handle refreshing when the owning Asset changes via the `RefreshFromSettings` function.

Additionally, you should implement default settings for your properties, which serializes in the `DefaultEngine.ini`. In the Example: Settings Implementation, this is achieved via the `defaultconfig` markup on the settings object.

The settings default is used in cases where the property has not been set, so it is unnecessary to pass it every time you create an AudioLink.

### UFactory Implementation

Unreal Engine serializes AudioLink Settings as an asset. As a result, you are responsible for implementing an asset factory for the settings class so you can create the asset.

#### Example: Standard Settings Factory Implementation

```
	`class FAssetTypeActions_AudioLinkExampleSettings : public FAssetTypeActions_Base 	{ 		public: 			virtual FText GetName() const override; 			virtual FColor GetTypeColor() const override; 			virtual const TArray<FText>& GetSubMenus() const override; 			virtual UClass* GetSupportedClass() const override; 			virtual uint32 GetCategories() override; 	};  	UCLASS(hidecategories = Object, MinimalAPI) 	class UAudioLinkExampleSettingsFactory : public UFactory 	{ 		GENERATED_UCLASS_BODY()  		virtual UObject* FactoryCreateNew(UClass* Class, UObject* InParent, FName Name, EObjectFlags Flags, UObject* Context, FFeedbackContext* Warn) override;  		virtual uint32 GetMenuCategories() const override; 	};`
Copy full snippet
```
class FAssetTypeActions\_AudioLinkExampleSettings : public FAssetTypeActions\_Base { public: virtual FText GetName() const override; virtual FColor GetTypeColor() const override; virtual const TArray<FText>& GetSubMenus() const override; virtual UClass\* GetSupportedClass() const override; virtual uint32 GetCategories() override; }; UCLASS(hidecategories = Object, MinimalAPI) class UAudioLinkExampleSettingsFactory : public UFactory { GENERATED\_UCLASS\_BODY() virtual UObject\* FactoryCreateNew(UClass\* Class, UObject\* InParent, FName Name, EObjectFlags Flags, UObject\* Context, FFeedbackContext\* Warn) override; virtual uint32 GetMenuCategories() const override; };

## IAudioLink

`IAudioLink` is the primary abstraction used by the `IAudioLinkFactory` and is often returned by a `TUniquePtr`. It's an opaque type designed to contain the hidden details of plugin-specific implementation and in a thread-safe shared pointer to both a consumer and producer. The consumer object maintains a weak reference to the producer and safely terminates the connection when the producer is deleted, typically when the link ends due to elapsing lifetime.

### Example: Instance Implementation

```
	`//* AudioLink Instance, a container holding shared pointers for lifetime management. */ 	struct FExampleLink : IAudioLink 	{ 		// Circular buffer (submix/source) that listening for new buffers 		FSharedBufferedOutputPtr ProducerSP;   		// Example client 		FSharedExampleAudioInputClientPtr ConsumerSP;	  		// ... 	};`
Copy full snippet
```
//\* AudioLink Instance, a container holding shared pointers for lifetime management. \*/ struct FExampleLink : IAudioLink { // Circular buffer (submix/source) that listening for new buffers FSharedBufferedOutputPtr ProducerSP; // Example client FSharedExampleAudioInputClientPtr ConsumerSP; // ... };

## IAudioMixerPlatformInterface

When you register an AudioLink Factory with UE, an AudioLink Platform Mixer is instantiated and hooks into AudioLink instead of the platform's hardware. Traditionally, third-party libraries have had to modify `.ini` files to prevent this, but AudioLink makes this less troublesome.

## IBufferedAudioOutput

Most AudioLink instances use a class derived from `IBufferedAudioOutput` to create a producer object. Internally, they function as a circular buffer of pulse-code modulation (PCM) data waiting to be drained by a consumer object.

A circular buffer is a first in, first out (FIFO) data structure that buffers PCM data across UE boundaries. For AudioLink, these are atomic but not lockless.

Implementations of this interface are already defined in the source code (`FBufferedSourceListener` and `FBufferedSubmixListener`), so it's likely unnecessary to build your own derived versions of these types.

Often, the link is created before the format of the incoming audio is recognized. As a result, an `OnFormatKnown` delegate fires once the format is known. You should set the delegate and start playback when it occurs.

Give careful consideration to how much space you allocate for these objects. A size too large can lead to latency, but too small can lead to buffer underruns. Typically, you should use a size at a 2:1 or higher ratio of the consumer's bitrate.

### Lifetime of a Link Instance

The lifetime of a link instance depends on its type.

-   A source link generally lives for the lifetime of a source's playback. Once over, the source is deleted, severing the link. This severance is mainly due to the format of the source potentially being different for every new source.
-   A submix link is open while the submix is running, which is usually the application's runtime. This can lead to issues caused by instance lifetime, especially in the editor. See [Troubleshooting](/documentation/en-us/unreal-engine/audiolink-overview#troubleshooting) for more information.

## IAudioLinkSynchronizer

Every AudioLink implementation needs a synchronizer class derived from `IAudioLinkSynchronizer`, which contains registration and removal calls for setting various callbacks. This class synchronizes to another clock source, so UE and the external application can stay in sync.

You must provide thread-safe delegates for each of these callbacks:

-   `Suspend`
-   `Resume`
-   `OpenStream`
-   `CloseStream`
-   `BeginRender`
-   `EndRender`

Use `OpenStream` to notify UE of the format of an external AudioLink Factory. This notification is most useful for matching block / sample rates and channel counts.

Use `BeginRender` and `EndRender` to synchronize UE with the external renderer.

### Example: Synchronizer Implementation

```
	`struct FExampleSynchronizerAudioLink : IAudioLinkSynchronizer  	{ 		IAudioLinkSynchronizer::FOnSuspend		OnSuspend; 		IAudioLinkSynchronizer::FOnResume		OnResume; 		IAudioLinkSynchronizer::FOnOpenStream	OnOpenStream; 		IAudioLinkSynchronizer::FOnCloseStream	OnCloseStream; 		IAudioLinkSynchronizer::FOnBeginRender	OnBeginRender; 		IAudioLinkSynchronizer::FOnEndRender	OnEndRender;  		FRWLock RwLock;  		// ...  		#define MAKE_DELEGATE_FUNC(X)\ 			FDelegateHandle Register##X##Delegate(const FOn##X::FDelegate& InDelegate) override\ 			{\ 				FWriteScopeLock WriteLock(RwLock);\ 				return On##X.Add(InDelegate);\ 			}\ 			bool Remove##X##Delegate(const FDelegateHandle& InHandle) override\ 			{\ 				FWriteScopeLock WriteLock(RwLock);\ 				return On##X.Remove(InHandle);\ 			}  		MAKE_DELEGATE_FUNC(Suspend) 		MAKE_DELEGATE_FUNC(Resume) 		MAKE_DELEGATE_FUNC(OpenStream) 		MAKE_DELEGATE_FUNC(CloseStream) 		MAKE_DELEGATE_FUNC(BeginRender) 		MAKE_DELEGATE_FUNC(EndRender)  		#undef MAKE_DELEGATE_FUNC 	};`
Copy full snippet
```
struct FExampleSynchronizerAudioLink : IAudioLinkSynchronizer { IAudioLinkSynchronizer::FOnSuspend OnSuspend; IAudioLinkSynchronizer::FOnResume OnResume; IAudioLinkSynchronizer::FOnOpenStream OnOpenStream; IAudioLinkSynchronizer::FOnCloseStream OnCloseStream; IAudioLinkSynchronizer::FOnBeginRender OnBeginRender; IAudioLinkSynchronizer::FOnEndRender OnEndRender; FRWLock RwLock; // ... #define MAKE\_DELEGATE\_FUNC(X)\\ FDelegateHandle Register##X##Delegate(const FOn##X::FDelegate& InDelegate) override\\ {\\ FWriteScopeLock WriteLock(RwLock);\\ return On##X.Add(InDelegate);\\ }\\ bool Remove##X##Delegate(const FDelegateHandle& InHandle) override\\ {\\ FWriteScopeLock WriteLock(RwLock);\\ return On##X.Remove(InHandle);\\ } MAKE\_DELEGATE\_FUNC(Suspend) MAKE\_DELEGATE\_FUNC(Resume) MAKE\_DELEGATE\_FUNC(OpenStream) MAKE\_DELEGATE\_FUNC(CloseStream) MAKE\_DELEGATE\_FUNC(BeginRender) MAKE\_DELEGATE\_FUNC(EndRender) #undef MAKE\_DELEGATE\_FUNC };