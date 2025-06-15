# Tasks System Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/tasks-system-references-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/tasks-system-references-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:34

---

Tasks System resides in the `UE::Tasks` namespace. To use Tasks System you will need to include the `Tasks/Task.h` library. You can refer to the `Tests/Tasks/TasksTest.cpp` class for usage examples. The reference table below provides a few examples to the key functions of the Tasks System.

| Reference | Description |
| --- | --- |
| `TTask<ResultType>()` | 
A handle of an actual task. It uses reference counting to manage the task's lifetime.

-   The task is created when it's launched.
    
-   Releasing the last user-held reference doesn't necessarily release the task as the system can still hold an internal reference used to execute the task.
    
-   FTask is an alias for tasks that do not return results (TTask);
    



 |
| `TTask<ResultType>::IsValid()` | 

The function:

```
	`bool TTask<ResultType>::IsValid() const;`

Copy full snippet
```
bool TTask<ResultType>::IsValid() const;

Returns true if the task handle references a task. A default-constructed task handle is "empty" and so is "not valid". A task is constructed when it's launched. For example:

```
	`FTask Task;  	check(!Task.IsValid());  	Task = Launch(UE_SOURCE_LOCATION, [] {});  	check(Task.IsValid());  	Task = {}; // reset the task object  	check(!Task.IsValid());`
Copy full snippet
```
FTask Task; check(!Task.IsValid()); Task = Launch(UE\_SOURCE\_LOCATION, \[\] {}); check(Task.IsValid()); Task = {}; // reset the task object check(!Task.IsValid());

 |
| `Task<ResultType>::Launch` | 

Launches a task for asynchronous execution. In the Code example below launch is used on a task and returns its handle:

```
	`template<typename TaskBodyType>  	TTask<TInvokeResult_T<TaskBodyType>> Launch( 	const TCHAR* DebugName, 	TaskBodyType&& TaskBody, 	LowLevelTasks::ETaskPriority Priority = 	LowLevelTasks::ETaskPriority::Normal 	);`

Copy full snippet
```
template<typename TaskBodyType> TTask<TInvokeResult\_T<TaskBodyType>> Launch( const TCHAR\* DebugName, TaskBodyType&& TaskBody, LowLevelTasks::ETaskPriority Priority = LowLevelTasks::ETaskPriority::Normal );

Prerequisites are other tasks that must be completed before the task that depends on them is executed. Once all prerequisites are completed, the task is automatically scheduled for execution.

```
	`template<typename TaskBodyType, typename PrerequisitesCollectionType> 	TTask<TInvokeResult_T<TaskBodyType>> TTask<ResultType>::Launch( 	const TCHAR* DebugName, 	TaskBodyType&& TaskBody, 	PrerequisitesCollectionType&& Prerequisites, 	LowLevelTasks::ETaskPriority Priority = 		LowLevelTasks::ETaskPriority::Normal 	);`

Copy full snippet
```
template<typename TaskBodyType, typename PrerequisitesCollectionType> TTask<TInvokeResult\_T<TaskBodyType>> TTask<ResultType>::Launch( const TCHAR\* DebugName, TaskBodyType&& TaskBody, PrerequisitesCollectionType&& Prerequisites, LowLevelTasks::ETaskPriority Priority = LowLevelTasks::ETaskPriority::Normal );

**Parameters**:

-   DebugName - a (preferably) unique name for task identification in debugger and profiler. UE\_SOURCE\_LOCATION macro can be used, that generates a string \[Filename\]:\[Lineno\] of the source location where it's used.
    
-   TaskBody - a callable object that will be executed asynchronously, e.g. a lambda, a function pointer or a class with operator();
    
-   Prerequisites - an iterable collection of TTask. Their result type is not required to match the result type of the task.
    
-   Priority - task priority that affects the order in which tasks are executed.
    

**Example**:

```
	`FTask Prerequisite1 = Launch(UE_SOURCE_LOCATION, []{});  	FTask Prerequisite2 = Launch(UE_SOURCE_LOCATION, []{}, ETaskPriority::High);  	FTask DependentTask = Launch(UE_SOURCE_LOCATION, []{}, Prerequisites(Prerequisite1, Prerequisite2));  	TTask<bool> BoolTask = Launch(UE_SOURCE_LOCATION, []{ return true; });`
Copy full snippet
```
FTask Prerequisite1 = Launch(UE\_SOURCE\_LOCATION, \[\]{}); FTask Prerequisite2 = Launch(UE\_SOURCE\_LOCATION, \[\]{}, ETaskPriority::High); FTask DependentTask = Launch(UE\_SOURCE\_LOCATION, \[\]{}, Prerequisites(Prerequisite1, Prerequisite2)); TTask<bool> BoolTask = Launch(UE\_SOURCE\_LOCATION, \[\]{ return true; });

`template<typename... TaskTypes> TPrerequisites<TaskTypes...> Prerequisites(TaskTypes&... Tasks);` is a helper function to pass a variable number of prerequisites to `Launch()` and `FTaskEvent::AddPrerequisites()`. For additional examples, you can observe the tasks: `IsCompleted()`, `Wait()`,`GetResult()`.



 |
| `TTask<ResultType>::IsCompleted` | 

Returns true if the task is completed or is not valid.

```
	`bool TTask<ResultType>::IsCompleted() const;`

Copy full snippet
```
bool TTask<ResultType>::IsCompleted() const;

A task is completed **if** its execution is finished and all its nested tasks are completed.

**Example:**

```
	`FTask Task;  	check(Task.IsCompleted());  	Task = Launch(UE_SOURCE_LOCATION, []{});  	Task.Wait();  	check(Task.IsCompleted());`

Copy full snippet
```
FTask Task; check(Task.IsCompleted()); Task = Launch(UE\_SOURCE\_LOCATION, \[\]{}); Task.Wait(); check(Task.IsCompleted());

For additional examples, you can observe the tasks: `Launch()`, `Wait()` and `GetResult()`.



 |
| `TTask<ResultType>::Wait` | 

Blocks the current thread until the task(s) is completed or waiting timed out. Returns false on timeout. Waiting can take longer than the specified timeout value. The task(s) is completed if `Wait()` returns true. Returns true immediately if the task is not valid:

```
	`bool TTask<ResultType>::Wait(FTimespan Timeout); 	template<typename TaskCollectionType>  	bool Wait(const TaskCollectionType& Tasks, FTimespan InTimeout);`

Copy full snippet
```
bool TTask<ResultType>::Wait(FTimespan Timeout); template<typename TaskCollectionType> bool Wait(const TaskCollectionType& Tasks, FTimespan InTimeout);

**Example**:

```
	`FTask Task; 	Task.Wait(); // returns immediately 	Task = Launch(UE_SOURCE_LOCATION, []{}); 	Task.Wait(FTimespan::FromMillisecond(3)); // blocks until the task is completed or waiting timed out  	FTask AnotherTask = Launch(UE_SOURCE_LOCATION, []{}); 	TArray<FTask> Tasks{ Task, AnotherTask }; 	Wait(Tasks); // blocks until all tasks are completed`

Copy full snippet
```
FTask Task; Task.Wait(); // returns immediately Task = Launch(UE\_SOURCE\_LOCATION, \[\]{}); Task.Wait(FTimespan::FromMillisecond(3)); // blocks until the task is completed or waiting timed out FTask AnotherTask = Launch(UE\_SOURCE\_LOCATION, \[\]{}); TArray<FTask> Tasks{ Task, AnotherTask }; Wait(Tasks); // blocks until all tasks are completed

If the task execution is not started yet (it's blocked by a prerequisite, or wasn't picked up by a worker thread yet), waiting for it will "retract" the task and execute it locally (inline). As the task execution hasn't started yet, the waiting thread would need to be blocked while a worker thread executes the task. Executing the task by the waiting thread is not slow process but can be faster, and doesn't occupy a worker thread. Task retraction follows task dependencies, so-called "deep task retraction". If task execution is blocked by prerequisites, task retraction will try to unblock the task by retracting and executing its prerequisites, recursively. If task retraction fails for any reason(the task execution already started) it falls back to blocking waiting.

**Example**:

```
	`FTask Task1 = Launch(UE_SOURCE_LOCATION, []{}); 	FTask Task2 = Launch(UE_SOURCE_LOCATION, []{}); 	FTask Task3 = Launch(UE_SOURCE_LOCATION, []{}, Task2); 	Task3.Wait();`

Copy full snippet
```
FTask Task1 = Launch(UE\_SOURCE\_LOCATION, \[\]{}); FTask Task2 = Launch(UE\_SOURCE\_LOCATION, \[\]{}); FTask Task3 = Launch(UE\_SOURCE\_LOCATION, \[\]{}, Task2); Task3.Wait();

The sample above launches three tasks, where `Task2` is a prerequisite of `Task3`. Waiting for `Task3` completion may retract `Task3` and/or its prerequisite `Task2` and execute them online, however this will not apply to `Task1`.



 |
| `TTask<ResultType>::BusyWait` (**Deprecated**) | 

**Busy-waiting is deprecated in UE 5.5.** Refer to the BusyWait section in the [Tasks System](/documentation/en-us/unreal-engine/tasks-systems-in-unreal-engine) page for more details and suggestions for alternatives.

Busy waiting for a task is the execution of other unrelated tasks while waiting for the task's completion. This can improve the system throughput but should be used cautiously. Busy waiting can take longer than blocking waiting and could affect latency-sensitive task-chains. In the function below, the task executes other ready for execution tasks until the task that is waited for is completed. Next, the task is completed after BusyWait Returns.

```
	`void TTask<ResultType>::BusyWait();`

Copy full snippet
```
void TTask<ResultType>::BusyWait();

In the code sample below, we execute other ready for execution tasks until the task(s) that is waited for is completed, or waiting timed out. Next, we Return false on timeout. Waiting can take longer than the specified timeout value. The task(s) is completed if BusyWait returns true.

```
	`bool TTask<ResultType>::BusyWait(FTimespan Timeout);  	template<typename TaskCollectionType> 	bool BusyWait(const TaskCollectionType& Tasks, 	FTimespan InTimeout = FTimespan::MaxValue())`

Copy full snippet
```
bool TTask<ResultType>::BusyWait(FTimespan Timeout); template<typename TaskCollectionType> bool BusyWait(const TaskCollectionType& Tasks, FTimespan InTimeout = FTimespan::MaxValue())

Before executing unrelated tasks, busy waiting first tries to retract the task that is waited for.

```
	`FTask Task; 	Task.BusyWait(); // returns immediately  	Task = Launch(UE_SOURCE_LOCATION, []{}); 	Task.BusyWait(); // blocks until the task is completed, can execute other tasks while blocked  	FTask AnotherTask = Launch(UE_SOURCE_LOCATION, []{}); 	TArray<FTask> Tasks{ Task, AnotherTask }; 	BusyWait(Tasks, FTimespan::FromMilliseconds(1)); 	// preceding line blocks until all tasks are completed or waiting timed out, can execute other tasks while blocked`

Copy full snippet
```
FTask Task; Task.BusyWait(); // returns immediately Task = Launch(UE\_SOURCE\_LOCATION, \[\]{}); Task.BusyWait(); // blocks until the task is completed, can execute other tasks while blocked FTask AnotherTask = Launch(UE\_SOURCE\_LOCATION, \[\]{}); TArray<FTask> Tasks{ Task, AnotherTask }; BusyWait(Tasks, FTimespan::FromMilliseconds(1)); // preceding line blocks until all tasks are completed or waiting timed out, can execute other tasks while blocked

 |
| `TTask<ResultType>::GetResult` | 

Returns a reference to an object returned by the task as a result of its execution (the value returned by task body execution).

```
	`ResultType& TTask<ResultType>::GetResult();`
Copy full snippet
```
ResultType& TTask<ResultType>::GetResult(); This exists only for tasks with non-void ResultType.

If the task is completed, the call returns immediately. Otherwise, it blocks until the task is completed. The result object gets destroyed when the task object is destroyed, which is when the last reference to the task object is released. The call asserts if the task is not valid.

**Example**:

```
	`TTask<bool> BoolTask = Launch(UE_SOURCE_LOCATION, []{ return true; }); 	bool bResult = BoolTask.GetResult();  	TTask<int32> IntTask; 	// IntTask.GetResult(); - asserts, the task is invalid as it wasn't launched`

Copy full snippet
```
TTask<bool> BoolTask = Launch(UE\_SOURCE\_LOCATION, \[\]{ return true; }); bool bResult = BoolTask.GetResult(); TTask<int32> IntTask; // IntTask.GetResult(); - asserts, the task is invalid as it wasn't launched

 |
| `AddNested()` | 

Registers the given task as "nested" to the "current" task (parent task). The **current task** is a task that is being executed by the current thread.

The **Parent task** is not completed until all nested tasks are completed.

Asserts if is called not from inside another task.

```
	`template<typename TaskType> 	void AddNested(const TaskType& Nested);`
Copy full snippet
```
template<typename TaskType> void AddNested(const TaskType& Nested);

**Example**:

```
	`FTask ParentTask = Launch(TEXT("Parent Task"), 		[] 		{ 			FTask NestedTask = Launch(TEXT("Nested Task"), []{}); 			AddNested(NestedTask); 	} 	);`

Copy full snippet
```
FTask ParentTask = Launch(TEXT("Parent Task"), \[\] { FTask NestedTask = Launch(TEXT("Nested Task"), \[\]{}); AddNested(NestedTask); } );

 |

## FTaskEvent

FTaskEvent shares a part of its API with `TTask<ResultType>`. For example, `IsValid()`, `IsCompleted()`, waiting and busy-waiting API is the same. This section describes only FTaskEvent specific API.

| Reference Task Event | Description |
| --- | --- |
| `FTaskEvent Constructor` | 
Creates a task event object with the given debug name. In contrast with TTask, task events are "valid" after construction `IsValid() == true`, and incomplete `IsCompleted() == false`. Debug name is used to identify a task event object for debugging purposes.

```
	`explicit FTaskEvent::FTaskEvent(const TCHAR* DebugName);`

Copy full snippet
```
explicit FTaskEvent::FTaskEvent(const TCHAR\* DebugName);

A task event must be triggered before it's destroyed.

**Example**:

```
	`FTaskEvent TaskEvent{ UE_SOURCE_LOCATION }; 	check(TaskEvent.IsValid()); 	check(!TaskEvent.IsCompleted()); 	TaskEvent.Trigger(); 	check(TaskEvent.IsCompleted());`
Copy full snippet
```
FTaskEvent TaskEvent{ UE\_SOURCE\_LOCATION }; check(TaskEvent.IsValid()); check(!TaskEvent.IsCompleted()); TaskEvent.Trigger(); check(TaskEvent.IsCompleted());

 |
| `FTaskEvent::AddPrerequisites` | 

Adds other tasks (or task events) as prerequisites. Can be called only before triggering the task event. Only when all prerequisites are completed and the task event is triggered does it become "completed" ("signaling").

```
	`template<typename PrerequisitesType> 	void FTaskEvent::AddPrerequisites(const PrerequisitesType& Prerequisites);`

Copy full snippet
```
template<typename PrerequisitesType> void FTaskEvent::AddPrerequisites(const PrerequisitesType& Prerequisites);

**Example**:

```
	`FTaskEvent TaskEvent{ TEXT("TaskEvent") };  	TArray<FTask> Prereqs 	{ 		Launch(TEXT("Task A"), [] {}), 		Launch(TEXT("Task B"), [] {}) 	}; 	TaskEvent.AddPrerequisites(Prereqs);  	FTask TaskC = Launch(TEXT("Task C"), [] {}); 	FTask TaskD = Launch(TEXT("Task D"), [] {}); 	TaskEvent.AddPrerequisites(Prerequisites(TaskC, TaskD));  	TaskEvent.Trigger();`

Copy full snippet
```
FTaskEvent TaskEvent{ TEXT("TaskEvent") }; TArray<FTask> Prereqs { Launch(TEXT("Task A"), \[\] {}), Launch(TEXT("Task B"), \[\] {}) }; TaskEvent.AddPrerequisites(Prereqs); FTask TaskC = Launch(TEXT("Task C"), \[\] {}); FTask TaskD = Launch(TEXT("Task D"), \[\] {}); TaskEvent.AddPrerequisites(Prerequisites(TaskC, TaskD)); TaskEvent.Trigger();

 |
| `FTaskEvent::Trigger` | 

A task event is incomplete ("non-signaling") until it's triggered. Triggering a task event doesn't necessarily make it signaling, only when all its prerequisites are completed and the task event is triggered does it become completed.

Every task event must be triggered. Otherwise, its destructor will assert that the task event is not completed.

```
	`void FTaskEvent::Trigger();`
Copy full snippet
```
void FTaskEvent::Trigger();

 |

## FPipe

Pipes are lightweight non-copyable and non-movable objects. The construction of a pipe doesn't allocate dynamic memory and doesn't perform costly processing.

| Reference Name | Description |
| --- | --- |
| `FPipe constructor` | 
Constructs a pipe object with the given debug name. Debug name is used for debugging purposes, to identify a pipe object.

```
	`FPipe::FPipe(const TCHAR* DebugName);`

Copy full snippet
```
FPipe::FPipe(const TCHAR\* DebugName);

Pipes are lightweight non-copyable and non-movable objects. The construction of a pipe doesn't allocate dynamic memory and doesn't do any costly processing



 |
| `FPipe destructor` | Checks if the pipe has any non completed tasks. A pipe must not have any non completed tasks upon destruction. |
| `HasWork()` | 

Checks if the pipe has any non completed tasks. A pipe must not have any non-completed tasks upon destruction.

```
	`bool FPipe::HasWork() const;`

Copy full snippet
```
bool FPipe::HasWork() const;

 |
| `WaitUntilEmpty()` | 

This call will block until all pipe's tasks are completed.

```
	`void FPipe::WaitUntilEmpty();`

Copy full snippet
```
void FPipe::WaitUntilEmpty();

Refer to the function `HasWork()` for an additional example.



 |
| `Launch()` | 

Launches a task in the pipe. Tasks launched in the same pipe are executed not concurrently (one after another), but can be executed by different worker threads.

```
	`template<typename TaskBodyType> 	TTask<TInvokeResult_T<TaskBodyType>> FPipe::Launch( 	const TCHAR* InDebugName, 	TaskBodyType&& TaskBody, 	LowLevelTasks::ETaskPriority Priority = LowLevelTasks::ETaskPriority::Default 	);  	template<typename TaskBodyType, typename PrerequisitesCollectionType> 	TTask<TInvokeResult_T<TaskBodyType>> FPipe::Launch( 	const TCHAR* InDebugName, 	TaskBodyType&& TaskBody, 	PrerequisitesCollectionType&& Prerequisites, 	LowLevelTasks::ETaskPriority Priority = LowLevelTasks::ETaskPriority::Default 	);`
Copy full snippet
```
template<typename TaskBodyType> TTask<TInvokeResult\_T<TaskBodyType>> FPipe::Launch( const TCHAR\* InDebugName, TaskBodyType&& TaskBody, LowLevelTasks::ETaskPriority Priority = LowLevelTasks::ETaskPriority::Default ); template<typename TaskBodyType, typename PrerequisitesCollectionType> TTask<TInvokeResult\_T<TaskBodyType>> FPipe::Launch( const TCHAR\* InDebugName, TaskBodyType&& TaskBody, PrerequisitesCollectionType&& Prerequisites, LowLevelTasks::ETaskPriority Priority = LowLevelTasks::ETaskPriority::Default );

 |
| `IsInContext()` | 

Returns true if called from inside a task that belongs to this pipe. Can be used to check if it's safe to access a shared resource protected by a pipe, such as when the code doesn't have scope of being executed by a piped task.

```
	`bool FPipe::IsInContext() const;`
Copy full snippet
```
bool FPipe::IsInContext() const;

 |