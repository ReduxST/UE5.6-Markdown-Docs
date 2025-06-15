# Stats Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/stats-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/stats-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:25

---

The **Online Services Stats Interface** is used to upload stats and data to online services and complete stats queries. Stats Interface functionality is also used by other interfaces that rely on user gameplay statistics such as the Online Services' Achievements and Leaderboards Interfaces.

## API Overview

The following table provides a high-level description of the functions included in the Stats Interface.

| **Function** | **Description** |
| --- | --- |
| **Update** |   |
| [`UpdateStats`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IStats/UpdateStats) | Upload stats to the platform |
| **Query** |   |
| [`QueryStats`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IStats/QueryStats) | Query the stats of a user and cache the result in the interface. |
| [`BatchQueryStats`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IStats/BatchQueryStats) | Query the stats of a group of users and cache the results in the interface. |
| **Get** |   |
| [`GetCachedStats`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IStats/GetCachedStats) | Retrieve the cached user stats stored after a call to QueryStats or BatchQueryStats. |
| **Event Listening** |   |
| [`OnStatsUpdated`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IStats/OnStatsUpdated) | An event will fire as a result of changes to user stats. |

## Configuration

You can use the Stats Interface with either a corresponding platform backend or a `StatsNull` implementation. To use the Stats Interface, you must first configure the Stats Interface in your `DefaultEngine.ini` file:

DefaultEngine.ini

```
`[OnlineServices.Stats] +StatDefinitions=(Name=<STAT_NAME>, Id=<ID_NUMBER>, ModifyMethod=<METHOD>, DefaultValue="<TYPE>:<DEFAULT_VALUE>")`
Copy full snippet
```
\[OnlineServices.Stats\] +StatDefinitions=(Name=<STAT\_NAME>, Id=<ID\_NUMBER>, ModifyMethod=<METHOD>, DefaultValue="<TYPE>:<DEFAULT\_VALUE>")

**Stat Definitions** consist of the following fields:

-   `Name`: The name of the stat.
    -   This is the name that will be used to update and query stats with `UpdateStats` and `QueryStats` respectively.
-   `Id`: The ID of the stat.
    -   This is the corresponding configured stat ID in the platform portal.
-   `ModifyMethod`: Method prescribing how the stat will be updated.
    -   For non-`StatsNull` implementations, the Modify Method is configured in the platform portal.
    -   The Modify Method is used by the Achievements Interface on all implementations when using Title Managed achievements to determine whether an achievement meets the prescribed unlock rules.
-   `DefaultValue`: The type and default value of the stat.
    -   This prescribes the initial value of the stat.

To unlock achievements and update leaderboards with stats, you must specify corresponding stats in the Achievements and Leaderboards config sections of `DefaultEngine.ini`.

### Configuration Example

Here is a configuration example for the Online Services Stats interface:

DefaultEngine.ini

```
`[OnlineServices.Stats] +StatDefinitions=(Name=Stat_Use_Largest, Id=0, ModifyMethod=Largest, DefaultValue="Int64:0") +StatDefinitions=(Name=Stat_Use_Smallest, Id=1, ModifyMethod=Smallest, DefaultValue="Int64:999") +StatDefinitions=(Name=Stat_Use_Set, Id=2, ModifyMethod=Set, DefaultValue="Int64:0") +StatDefinitions=(Name=Stat_Use_Sum, Id=3, ModifyMethod=Sum, DefaultValue="Int64:0") +StatDefinitions=(Name=Stat_Type_Bool, Id=4, ModifyMethod=Set, DefaultValue="Bool:True") +StatDefinitions=(Name=Stat_Type_Double, Id=5, ModifyMethod=Smallest, DefaultValue="Double:9999.999")`
Copy full snippet
```
\[OnlineServices.Stats\] +StatDefinitions=(Name=Stat\_Use\_Largest, Id=0, ModifyMethod=Largest, DefaultValue="Int64:0") +StatDefinitions=(Name=Stat\_Use\_Smallest, Id=1, ModifyMethod=Smallest, DefaultValue="Int64:999") +StatDefinitions=(Name=Stat\_Use\_Set, Id=2, ModifyMethod=Set, DefaultValue="Int64:0") +StatDefinitions=(Name=Stat\_Use\_Sum, Id=3, ModifyMethod=Sum, DefaultValue="Int64:0") +StatDefinitions=(Name=Stat\_Type\_Bool, Id=4, ModifyMethod=Set, DefaultValue="Bool:True") +StatDefinitions=(Name=Stat\_Type\_Double, Id=5, ModifyMethod=Smallest, DefaultValue="Double:9999.999")

## Examples

This section contains a variety of code examples that guide you on how to:

-   [Query Stats](/documentation/en-us/unreal-engine/stats-interface-in-unreal-engine#querystats)
-   [Get Cached Stats](/documentation/en-us/unreal-engine/stats-interface-in-unreal-engine#getcachedstats)
-   [Listen for an event](/documentation/en-us/unreal-engine/stats-interface-in-unreal-engine#listenforanevent)
-   [Execute a Console Command](/documentation/en-us/unreal-engine/stats-interface-in-unreal-engine#executeaconsolecommand)

### Query Stats

```
`UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices(); UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();  UE::Online::FQueryStats::Params Params; Params.LocalAccountId = LocalAccountId; Params.TargetAccountId = TargetAccountId; Params.StatNames = {"StatA", "StatB"};  // See Note below Walkthrough for more information about this OnComplete call Stats->QueryStats(MoveTemp(Params)).OnComplete([](const UE::Online::TOnlineResult<FQueryStats>& Result) { if (Result.IsError()) 	{ 		const UE::Online::FOnlineError OnlineError = Result.GetErrorValue(); 		// Process OnlineError 		return; 	} 	const UE::Online::FQueryStats::Result QueriedStats = Result.GetOkValue(); 	// Process QueriedStats });`
Copy full snippet
```
UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices(); UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface(); UE::Online::FQueryStats::Params Params; Params.LocalAccountId = LocalAccountId; Params.TargetAccountId = TargetAccountId; Params.StatNames = {"StatA", "StatB"}; // See Note below Walkthrough for more information about this OnComplete call Stats->QueryStats(MoveTemp(Params)).OnComplete(\[\](const UE::Online::TOnlineResult<FQueryStats>& Result) { if (Result.IsError()) { const UE::Online::FOnlineError OnlineError = Result.GetErrorValue(); // Process OnlineError return; } const UE::Online::FQueryStats::Result QueriedStats = Result.GetOkValue(); // Process QueriedStats });

#### Walkthrough

1.  Use the default online services by calling `GetServices` with no parameters specified:
    
    ```
         `UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices();`
    Copy full snippet
    ```
    UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices();
2.  Access the Stats Interface for the default online services:
    
    ```
         `UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();`
    Copy full snippet
    ```
    UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();
3.  Instantiate the parameters necessary to query the `StatNames` of the `TargetAccountId`:
    
    ```
         `UE::Online::FQueryStats::Params Params;      Params.LocalAccountId = LocalAccountId;      Params.TargetAccountId = TargetAccountId;      Params.StatNames = {"StatA", "StatB"};`
    Copy full snippet
    ```
    UE::Online::FQueryStats::Params Params; Params.LocalAccountId = LocalAccountId; Params.TargetAccountId = TargetAccountId; Params.StatNames = {"StatA", "StatB"};
4.  Handle the `QueryStats.OnComplete` callback by processing the error or the queried stats:
    
    ```
         `Stats->QueryStats(MoveTemp(Params)).OnComplete([](const UE::Online::TOnlineResult<FQueryStats>& Result)      {          if (Result.IsError())          {              const UE::Online::FOnlineError OnlineError = Result.GetErrorValue();              // Process OnlineError              return;          }          const UE::Online::FQueryStats::Result QueriedStats = Result.GetOkValue();          // Process QueriedStats      });`
    Copy full snippet
    ```
    Stats->QueryStats(MoveTemp(Params)).OnComplete(\[\](const UE::Online::TOnlineResult<FQueryStats>& Result) { if (Result.IsError()) { const UE::Online::FOnlineError OnlineError = Result.GetErrorValue(); // Process OnlineError return; } const UE::Online::FQueryStats::Result QueriedStats = Result.GetOkValue(); // Process QueriedStats });

To bind to a member function, always prefer to use a UObject-derived class or a class that inherits from `TSharedFromThis` and use

```
`.OnComplete(this, &MyClass::OnQueryStatsComplete)`
Copy full snippet
```
.OnComplete(this, &MyClass::OnQueryStatsComplete)

This automatically selects `CreateUObject`, `CreateThreadSafeSP`, or `CreateSP`. The safest delegate creation call will be used. For more information, refer to the [Callback Format](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#callbackformat) section of the Online Services Overview page.

### Get Cached Stats

```
`UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices(); UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();  UE::Online::TOnlineResult<FGetCachedStats> CachedStats = Stats->GetCachedStats({}); if (CachedStats.IsError()) { 	UE::Online::FOnlineError OnlineError = CachedStats.GetErrorValue(); 	// Process OnlineError 	return; }  UE::Online::FGetCachedStats::Result& CachedStatsData = CachedStats.GetOkValue(); // Process CachedStatsData`
Copy full snippet
```
UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices(); UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface(); UE::Online::TOnlineResult<FGetCachedStats> CachedStats = Stats->GetCachedStats({}); if (CachedStats.IsError()) { UE::Online::FOnlineError OnlineError = CachedStats.GetErrorValue(); // Process OnlineError return; } UE::Online::FGetCachedStats::Result& CachedStatsData = CachedStats.GetOkValue(); // Process CachedStatsData

#### Walkthrough

1.  Use the default online services by calling `GetServices` with no parameters specified and access the Stats Interface:
    
    ```
         `UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices();      UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();`
    Copy full snippet
    ```
    UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices(); UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();
2.  Retrieve the cached stats through the Stats Interface with `Stats->GetCachedStats`:
    
    ```
         `UE::Online::TOnlineResult<UE::Online::FGetCachedStats> CachedStats = Stats->GetCachedStats({});`
    Copy full snippet
    ```
    UE::Online::TOnlineResult<UE::Online::FGetCachedStats> CachedStats = Stats->GetCachedStats({});
3.  Handle the `CachedStats` by processing the error or the cached stats data:
    
    ```
         `if (CachedStats.IsError())      {          UE::Online::FOnlineError OnlineError = CachedStats.GetErrorValue();          // Process OnlineError          return; 		      }      UE::Online::FGetCachedStats::Result& CachedStatsData = CachedStats.GetOkValue();      // Process CachedStatsData`
    Copy full snippet
    ```
    if (CachedStats.IsError()) { UE::Online::FOnlineError OnlineError = CachedStats.GetErrorValue(); // Process OnlineError return; } UE::Online::FGetCachedStats::Result& CachedStatsData = CachedStats.GetOkValue(); // Process CachedStatsData

### Listen for an Event

Event listening is handled differently than synchronous and asynchronous functions. An `FOnlineEventDelegateHandle` is created to handle the result of the `OnStatsUpdated` event, then `Unbind` must be called in your shutdown code to ensure proper destruction.

#### Walkthrough

1.  Declare an event handle in your class for the Stat interface.
    
    ```
         `UE::Online::FOnlineEventDelegateHandle StatEventHandle;`
    Copy full snippet
    ```
    UE::Online::FOnlineEventDelegateHandle StatEventHandle;
2.  In your init code, initialize the default online services, access the Stats interface, and process the stats when an event happens.
    
    ```
         `UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices();      UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface();      StatEventHandle = Stats->OnStatsUpdated().Add([](const UE::Online::FStatsUpdated& StatsUpdated)      {          // custom logic inside this lambda      });`
    Copy full snippet
    ```
    UE::Online::IOnlineServicesPtr OnlineServices = UE::Online::GetServices(); UE::Online::IStatsPtr Stats = OnlineServices->GetStatsInterface(); StatEventHandle = Stats->OnStatsUpdated().Add(\[\](const UE::Online::FStatsUpdated& StatsUpdated) { // custom logic inside this lambda });
3.  Ensure that you unbind the event handler in your shutdown code.
    
    ```
         `StatEventHandle.Unbind();`
    Copy full snippet
    ```
    StatEventHandle.Unbind();

### Execute a Console Command

For the general command-line syntax to run an async interface with a console command, refer to the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) documentation.

#### Example

To run the `QueryStats` function, execute the following console command:

```
`OnlineServices Index=0 Stats QueryStats 0 0 ["StatA", "StatB"]`
Copy full snippet
```
OnlineServices Index=0 Stats QueryStats 0 0 \["StatA", "StatB"\]

This command calls `QueryStats` from the Stats Interface with the default online services for the zeroth local user. In particular, the above command queries the default online services for `StatA` and `StatB` of this user.

## Reset Stats Data

During development and testing, the `ResetStats` function resets all provided player stats for the current title. Although policies vary across online services, you should not expect this function to work outside a testing environment. Be sure to remove any code that uses `ResetStats` from shipping builds, or use compile-time logic to mask the code like this:

```
`#if !UE_BUILD_SHIPPING // Code block with call to ResetStats #endif`
Copy full snippet
```
#if !UE\_BUILD\_SHIPPING // Code block with call to ResetStats #endif

## More Information

### Header File

Consult the `Stats.h` header file directly for more information as needed. The Stats Interface header file `Stats.h` is located in the directory:

```
`Engine\Plugins\Online\OnlineServices\Source\OnlineServicesInterface\Public\Online`
Copy full snippet
```
Engine\\Plugins\\Online\\OnlineServices\\Source\\OnlineServicesInterface\\Public\\Online

For instructions on how to obtain the UE source code, refer to our documentation on [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

### Function Parameters and Return Types

Refer to the [Functions](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#functions) section of the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) page for an explanation of function parameters and return types, including how to pass parameters and processing the results when functions return.