# Online Subsystem Types

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-types-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-types-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:55

---

This document serves to define the different data structures that are used throughout the online subsystem.

### IOnlinePlatformData

**IOnlinePlatformData** is the base class for anything meant to be opaque so that the data can be passed around without consideration for the data it contains. A human-readable version of the data is available via the **ToString()** function; otherwise, nothing but platform code should try to operate directly on the data.

There are often platform-specific representations of various constructs that, while they need to be handled by the game, do not need their details exposed. This allows the game to hold onto the data and replicate it to other machines without understanding the details.

Classes deriving from IOnlinePlatformData:

-   [FUniqueNetId](/documentation/en-us/unreal-engine/online-subsystem-types-in-unreal-engine#funiquenetid)
-   [FSharedContentHandle](/documentation/en-us/unreal-engine/online-subsystem-types-in-unreal-engine#fsharedcontenthandle)
-   [FSessionInfo](/documentation/en-us/unreal-engine/online-subsystem-types-in-unreal-engine#fsessioninfo)

#### Functions

```
	`/** 	 * Get the raw byte representation of this opaque data 	 * This data is platform dependent and shouldn't be manipulated directly 	 * @return byte array of size GetSize() 	 */ 	virtual const uint8* GetBytes() const = 0;  	/** 	 * Get the size of the opaque data 	 * @return size in bytes of the data representation 	 */ 	virtual int32 GetSize() const = 0;  	/** 	 * Check the validity of the opaque data 	 * @return true if this is well formed data, false otherwise 	 */ 	virtual bool IsValid() const = 0;  	/** 	 * Get a human readable representation of the opaque data 	 * Shouldn't be used for anything other than logging/debugging 	 * @return data in string form 	 */ 	virtual FString ToString() const = 0;`
Copy full snippet
```
/\*\* \* Get the raw byte representation of this opaque data \* This data is platform dependent and shouldn't be manipulated directly \* @return byte array of size GetSize() \*/ virtual const uint8\* GetBytes() const = 0; /\*\* \* Get the size of the opaque data \* @return size in bytes of the data representation \*/ virtual int32 GetSize() const = 0; /\*\* \* Check the validity of the opaque data \* @return true if this is well formed data, false otherwise \*/ virtual bool IsValid() const = 0; /\*\* \* Get a human readable representation of the opaque data \* Shouldn't be used for anything other than logging/debugging \* @return data in string form \*/ virtual FString ToString() const = 0;

### FUniqueNetId

**FUniqueNetId** contains a profile service online ID and can represent anything from an individual player, friend or a session.

### FSharedContentHandle

**FSharedContentHandle** contains a profile service shared file handle. This handle can be passed around and used to access shared content from anywhere, given proper permissions.

### FSessionInfo

**FSessionInfo** contains a session's platform-specific info. In most cases, this would be information such as a session identifier, host address, or other means of identifying and connecting to a created session.

See: [Session Interface](/documentation/en-us/unreal-engine/online-subsystem-session-interface-in-unreal-engine)

### FEmsFile

**FEmsFile** is metadata about a given downloadable file. This structure is used when enumerating available data from a given service.

Contains the following elements:

-   Hash - the hash value of the given file contents.
-   Filename - the filename as downloaded.
-   Logical name - the name that maps to the downloaded filename.
-   File size - size of the file.

### FTitleFile

**FTitleFile** is the internal structure that holds the data used in downloading a file asynchronously from the online service.

Contains the following elements:

-   Filename - the filename as downloaded.
-   Async state - the state of the downloaded file. (see: [Async States](/documentation/en-us/unreal-engine/online-subsystem-types-in-unreal-engine#eonlineasynctaskstate) )
-   Data - a buffer containing the file contents.

### EOnlineAsyncTaskState

**EOnlineAsyncTaskState** is a simple enum representing the possible states for an asynchronous operation.

```
		`/** The task has not been started */ 		NotStarted, 		/** The task is currently being processed */ 		InProgress, 		/** The task has completed successfully */ 		Done, 		/** The task failed to complete */ 		Failed`
Copy full snippet
```
/\*\* The task has not been started \*/ NotStarted, /\*\* The task is currently being processed \*/ InProgress, /\*\* The task has completed successfully \*/ Done, /\*\* The task failed to complete \*/ Failed