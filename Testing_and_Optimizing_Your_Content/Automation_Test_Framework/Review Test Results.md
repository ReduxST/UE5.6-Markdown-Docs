# Review Test Results

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/review-test-results-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/review-test-results-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:23

---

There are three different test report formats you can review:

-   Log File
-   JSON
-   HTML

## Log File

By default, the Automation Test Framework will log events and the status of tests.

The patterns are:

-   `Test Started. Name={<short name>} Path={<full name>}`
-   `Test Completed. Result={<status>}. Name={<short name>} Path={<full name>}`
-   `BeginEvents: <test full name> (... events caught during the test) EndEvents: <test full name>`
-   `**** TEST COMPLETE. EXIT CODE: <exit code number> ****`

An exit code of 0 means no test failure.

## JSON

The command line argument `-ReportExportPath="<output path>"` stores the report in a `.json` file at the target path.

The file includes the test run's details, including:

-   all events raised,
-   durations of each test,
-   device details.

### Example

```
`{   "devices": [     {       "deviceName": "00-00-000-00",       "instance": "878B6A854613D3B6A69CDEAFBA1C5DBA",       "platform": "WindowsEditor",       "oSVersion": "Windows Server 2022 (21H2) [10.0.20348.524] ",       "model": "Default",       "gPU": "Microsoft Basic Display Adapter",       "cPUModel": "Intel(R) Xeon(R) Platinum 8259CL CPU @ 2.50GHz",       "rAMInGB": 127,       "renderMode": "D3D11_SM5",       "rHI": "DirectX 11",       "appInstanceLog": ""     }   ],   "reportCreatedOn": "2000.01.01-12.00.00",   "succeeded": 1,   "succeededWithWarnings": 0,   "failed": 0,   "notRun": 0,   "inProcess": 0,   "totalDuration": 0.3,   "comparisonExported": false,   "comparisonExportDirectory": "",   "tests": [     {       "testDisplayName": "Test1",       "fullTestPath": "Project.Functional Tests.SomeGroup.Test1",       "state": "Skipped",       "deviceInstance": [         "878B6A854613D3B6A69CDEAFBA1C5DBA"       ],       "duration": 0,       "dateTime": "2000.01.01-12.00.00",       "entries": [         {           "event": {             "type": "Info",             "message": "Skipping test: Tests for review [config]",             "context": "",             "artifact": "00000000000000000000000000000000"           },           "filename": "",           "lineNumber": -1,           "timestamp": "2000.01.01-12.00.00"         }       ],       "warnings": 0,       "errors": 0,       "artifacts": []     },     {       "testDisplayName": "Test2",       "fullTestPath": "Project.Functional Tests.SomeGroup.Test2",       "state": "Success",       "deviceInstance": [         "878B6A854613D3B6A69CDEAFBA1C5DBA"       ],       "duration": 0.3,       "dateTime": "2000.01.01-12.00.00",       "entries": [],       "warnings": 0,       "errors": 0,       "artifacts": []     }   ] }`
Copy full snippet
```
{ "devices": \[ { "deviceName": "00-00-000-00", "instance": "878B6A854613D3B6A69CDEAFBA1C5DBA", "platform": "WindowsEditor", "oSVersion": "Windows Server 2022 (21H2) \[10.0.20348.524\] ", "model": "Default", "gPU": "Microsoft Basic Display Adapter", "cPUModel": "Intel(R) Xeon(R) Platinum 8259CL CPU @ 2.50GHz", "rAMInGB": 127, "renderMode": "D3D11\_SM5", "rHI": "DirectX 11", "appInstanceLog": "" } \], "reportCreatedOn": "2000.01.01-12.00.00", "succeeded": 1, "succeededWithWarnings": 0, "failed": 0, "notRun": 0, "inProcess": 0, "totalDuration": 0.3, "comparisonExported": false, "comparisonExportDirectory": "", "tests": \[ { "testDisplayName": "Test1", "fullTestPath": "Project.Functional Tests.SomeGroup.Test1", "state": "Skipped", "deviceInstance": \[ "878B6A854613D3B6A69CDEAFBA1C5DBA" \], "duration": 0, "dateTime": "2000.01.01-12.00.00", "entries": \[ { "event": { "type": "Info", "message": "Skipping test: Tests for review \[config\]", "context": "", "artifact": "00000000000000000000000000000000" }, "filename": "", "lineNumber": -1, "timestamp": "2000.01.01-12.00.00" } \], "warnings": 0, "errors": 0, "artifacts": \[\] }, { "testDisplayName": "Test2", "fullTestPath": "Project.Functional Tests.SomeGroup.Test2", "state": "Success", "deviceInstance": \[ "878B6A854613D3B6A69CDEAFBA1C5DBA" \], "duration": 0.3, "dateTime": "2000.01.01-12.00.00", "entries": \[\], "warnings": 0, "errors": 0, "artifacts": \[\] } \] }

## HTML

See [Setting Up an Automation Test Report Server](/documentation/en-us/unreal-engine/setting-up-an-automation-test-report-server) for more information on HTML reports.