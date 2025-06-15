# TArray: Arrays in Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/array-containers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/array-containers-in-unreal-engine)  
**Processed:** 2025-06-14 16:08:01

---

The simplest container class in Unreal Engine is `TArray`. `TArray` is responsible for the ownership and organization of a sequence of other objects (called "elements") of the same type. As a `TArray` is a sequence, its elements have a well-defined order and its functions are used to deterministically manipulate those objects and their order.

## TArray

`TArray` is the most common container class within Unreal Engine. It is fast, memory efficient, and safe. `TArray` types are defined by two properties: Element type, and an optional allocator.

The element type is the type of the objects that will be stored in the array. `TArray` is what is called a homogenous container, meaning that all of its elements are strictly the same type; you cannot store elements of different types in a single `TArray`.

The allocator is quite frequently omitted and will default to one which is appropriate for most use cases. It defines how the objects are laid out in memory and how the array should grow to accommodate more elements. There are a number of different allocators you can use if you decide that the default behavior is not for you, or you can write your own. More on this later.

`TArray` is a value type, meaning that it should be treated similarly as any other built-in type, like `int32` or `float`. It is not designed to be extended, and creating or destroying `TArray` instances with `new` and `delete` is not a recommended practice. The elements are also value types, and the array owns them. Destruction of a `TArray` will result in the destruction of any elements it still contains. Creating a TArray variable from another will copy its elements into the new variable; there is no shared state.

## Creating and Filling an Array

To create an array, define it like this:

```
	`TArray<int32> IntArray;`
Copy full snippet
```
TArray<int32> IntArray;

This creates an empty array designed to hold a sequence of integers. The element type can be any value type that is copyable and destructible according to normal C++ value rules, like `int32`, `FString`, `TSharedPtr`, and so on. No allocator has been specified, so the `TArray` will use the default, heap-based allocator. At this point, no memory has been allocated.

`TArrays` can be populated in several ways. One way is with the `Init` function, which will fill an array with a number of copies of an element:

```
	`IntArray.Init(10, 5); 	// IntArray == [10,10,10,10,10]`
Copy full snippet
```
IntArray.Init(10, 5); // IntArray == \[10,10,10,10,10\]

`Add` and `Emplace` functions can create new elements at the end of the array:

```
	`TArray<FString> StrArr; 	StrArr.Add    (TEXT("Hello")); 	StrArr.Emplace(TEXT("World")); 	// StrArr == ["Hello","World"]`
Copy full snippet
```
TArray<FString> StrArr; StrArr.Add (TEXT("Hello")); StrArr.Emplace(TEXT("World")); // StrArr == \["Hello","World"\]

The array's allocator provides memory as needed when new elements are added to the array. The default allocator adds enough memory for multiple new elements whenever the current array size is exceeded. `Add` and `Emplace` do much the same thing but with a subtle difference:

-   `Add` (or `Push`) will copy (or move) an instance of the element type into the array.
-   `Emplace` will use the arguments you give it to construct a new instance of the element type.

In the case of our `TArray<FString>`, `Add` will create a temporary `FString` from the string literal and then move the contents of that temporary `FString` into a new `FString` inside the container, whereas `Emplace` will just create the new `FString` directly using the string literal. The end result is the same, but `Emplace` avoids creating a temporary variable, which is often undesirable for non-trivial value types like `FString`.

In general, `Emplace` is preferable to `Add`, in that it avoids creating unnecessary temporary variables at the call site which are then copied or moved into the container. As a rule of thumb, use `Add` for trivial types and `Emplace` otherwise. `Emplace` will never be less efficient than `Add`, but `Add` may read better.

`Append` adds multiple elements at once from either another `TArray`, or a pointer to a regular C array and the size of that array:

```
	`FString Arr[] = { TEXT("of"), TEXT("Tomorrow") }; 	StrArr.Append(Arr, ARRAY_COUNT(Arr)); 	// StrArr == ["Hello","World","of","Tomorrow"]`
Copy full snippet
```
FString Arr\[\] = { TEXT("of"), TEXT("Tomorrow") }; StrArr.Append(Arr, ARRAY\_COUNT(Arr)); // StrArr == \["Hello","World","of","Tomorrow"\]

`AddUnique` only adds a new element to the container if an equivalent element doesn't already exist. Equivalence is checked by using the element type's `operator==`:

```
	`StrArr.AddUnique(TEXT("!")); 	// StrArr == ["Hello","World","of","Tomorrow","!"]  	StrArr.AddUnique(TEXT("!")); 	// StrArr is unchanged as "!" is already an element`
Copy full snippet
```
StrArr.AddUnique(TEXT("!")); // StrArr == \["Hello","World","of","Tomorrow","!"\] StrArr.AddUnique(TEXT("!")); // StrArr is unchanged as "!" is already an element

`Insert`, like `Add`, `Emplace` and `Append`, adds a single element or a copy of an array of elements at a given index:

```
	`StrArr.Insert(TEXT("Brave"), 1); 	// StrArr == ["Hello","Brave","World","of","Tomorrow","!"]`
Copy full snippet
```
StrArr.Insert(TEXT("Brave"), 1); // StrArr == \["Hello","Brave","World","of","Tomorrow","!"\]

The `SetNum` function can directly set the number of array elements, with new elements being created using the element type's default constructor if the new number is greater than the current one:

```
	`StrArr.SetNum(8); 	// StrArr == ["Hello","Brave","World","of","Tomorrow","!","",""]`
Copy full snippet
```
StrArr.SetNum(8); // StrArr == \["Hello","Brave","World","of","Tomorrow","!","",""\]

`SetNum` will also remove elements if the new number is less than the current one. More detailed information on element removal will come later:

```
	`StrArr.SetNum(6); 	// StrArr == ["Hello","Brave","World","of","Tomorrow","!"]`
Copy full snippet
```
StrArr.SetNum(6); // StrArr == \["Hello","Brave","World","of","Tomorrow","!"\]

## Iteration

There are several ways to iterate over the elements of your array, but the recommended way is to use the C++ ranged-for feature:

```
	`FString JoinedStr; 	for (auto& Str : StrArr) 	{ 		JoinedStr += Str; 		JoinedStr += TEXT(" "); 	} 	// JoinedStr == "Hello Brave World of Tomorrow ! "`
Copy full snippet
```
FString JoinedStr; for (auto& Str : StrArr) { JoinedStr += Str; JoinedStr += TEXT(" "); } // JoinedStr == "Hello Brave World of Tomorrow ! "

Regular index-based iteration is also possible, of course:

```
	`for (int32 Index = 0; Index != StrArr.Num(); ++Index) 	{ 		JoinedStr += StrArr[Index]; 		JoinedStr += TEXT(" "); 	}`
Copy full snippet
```
for (int32 Index = 0; Index != StrArr.Num(); ++Index) { JoinedStr += StrArr\[Index\]; JoinedStr += TEXT(" "); }

Finally, arrays also have their own iterator type for more control over your iteration. There are two functions called `CreateIterator` and `CreateConstIterator` which can be used for read-write or read-only access to the elements respectively:

```
	`for (auto It = StrArr.CreateConstIterator(); It; ++It) 	{ 		JoinedStr += *It; 		JoinedStr += TEXT(" "); 	}`
Copy full snippet
```
for (auto It = StrArr.CreateConstIterator(); It; ++It) { JoinedStr += \*It; JoinedStr += TEXT(" "); }

## Sorting

Arrays can be sorted simply by calling the `Sort` function:

```
	`StrArr.Sort(); 	// StrArr == ["!","Brave","Hello","of","Tomorrow","World"]`
Copy full snippet
```
StrArr.Sort(); // StrArr == \["!","Brave","Hello","of","Tomorrow","World"\]

Here, the values are sorted by means of the element type's `operator<`. In FString's case, this is a case-insensitive lexicographical comparison. A binary predicate can also be implemented to provide different ordering semantics, like this:

```
	`StrArr.Sort([](const FString& A, const FString& B) { 		return A.Len() < B.Len(); 	}); 	// StrArr == ["!","of","Hello","Brave","World","Tomorrow"]`
Copy full snippet
```
StrArr.Sort(\[\](const FString& A, const FString& B) { return A.Len() < B.Len(); }); // StrArr == \["!","of","Hello","Brave","World","Tomorrow"\]

Now the strings are sorted by their lengths. Note how the three strings with the same length - "Hello", "Brave" and "World" - have changed order relative to their positions in the array beforehand. This is because `Sort` is unstable and the relative order of equivalent elements (those strings are equivalent here because the predicate only compares length) is not guaranteed. `Sort` is implemented as a quicksort.

The `HeapSort` function, with or without a binary predicate, can be used to perform a heap sort. Whether or not you choose to use it depends on your particular data and how efficiently it sorts compared to the Sort function. Like `Sort`, `HeapSort` is not stable. If we had used `HeapSort` instead of `Sort` above, this would be the result (the same, in this case):

```
	`StrArr.HeapSort([](const FString& A, const FString& B) { 		return A.Len() < B.Len(); 	}); 	// StrArr == ["!","of","Hello","Brave","World","Tomorrow"]`
Copy full snippet
```
StrArr.HeapSort(\[\](const FString& A, const FString& B) { return A.Len() < B.Len(); }); // StrArr == \["!","of","Hello","Brave","World","Tomorrow"\]

Finally, `StableSort` can be used to guarantee the relative order of equivalent elements after sorting. If we had called `StableSort` instead of `Sort` or `HeapSort` above, the result would have been as follows:

```
	`StrArr.StableSort([](const FString& A, const FString& B) { 		return A.Len() < B.Len(); 	}); 	// StrArr == ["!","of","Brave","Hello","World","Tomorrow"]`
Copy full snippet
```
StrArr.StableSort(\[\](const FString& A, const FString& B) { return A.Len() < B.Len(); }); // StrArr == \["!","of","Brave","Hello","World","Tomorrow"\]

That is, "Brave", "Hello" and "World" remain in their same relative order after previously having been lexicographically sorted. `StableSort` is implemented as a merge sort.

## Queries

We can ask the array how many elements it holds by using the `Num` function:

```
	`int32 Count = StrArr.Num(); 	// Count == 6`
Copy full snippet
```
int32 Count = StrArr.Num(); // Count == 6

If you need direct access to the array memory, perhaps for interoperability with a C-style API, you can use the `GetData` function to return a pointer to the elements in the array. This pointer is only valid as long as the array exists and before any mutating operations are made to the array. Only the first `Num` indices from the `StrPtr` are dereferenceable:

```
	`FString* StrPtr = StrArr.GetData(); 	// StrPtr[0] == "!" 	// StrPtr[1] == "of" 	// ... 	// StrPtr[5] == "Tomorrow" 	// StrPtr[6] - undefined behavior`
Copy full snippet
```
FString\* StrPtr = StrArr.GetData(); // StrPtr\[0\] == "!" // StrPtr\[1\] == "of" // ... // StrPtr\[5\] == "Tomorrow" // StrPtr\[6\] - undefined behavior

If the container is const, then the returned pointer will also be const.

You can also ask the container how big the elements are:

```
	`uint32 ElementSize = StrArr.GetTypeSize(); 	// ElementSize == sizeof(FString)`
Copy full snippet
```
uint32 ElementSize = StrArr.GetTypeSize(); // ElementSize == sizeof(FString)

To retrieve elements, you can use the indexing `operator[]` and pass it a zero-based index to the element you want:

```
	`FString Elem1 = StrArr[1]; 	// Elem1 == "of"`
Copy full snippet
```
FString Elem1 = StrArr\[1\]; // Elem1 == "of"

Passing an invalid index — less than 0 or greater than or equal to Num() — will cause a runtime error. You can ask the container if a particular index is valid using the `IsValidIndex` function:

```
	`bool bValidM1 = StrArr.IsValidIndex(-1); 	bool bValid0  = StrArr.IsValidIndex(0); 	bool bValid5  = StrArr.IsValidIndex(5); 	bool bValid6  = StrArr.IsValidIndex(6); 	// bValidM1 == false 	// bValid0  == true 	// bValid5  == true 	// bValid6  == false`
Copy full snippet
```
bool bValidM1 = StrArr.IsValidIndex(-1); bool bValid0 = StrArr.IsValidIndex(0); bool bValid5 = StrArr.IsValidIndex(5); bool bValid6 = StrArr.IsValidIndex(6); // bValidM1 == false // bValid0 == true // bValid5 == true // bValid6 == false

`operator[]` returns a reference, so it can also be used to mutate the elements inside the array, assuming your array isn't const:

```
	`StrArr[3] = StrArr[3].ToUpper(); 	// StrArr == ["!","of","Brave","HELLO","World","Tomorrow"]`
Copy full snippet
```
StrArr\[3\] = StrArr\[3\].ToUpper(); // StrArr == \["!","of","Brave","HELLO","World","Tomorrow"\]

Like the GetData function, `operator[]` will return a const reference if the array is const. You can also index from the end of the array backward by using the `Last` function. The index defaults to zero. The `Top` function is a synonym for `Last`, except it doesn't take an index:

```
	`FString ElemEnd  = StrArr.Last(); 	FString ElemEnd0 = StrArr.Last(0); 	FString ElemEnd1 = StrArr.Last(1); 	FString ElemTop  = StrArr.Top(); 	// ElemEnd  == "Tomorrow" 	// ElemEnd0 == "Tomorrow" 	// ElemEnd1 == "World" 	// ElemTop  == "Tomorrow"`
Copy full snippet
```
FString ElemEnd = StrArr.Last(); FString ElemEnd0 = StrArr.Last(0); FString ElemEnd1 = StrArr.Last(1); FString ElemTop = StrArr.Top(); // ElemEnd == "Tomorrow" // ElemEnd0 == "Tomorrow" // ElemEnd1 == "World" // ElemTop == "Tomorrow"

We can ask the array if it contains a certain element:

```
	`bool bHello   = StrArr.Contains(TEXT("Hello")); 	bool bGoodbye = StrArr.Contains(TEXT("Goodbye")); 	// bHello   == true 	// bGoodbye == false`
Copy full snippet
```
bool bHello = StrArr.Contains(TEXT("Hello")); bool bGoodbye = StrArr.Contains(TEXT("Goodbye")); // bHello == true // bGoodbye == false

Or ask the array if it contains an element which matches a specific predicate:

```
	`bool bLen5 = StrArr.ContainsByPredicate([](const FString& Str){ 		return Str.Len() == 5; 	}); 	bool bLen6 = StrArr.ContainsByPredicate([](const FString& Str){ 		return Str.Len() == 6; 	}); 	// bLen5 == true 	// bLen6 == false`
Copy full snippet
```
bool bLen5 = StrArr.ContainsByPredicate(\[\](const FString& Str){ return Str.Len() == 5; }); bool bLen6 = StrArr.ContainsByPredicate(\[\](const FString& Str){ return Str.Len() == 6; }); // bLen5 == true // bLen6 == false

We can find elements by using the `Find` family of functions. To check if an element exists and return its index, we use Find:

```
	`int32 Index; 	if (StrArr.Find(TEXT("Hello"), Index)) 	{ 		// Index == 3 	}`
Copy full snippet
```
int32 Index; if (StrArr.Find(TEXT("Hello"), Index)) { // Index == 3 }

This sets `Index` to be the index of the first element found. If there are duplicate elements and we instead want to find the index of last element, we use the `FindLast` function instead:

```
	`int32 IndexLast; 	if (StrArr.FindLast(TEXT("Hello"), IndexLast)) 	{ 		// IndexLast == 3, because there aren't any duplicates 	}`
Copy full snippet
```
int32 IndexLast; if (StrArr.FindLast(TEXT("Hello"), IndexLast)) { // IndexLast == 3, because there aren't any duplicates }

Both of these functions return a bool to indicate whether or not an element was found, while also writing the index of that element into a variable when it was found.

`Find` and `FindLast` can also return an element index directly. They will do this if you do not pass the index as an explicit argument. This can be more succinct than the above function, and which function you use depends on what suits your particular need or style.

If no element was found, the special `INDEX_NONE` value is returned:

```
	`int32 Index2     = StrArr.Find(TEXT("Hello")); 	int32 IndexLast2 = StrArr.FindLast(TEXT("Hello")); 	int32 IndexNone  = StrArr.Find(TEXT("None")); 	// Index2     == 3 	// IndexLast2 == 3 	// IndexNone  == INDEX_NONE`
Copy full snippet
```
int32 Index2 = StrArr.Find(TEXT("Hello")); int32 IndexLast2 = StrArr.FindLast(TEXT("Hello")); int32 IndexNone = StrArr.Find(TEXT("None")); // Index2 == 3 // IndexLast2 == 3 // IndexNone == INDEX\_NONE

`IndexOfByKey` works similarly, but allows comparison of the elements with an arbitrary object. With the `Find` functions, the argument is actually converted to the element type (`FString` in this case) before the search begins. With `IndexOfByKey`, the key is compared directly, supporting searches even when the key type isn't directly convertible to the element type.

`IndexOfByKey` works for any key type for which `operator==(ElementType, KeyType)` exists. `IndexOfByKey` will return the index of the first found element, or `INDEX_NONE` if no element was found:

```
	`int32 Index = StrArr.IndexOfByKey(TEXT("Hello")); 	// Index == 3`
Copy full snippet
```
int32 Index = StrArr.IndexOfByKey(TEXT("Hello")); // Index == 3

The `IndexOfByPredicate` function finds the index of the first element that matches the specified predicate, again returning the special `INDEX_NONE` value if none was found:

```
	`int32 Index = StrArr.IndexOfByPredicate([](const FString& Str){ 		return Str.Contains(TEXT("r")); 	}); 	// Index == 2`
Copy full snippet
```
int32 Index = StrArr.IndexOfByPredicate(\[\](const FString& Str){ return Str.Contains(TEXT("r")); }); // Index == 2

Instead of returning indices, we can return pointers back to the elements we find. `FindByKey` works like `IndexOfByKey`, comparing the elements to an arbitrary object, but returning a pointer to the element it finds. If it does not find an element, it will return `nullptr`:

```
	`auto* OfPtr  = StrArr.FindByKey(TEXT("of"))); 	auto* ThePtr = StrArr.FindByKey(TEXT("the"))); 	// OfPtr  == &StrArr[1] 	// ThePtr == nullptr`
Copy full snippet
```
auto\* OfPtr = StrArr.FindByKey(TEXT("of"))); auto\* ThePtr = StrArr.FindByKey(TEXT("the"))); // OfPtr == &StrArr\[1\] // ThePtr == nullptr

`FindByPredicate` can be used like `IndexOfByPredicate`, except that it returns pointer instead of an index:

```
	`auto* Len5Ptr = StrArr.FindByPredicate([](const FString& Str){ 		return Str.Len() == 5; 	}); 	auto* Len6Ptr = StrArr.FindByPredicate([](const FString& Str){ 		return Str.Len() == 6; 	}); 	// Len5Ptr == &StrArr[2] 	// Len6Ptr == nullptr`
Copy full snippet
```
auto\* Len5Ptr = StrArr.FindByPredicate(\[\](const FString& Str){ return Str.Len() == 5; }); auto\* Len6Ptr = StrArr.FindByPredicate(\[\](const FString& Str){ return Str.Len() == 6; }); // Len5Ptr == &StrArr\[2\] // Len6Ptr == nullptr

Finally, you can retrieve an array of elements matching a particular predicate with the `FilterByPredicate` function:

```
	`auto Filter = StrArray.FilterByPredicate([](const FString& Str){ 		return !Str.IsEmpty() && Str[0] < TEXT('M'); 	});`
Copy full snippet
```
auto Filter = StrArray.FilterByPredicate(\[\](const FString& Str){ return !Str.IsEmpty() && Str\[0\] < TEXT('M'); });

## Removal

You can erase elements from the array using the `Remove` family of functions. The `Remove` function removes all elements that are considered equal to the element you provide, according to the element type's `operator==` function. For example:

```
	`TArray<int32> ValArr; 	int32 Temp[] = { 10, 20, 30, 5, 10, 15, 20, 25, 30 }; 	ValArr.Append(Temp, ARRAY_COUNT(Temp)); 	// ValArr == [10,20,30,5,10,15,20,25,30]  	ValArr.Remove(20); 	// ValArr == [10,30,5,10,15,25,30]`
Copy full snippet
```
TArray<int32> ValArr; int32 Temp\[\] = { 10, 20, 30, 5, 10, 15, 20, 25, 30 }; ValArr.Append(Temp, ARRAY\_COUNT(Temp)); // ValArr == \[10,20,30,5,10,15,20,25,30\] ValArr.Remove(20); // ValArr == \[10,30,5,10,15,25,30\]

You can also use `RemoveSingle` to erase the first matching element in the array. This is useful if you know your array may contain duplicates and you only want to erase one, or as an optimization if you know that your array can only ever contain one matching element:

```
	`ValArr.RemoveSingle(30); 	// ValArr == [10,5,10,15,25,30]`
Copy full snippet
```
ValArr.RemoveSingle(30); // ValArr == \[10,5,10,15,25,30\]

We can also remove elements by their zero-based index by using the `RemoveAt` function. You may wish to use `IsValidIndex` to verify that the array has an element with the index you plan to provide, as passing an invalid index to this function will cause a runtime error.:

```
	`ValArr.RemoveAt(2); // Removes the element at index 2 	// ValArr == [10,5,15,25,30]  	ValArr.RemoveAt(99); // This will cause a runtime error as 	                       // there is no element at index 99`
Copy full snippet
```
ValArr.RemoveAt(2); // Removes the element at index 2 // ValArr == \[10,5,15,25,30\] ValArr.RemoveAt(99); // This will cause a runtime error as // there is no element at index 99

We can also remove elements which match a predicate by using the `RemoveAll` function. For example, removing all values which are a multiple of 3:

```
	`ValArr.RemoveAll([](int32 Val) { 		return Val % 3 == 0; 	}); 	// ValArr == [10,5,25]`
Copy full snippet
```
ValArr.RemoveAll(\[\](int32 Val) { return Val % 3 == 0; }); // ValArr == \[10,5,25\]

In all of these cases, when elements were removed, the elements that followed were shuffled down into lower indices, as there can never be holes left in the array.

The shuffling process has an overhead. If you don't really care what order the remaining elements are left in, this overhead can be reduced by using the `RemoveSwap`, `RemoveAtSwap` and `RemoveAllSwap` functions, which work like their non-swapping variants except that they don't guarantee the order of the remaining elements, enabling them to complete their tasks more quickly:

```
	`TArray<int32> ValArr2; 	for (int32 i = 0; i != 10; ++i) 		ValArr2.Add(i % 5); 	// ValArr2 == [0,1,2,3,4,0,1,2,3,4]  	ValArr2.RemoveSwap(2); 	// ValArr2 == [0,1,4,3,4,0,1,3]  	ValArr2.RemoveAtSwap(1); 	// ValArr2 == [0,3,4,3,4,0,1]  	ValArr2.RemoveAllSwap([](int32 Val) { 		return Val % 3 == 0; 	}); 	// ValArr2 == [1,4,4]`
Copy full snippet
```
TArray<int32> ValArr2; for (int32 i = 0; i != 10; ++i) ValArr2.Add(i % 5); // ValArr2 == \[0,1,2,3,4,0,1,2,3,4\] ValArr2.RemoveSwap(2); // ValArr2 == \[0,1,4,3,4,0,1,3\] ValArr2.RemoveAtSwap(1); // ValArr2 == \[0,3,4,3,4,0,1\] ValArr2.RemoveAllSwap(\[\](int32 Val) { return Val % 3 == 0; }); // ValArr2 == \[1,4,4\]

Finally, the `Empty` function will remove everything from the array:

```
	`ValArr2.Empty(); 	// ValArr2 == []`
Copy full snippet
```
ValArr2.Empty(); // ValArr2 == \[\]

## Operators

Arrays are regular value types and as such can be copied by the standard copy constructor or assignment operator. As arrays strictly own their elements, copying an array is deep and so the new array will have its own copy of the elements:

```
	`TArray<int32> ValArr3; 	ValArr3.Add(1); 	ValArr3.Add(2); 	ValArr3.Add(3);  	auto ValArr4 = ValArr3; 	// ValArr4 == [1,2,3]; 	ValArr4[0] = 5; 	// ValArr3 == [1,2,3]; 	// ValArr4 == [5,2,3];`
Copy full snippet
```
TArray<int32> ValArr3; ValArr3.Add(1); ValArr3.Add(2); ValArr3.Add(3); auto ValArr4 = ValArr3; // ValArr4 == \[1,2,3\]; ValArr4\[0\] = 5; // ValArr3 == \[1,2,3\]; // ValArr4 == \[5,2,3\];

As an alternative to the `Append` function, you can concatenate arrays with `operator+=`:

```
	`ValArr4 += ValArr3; 	// ValArr4 == [5,2,3,1,2,3]`
Copy full snippet
```
ValArr4 += ValArr3; // ValArr4 == \[5,2,3,1,2,3\]

`TArray` also supports move semantics, which can be invoked using the `MoveTemp` function. After a move, the source array is guaranteed to be left empty:

```
	`ValArr3 = MoveTemp(ValArr4); 	// ValArr3 == [5,2,3,1,2,3] 	// ValArr4 == []`
Copy full snippet
```
ValArr3 = MoveTemp(ValArr4); // ValArr3 == \[5,2,3,1,2,3\] // ValArr4 == \[\]

Arrays can be compared using the `operator==` and `operator!=`. The order of the elements are important — two arrays are only equal if they have the same number of elements in the same order. Elements are compared using their own `operator==`:

```
	`TArray<FString> FlavorArr1; 	FlavorArr1.Emplace(TEXT("Chocolate")); 	FlavorArr1.Emplace(TEXT("Vanilla")); 	// FlavorArr1 == ["Chocolate","Vanilla"]  	auto FlavorArr2 = Str1Array; 	// FlavorArr2 == ["Chocolate","Vanilla"]  	bool bComparison1 = FlavorArr1 == FlavorArr2; 	// bComparison1 == true  	for (auto& Str : FlavorArr2) 	{ 		Str = Str.ToUpper(); 	} 	// FlavorArr2 == ["CHOCOLATE","VANILLA"]  	bool bComparison2 = FlavorArr1 == FlavorArr2; 	// bComparison2 == true, because FString comparison ignores case  	Exchange(FlavorArr2[0], FlavorArr2[1]); 	// FlavorArr2 == ["VANILLA","CHOCOLATE"]  	bool bComparison3 = FlavorArr1 == FlavorArr2; 	// bComparison3 == false, because the order has changed`
Copy full snippet
```
TArray<FString> FlavorArr1; FlavorArr1.Emplace(TEXT("Chocolate")); FlavorArr1.Emplace(TEXT("Vanilla")); // FlavorArr1 == \["Chocolate","Vanilla"\] auto FlavorArr2 = Str1Array; // FlavorArr2 == \["Chocolate","Vanilla"\] bool bComparison1 = FlavorArr1 == FlavorArr2; // bComparison1 == true for (auto& Str : FlavorArr2) { Str = Str.ToUpper(); } // FlavorArr2 == \["CHOCOLATE","VANILLA"\] bool bComparison2 = FlavorArr1 == FlavorArr2; // bComparison2 == true, because FString comparison ignores case Exchange(FlavorArr2\[0\], FlavorArr2\[1\]); // FlavorArr2 == \["VANILLA","CHOCOLATE"\] bool bComparison3 = FlavorArr1 == FlavorArr2; // bComparison3 == false, because the order has changed

## Heap

`TArray` has functions that support a binary heap data structure. A heap is a type of binary tree in which any parent node is equivalent to or ordered before all of its child nodes. When implemented as an array, the root node of the tree is at element 0 and the indices of the left and right child nodes of a node at index N are 2N+1 and 2N+2 respectively. The children are not in any particular order with respect to one another.

Any existing array can be turned into a heap by calling the `Heapify` function. This is overloaded to take a predicate or not, where the non-predicated version will use the element type's `operator<` to determine ordering:

```
	`TArray<int32> HeapArr; 	for (int32 Val = 10; Val != 0; --Val) 	{ 		HeapArr.Add(Val); 	} 	// HeapArr == [10,9,8,7,6,5,4,3,2,1] 	HeapArr.Heapify(); 	// HeapArr == [1,2,4,3,6,5,8,10,7,9]`
Copy full snippet
```
TArray<int32> HeapArr; for (int32 Val = 10; Val != 0; --Val) { HeapArr.Add(Val); } // HeapArr == \[10,9,8,7,6,5,4,3,2,1\] HeapArr.Heapify(); // HeapArr == \[1,2,4,3,6,5,8,10,7,9\]

This is a visualization of the tree:

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32ac6b2a-4219-4a9c-856f-0a3197af1f64/image_0.png)

The nodes in the tree can be read from left-to-right, top-to-bottom as the order of the elements in the heapified array. Note that the array isn't necessarily sorted after being transformed into a heap. While a sorted array would also be a valid heap, the heap structure definition is loose enough to allow multiple valid heaps for the same set of elements.

New elements can be added to the heap via the HeapPush function, reordering other nodes to maintain the heap:

```
	`HeapArr.HeapPush(4); 	// HeapArr == [1,2,4,3,4,5,8,10,7,9,6]`
Copy full snippet
```
HeapArr.HeapPush(4); // HeapArr == \[1,2,4,3,4,5,8,10,7,9,6\] ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a90c43f-8e88-41eb-939e-165aae638b0f/image_1.png)

The `HeapPop` and `HeapPopDiscard` functions are used to remove the top node from the heap. The difference between the two is that the former takes a reference to an element type to return a copy of the top element, and the latter simply removes the top node without returning it in any way. Both functions result in the same change to the array, and the heap is again maintained by reordering other elements appropriately:

```
	`int32 TopNode; 	HeapArr.HeapPop(TopNode); 	// TopNode == 1 	// HeapArr == [2,3,4,6,4,5,8,10,7,9]`
Copy full snippet
```
int32 TopNode; HeapArr.HeapPop(TopNode); // TopNode == 1 // HeapArr == \[2,3,4,6,4,5,8,10,7,9\] ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d833a56-87ac-4822-947b-cad873475d78/image_2.png)

`HeapRemoveAt` will remove an element from the array at a given index, and then reorder elements to maintain the heap:

```
	`HeapArr.HeapRemoveAt(1); 	// HeapArr == [2,4,4,6,9,5,8,10,7]`
Copy full snippet
```
HeapArr.HeapRemoveAt(1); // HeapArr == \[2,4,4,6,9,5,8,10,7\] ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef8489bc-21fa-4428-a5e0-c54ff28723b2/image_3.png)

`HeapPush`, `HeapPop`, `HeapPopDiscard` and `HeapRemoveAt` should only be called when the structure is already a valid heap, such as after a `Heapify` call, any other heap operation, or by manually manipulating the array into a heap.

Each of these functions, including `Heapify`, can take an optional binary predicate to determine the order of the node elements in the heap. By default, heap operations use the element type's `operator<` to determine order. When using a custom predicate, it is important to use the same predicate on all heap operations.

Finally, the top node of the heap can be inspected using `HeapTop`, without changing the array:

```
	`int32 Top = HeapArr.HeapTop(); 	// Top == 2`
Copy full snippet
```
int32 Top = HeapArr.HeapTop(); // Top == 2

## Slack

Because arrays can resize, they use a variable amount of memory. To avoid reallocation every time elements are added, allocators usually provide more memory than was requested so that future `Add` calls don't pay a performance penalty for reallocation. Likewise, removing elements doesn't usually free memory. This leaves the array with slack elements, which are effectively pre-allocated element storage slots that are not currently in use. The amount of slack in an array is defined as the difference between the number of elements stored in the array and the number of elements that the array could store with the amount of memory it has allocated.

As a default-constructed array allocates no memory, the slack will initially be zero. You can find out how much slack there is in an array by using the `GetSlack` function. The maximum number of elements that the array can hold before the container reallocates can be obtained by the `Max` function. `GetSlack` is equivalent to the difference between `Max` and `Num`:

```
	`TArray<int32> SlackArray; 	// SlackArray.GetSlack() == 0 	// SlackArray.Num()      == 0 	// SlackArray.Max()      == 0  	SlackArray.Add(1); 	// SlackArray.GetSlack() == 3 	// SlackArray.Num()      == 1 	// SlackArray.Max()      == 4  	SlackArray.Add(2); 	SlackArray.Add(3); 	SlackArray.Add(4); 	SlackArray.Add(5); 	// SlackArray.GetSlack() == 17 	// SlackArray.Num()      == 5 	// SlackArray.Max()      == 22`
Copy full snippet
```
TArray<int32> SlackArray; // SlackArray.GetSlack() == 0 // SlackArray.Num() == 0 // SlackArray.Max() == 0 SlackArray.Add(1); // SlackArray.GetSlack() == 3 // SlackArray.Num() == 1 // SlackArray.Max() == 4 SlackArray.Add(2); SlackArray.Add(3); SlackArray.Add(4); SlackArray.Add(5); // SlackArray.GetSlack() == 17 // SlackArray.Num() == 5 // SlackArray.Max() == 22

The amount of slack in a container after a reallocation is decided by the allocator, so users should not rely on slack remaining constant.

Although slack management is not required, you can use it to your advantage to give the array optimization hints. For example, if you know you are about to add 100 new elements to the array, you can ensure you have a slack of at least 100 before adding, so that the array will not need to allocate memory while adding the new elements. The `Empty` function, mentioned above, takes an optional slack argument:

```
	`SlackArray.Empty(); 	// SlackArray.GetSlack() == 0 	// SlackArray.Num()      == 0 	// SlackArray.Max()      == 0 	SlackArray.Empty(3); 	// SlackArray.GetSlack() == 3 	// SlackArray.Num()      == 0 	// SlackArray.Max()      == 3 	SlackArray.Add(1); 	SlackArray.Add(2); 	SlackArray.Add(3); 	// SlackArray.GetSlack() == 0 	// SlackArray.Num()      == 3 	// SlackArray.Max()      == 3`
Copy full snippet
```
SlackArray.Empty(); // SlackArray.GetSlack() == 0 // SlackArray.Num() == 0 // SlackArray.Max() == 0 SlackArray.Empty(3); // SlackArray.GetSlack() == 3 // SlackArray.Num() == 0 // SlackArray.Max() == 3 SlackArray.Add(1); SlackArray.Add(2); SlackArray.Add(3); // SlackArray.GetSlack() == 0 // SlackArray.Num() == 3 // SlackArray.Max() == 3

There is a `Reset` function which works similarly to Empty, except that it doesn't free memory if the requested slack is already provided by the current allocation. However, it will allocate more memory if the requested slack is larger:

```
	`SlackArray.Reset(0); 	// SlackArray.GetSlack() == 3 	// SlackArray.Num()      == 0 	// SlackArray.Max()      == 3 	SlackArray.Reset(10); 	// SlackArray.GetSlack() == 10 	// SlackArray.Num()      == 0 	// SlackArray.Max()      == 10`
Copy full snippet
```
SlackArray.Reset(0); // SlackArray.GetSlack() == 3 // SlackArray.Num() == 0 // SlackArray.Max() == 3 SlackArray.Reset(10); // SlackArray.GetSlack() == 10 // SlackArray.Num() == 0 // SlackArray.Max() == 10

And finally, you can remove all slack with the `Shrink` function, which will resize the allocation to be the minimum size required to hold the current elements. `Shrink` does not have any effect on the elements in the array:

```
	`SlackArray.Add(5); 	SlackArray.Add(10); 	SlackArray.Add(15); 	SlackArray.Add(20); 	// SlackArray.GetSlack() == 6 	// SlackArray.Num()      == 4 	// SlackArray.Max()      == 10 	SlackArray.Shrink(); 	// SlackArray.GetSlack() == 0 	// SlackArray.Num()      == 4 	// SlackArray.Max()      == 4`
Copy full snippet
```
SlackArray.Add(5); SlackArray.Add(10); SlackArray.Add(15); SlackArray.Add(20); // SlackArray.GetSlack() == 6 // SlackArray.Num() == 4 // SlackArray.Max() == 10 SlackArray.Shrink(); // SlackArray.GetSlack() == 0 // SlackArray.Num() == 4 // SlackArray.Max() == 4

## Raw Memory

`TArray` is ultimately just a wrapper around allocated memory. It can be useful to treat it as such by direct modification of the bytes of the allocation and by creating elements yourself. `TArray` will always try to do the best it can with the information it has, but sometimes you may need to drop to a lower level.

The following functions give you fast, low-level access to `TArray` and the data it holds, but, if used improperly, give you the ability to put the container into invalid states and cause undefined behavior. It is up to you to return the container to a valid state after invoking these functions but before any other regular function is called.

The `AddUninitialized` and `InsertUninitialized` functions will add some uninitialized space to the array. They work like the `Add` and `Insert` functions, respectively, but they will not call the constructor of the element type. This can be useful to avoid calling constructors. You might do this in cases like the following example, where you plan to overwrite the entire struct with a `Memcpy` call:

```
	`int32 SrcInts[] = { 2, 3, 5, 7 }; 	TArray<int32> UninitInts; 	UninitInts.AddUninitialized(4); 	FMemory::Memcpy(UninitInts.GetData(), SrcInts, 4*sizeof(int32)); 	// UninitInts == [2,3,5,7]`
Copy full snippet
```
int32 SrcInts\[\] = { 2, 3, 5, 7 }; TArray<int32> UninitInts; UninitInts.AddUninitialized(4); FMemory::Memcpy(UninitInts.GetData(), SrcInts, 4\*sizeof(int32)); // UninitInts == \[2,3,5,7\]

You can also use this feature to reserve memory for objects which you plan to construct yourself:

```
	`TArray<FString> UninitStrs; 	UninitStrs.Emplace(TEXT("A")); 	UninitStrs.Emplace(TEXT("D")); 	UninitStrs.InsertUninitialized(1, 2); 	new ((void*)(UninitStrs.GetData() + 1)) FString(TEXT("B")); 	new ((void*)(UninitStrs.GetData() + 2)) FString(TEXT("C")); 	// UninitStrs == ["A","B","C","D"]`
Copy full snippet
```
TArray<FString> UninitStrs; UninitStrs.Emplace(TEXT("A")); UninitStrs.Emplace(TEXT("D")); UninitStrs.InsertUninitialized(1, 2); new ((void\*)(UninitStrs.GetData() + 1)) FString(TEXT("B")); new ((void\*)(UninitStrs.GetData() + 2)) FString(TEXT("C")); // UninitStrs == \["A","B","C","D"\]

`AddZeroed` and `InsertZeroed` work similarly, except they also zero the bytes of the added/inserted space:

```
	`struct S 	{ 		S(int32 InInt, void* InPtr, float InFlt) 			: Int(InInt) 			, Ptr(InPtr) 			, Flt(InFlt) 		{ 		} 		int32 Int; 		void* Ptr; 		float Flt; 	}; 	TArray<S> SArr; 	SArr.AddZeroed(); 	// SArr == [{ Int: 0, Ptr: nullptr, Flt: 0.0f }]`
Copy full snippet
```
struct S { S(int32 InInt, void\* InPtr, float InFlt) : Int(InInt) , Ptr(InPtr) , Flt(InFlt) { } int32 Int; void\* Ptr; float Flt; }; TArray<S> SArr; SArr.AddZeroed(); // SArr == \[{ Int: 0, Ptr: nullptr, Flt: 0.0f }\]

There are also `SetNumUninitialized` and `SetNumZeroed` functions which work like `SetNum` except that, in the case where the new number is greater than the current one, the space for the new elements will be left uninitialized or bitwise-zeroed respectively. As with the `AddUninitialized` and `InsertUninitialized` functions, you should ensure that, if necessary, new elements are properly constructed into the new space if they need to be:

```
	`SArr.SetNumUninitialized(3); 	new ((void*)(SArr.GetData() + 1)) S(5, (void*)0x12345678, 3.14); 	new ((void*)(SArr.GetData() + 2)) S(2, (void*)0x87654321, 2.72); 	// SArr == [ 	//   { Int: 0, Ptr: nullptr,    Flt: 0.0f  }, 	//   { Int: 5, Ptr: 0x12345678, Flt: 3.14f }, 	//   { Int: 2, Ptr: 0x87654321, Flt: 2.72f } 	// ]  	SArr.SetNumZeroed(5); 	// SArr == [ 	//   { Int: 0, Ptr: nullptr,    Flt: 0.0f  }, 	//   { Int: 5, Ptr: 0x12345678, Flt: 3.14f }, 	//   { Int: 2, Ptr: 0x87654321, Flt: 2.72f }, 	//   { Int: 0, Ptr: nullptr,    Flt: 0.0f  }, 	//   { Int: 0, Ptr: nullptr,    Flt: 0.0f  } 	// ]`
Copy full snippet
```
SArr.SetNumUninitialized(3); new ((void\*)(SArr.GetData() + 1)) S(5, (void\*)0x12345678, 3.14); new ((void\*)(SArr.GetData() + 2)) S(2, (void\*)0x87654321, 2.72); // SArr == \[ // { Int: 0, Ptr: nullptr, Flt: 0.0f }, // { Int: 5, Ptr: 0x12345678, Flt: 3.14f }, // { Int: 2, Ptr: 0x87654321, Flt: 2.72f } // \] SArr.SetNumZeroed(5); // SArr == \[ // { Int: 0, Ptr: nullptr, Flt: 0.0f }, // { Int: 5, Ptr: 0x12345678, Flt: 3.14f }, // { Int: 2, Ptr: 0x87654321, Flt: 2.72f }, // { Int: 0, Ptr: nullptr, Flt: 0.0f }, // { Int: 0, Ptr: nullptr, Flt: 0.0f } // \]

Use the "Uninitialized" and "Zeroed" families of functions carefully. If an element type includes a member that needs construction, or that doesn't have a valid bitwise-zeroed state, it can result in invalid array elements and undefined behavior. These functions are most useful on arrays of types that will likely never change, like FMatrix or FVector.

## Miscellaneous

The `BulkSerialize` function is a serialization function that can be used as an alternative `operator<<` in order to serialize the array as a block of raw bytes, rather than doing per-element serialization. This can improve performance with trivial elements, like a built-in type or a plain data struct.

The `CountBytes` and `GetAllocatedSize` functions are used to estimate how much memory is currently being utilized by the array. `CountBytes` takes an `FArchive`, while `GetAllocatedSize` can be called directly. These functions are typically used for stats reporting.

The `Swap` and `SwapMemory` functions both take two indices and will swap the value of the elements at those indices. They are equivalent except that `Swap` does some extra error checking on the indices and will assert if the indices are out of range.