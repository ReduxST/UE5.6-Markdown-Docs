# Logging in Unreal

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/logging-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/logging-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:22

---

When debugging, logs are an invaluable tool that provide detailed information on what logic your code is executing. You can inspect data values passed between functions, and report potential issues.

-   Logging in Unreal provides several ways to keep an ordered record of events, function calls, and values of variables at any particular moment during runtime.
    
-   You can observe your logs in the Unreal Editor by navigating to **Window** > **Output Log**.
    

![output-log-window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5662d672-4241-46b3-9787-83f522265574/outputlogwindow.png)

The Output Log window is located in the Unreal Editor.

-   Logs are saved in a `.txt` file in your project's `Saved/Logs` directory

## UE\_LOG

**UE\_LOG** is a macro that logs a formatted message into the log file.

For example:

```
`UE_LOG(LogTemp, Warning, TEXT("Hello World"));`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("Hello World"));

-   The first input parameter `LogTemp` is the Category Name as provided to the `DEFINE_LOG_CATEGORY` macro. You can find these categories in the engine located in `CoreGlobals.h`. To create your own custom logging categories, see the [Define your own log category](/documentation/en-us/unreal-engine/logging-in-unreal-engine#defineyourownlogcategory) section.
    
-   The second input parameter `Warning` is a Verbosity level that is used to print a warning to the console and the log file. You can set varying verbosity levels to allow line breaks in a given log or set the log text color. See the [Log Verbosity](/documentation/en-us/unreal-engine/logging-in-unreal-engine#logverbosity) section for additional details.
    
-   The third input parameter `Text` is the format of the string literal in the style of the C language library function printf.
    

### Log Verbosity

**ELogVerbosity** is an enum that defines the verbosity levels of the logging system. It defines additional non-verbosity levels that allow breaking on a given log line or setting the color of the log text.

| Enum | Description |
| --- | --- |
| Fatal | Always prints a fatal error to the console and log file, then crashes even if logging is disabled. |
| Error | Prints an error to the console and log file. Commandlets and the editor collect and report errors. Error messages result in a commandlet failure. |
| Warning | Prints a warning to the console and log file. Commandlets and the editor collect and report warnings. |
| Display | Prints a message to the console and log file. |
| Log | Prints a message to the log file, however, it does not print to the console. |
| Verbose | Prints a verbose message to a log file if Verbose logging is enabled for the given category. This is usually used for detailed logging. |
| VeryVerbose | 
Prints a verbose message to a log file. If VeryVerbose logging is enabled, then this is used for detailed logging that would otherwise spam output.

Below are some sample Log masks and special Enum values:

```
`VeryVerbose, NumVerbosity, VerbosityMask	= 0xf, SetColor		= 0x40, // not actually a verbosity, used to set the color of an output device  BreakOnLog		= 0x80`
Copy full snippet
```
VeryVerbose, NumVerbosity, VerbosityMask = 0xf, SetColor = 0x40, // not actually a verbosity, used to set the color of an output device BreakOnLog = 0x80

 |

### Console Commands

It's possible to change the verbosity of different log categories from the command line using `-LogCmds=`

For example:

```
    `-LogCmds="LogDerivedDataCache Verbose"`  
Copy full snippet
```
\-LogCmds="LogDerivedDataCache Verbose"

This command lets you specify multiple categories, including an "all" category that toggles every log category to a specific verbosity level.

### Logging Fundamental Data Types

The table below provides some syntax formatting examples on how to log a particular data type.

| Data Type | Example |
| --- | --- |
| `FString` | 
```
`UE_LOG(LogTemp, Warning, TEXT("An Actor's name is %s"), *ExampleActor->GetName());`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("An Actor's name is %s"), \*ExampleActor->GetName());

 |
| `Bool` | 

```
`UE_LOG(LogTemp, Warning, TEXT("The boolean value is %s"), ( bExampleBool ? TEXT("true"): TEXT("false") ));`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("The boolean value is %s"), ( bExampleBool ? TEXT("true"): TEXT("false") ));

 |
| `Integer` | 

```
`UE_LOG(LogTemp, Warning, TEXT("The integer value is: %d"), ExampleInteger);`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("The integer value is: %d"), ExampleInteger);

 |
| `Float` | 

```
`UE_LOG(LogTemp, Warning, TEXT("The float value is: %f"), ExampleFloat);`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("The float value is: %f"), ExampleFloat);

 |
| `FVector` | 

```
`UE_LOG(LogTemp, Warning, TEXT("The vector value is: %s"), *ExampleVector.ToString());`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("The vector value is: %s"), \*ExampleVector.ToString());

 |
| `Multiple Specifiers` | 

```
`UE_LOG(LogTemp, Warning, TEXT("Current values are: vector %s, float %f, and integer %d"), *ExampleVector.ToString(), ExampleFloat, ExampleInteger);`
Copy full snippet
```
UE\_LOG(LogTemp, Warning, TEXT("Current values are: vector %s, float %f, and integer %d"), \*ExampleVector.ToString(), ExampleFloat, ExampleInteger);

 |

### Define Your Own Log Category

You can define your own log category and use it in your C++ code example. This might be beneficial if your examples include multiple files or frameworks that require distinct categorization. In the relevant header file, add the following just below the include directives:

```
`DECLARE_LOG_CATEGORY_EXTERN(<LOG_CATEGORY>, <VERBOSITY_LEVEL>, All);`
Copy full snippet
```
DECLARE\_LOG\_CATEGORY\_EXTERN(<LOG\_CATEGORY>, <VERBOSITY\_LEVEL>, All);

where `<LOG_CATEGORY>` is your custom log category string and is one of the following table values:

**Log verbosity levels**

| Verbosity Level | Printed in Console | Printed in Editor Log | Text Color | Additional Information |
| --- | --- | --- | --- | --- |
| Fatal | Y | NA | NA | Crashes session. |
| Error | Y | Y | Red | NA |
| Warning | Y | Y | Yellow | NA |
| Display | Y | Y | Grey | NA |
| Log | N | Y | Grey | NA |
| Verbose | N | N | NA | NA |
| VeryVerbose | N | N | NA | Can use Log masks and special Enum values to set the text color. |

In the relevant C++ file, add the following just below the include directives:

```
`DEFINE_LOG_CATEGORY(<LOG_CATEGORY>);`
Copy full snippet
```
DEFINE\_LOG\_CATEGORY(<LOG\_CATEGORY>);

Now you can use this category in your C++ file code as:

```
`UE_LOG(<LOG_CATEGORY>, <VERBOSITY_LEVEL>, TEXT("My log string."));`
Copy full snippet
```
UE\_LOG(<LOG\_CATEGORY>, <VERBOSITY\_LEVEL>, TEXT("My log string."));

You can implement your own output by deriving from `FOutputDevice`.

## UE\_LOGFMT

**UE\_LOGFMT** records a structured log event that supports **Positional** or **Named** parameters but can not mix both styles. To use this macro you, need to include the `Logging/StructuredLog.h` library declaration.

  

The `UE_LOGFMT` macro was introduced in Unreal Engine 5.2. Check that your current Engine version is up to date.

| Parameter Name | Description |
| --- | --- |
| Positional | 
When using positional parameters, the field values must exactly match the field referenced by format.

For example:

```
``UE_LOGFMT(LogCore, Warning, "Loading `{Name}` failed with error {Error}", Package->GetName(),  ErrorCode);``
Copy full snippet
```
UE\_LOGFMT(LogCore, Warning, "Loading \`{Name}\` failed with error {Error}", Package->GetName(), ErrorCode);

 |
| Named | 

When using Named parameters, the field values must contain every field reference by format. The order is irrelevant and extra fields are permitted.

For example:

```
``UE_LOGFMT(LogCore, Warning, "Loading `{Name}` failed with error {Error}",("Name", Package->GetName()), ("Error", ErrorCode),("Flags", LoadFlags));``
Copy full snippet
```
UE\_LOGFMT(LogCore, Warning, "Loading \`{Name}\` failed with error {Error}",("Name", Package->GetName()), ("Error", ErrorCode),("Flags", LoadFlags));

Field names must match the "\[A-Za-z0-9\_\]+" format and must be unique within this log event. Field values are serialized using SerializeForLog or the operator `<<(FCbWriter&, FieldType)`.

-   **CategoryName**: Name of a log category declared by DECLARE\_LOG\_CATEGORY\_\*.
    
-   **Verbosity**: Name of a log verbosity level from `ELogVerbosity`.
    
-   **Format**: Formats the string in the style of `FLogTemplate`.
    
-   **Fields\[0-16\]**: Zero to sixteen fields or field values.
    



 |

### On-screen debug messages

Another useful method of communicating information is through on-screen debug messages. You can add an on-screen debug message with the following code:

```
`if (GEngine) {     GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::White, TEXT("This is an Example on-screen debug message.")); }`
Copy full snippet
```
if (GEngine) { GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::White, TEXT("This is an Example on-screen debug message.")); }

-   The first input parameter *key* takes a unique integer key to prevent the same message from being added multiple times.
    
-   The second input parameter *TimeToDisplay* takes a float for how many seconds to display the message before it fades away.
    
-   The third input parameter *DisplayColor* takes a color to display the text in.
    
-   The fourth input parameter *DebugMessage* is the message to display. You can use format specifiers and variables in on-screen debug messages similar to logs.