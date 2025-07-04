# Automation Driver

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/automation-driver-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/automation-driver-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:24

---

The **Automation Driver** is an **Unreal Engine** feature that enables programmers to simulate user input through the application using fluent syntax. The Automation Driver is very similar in feature set to other external libraries you might find for browser input simulation and is primarily used, like these other libraries, to write functional tests that simulate user behavior.

![Automation Driver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7dc283e-11ba-46aa-a26b-2f2b68918f53/automationdriver.gif)

## What can it do?

The Automation Driver simulates input, which means that it can simulate cursor movement, clicks, pressing, typing, scrolling, drag-and-drop, and more. In this initial revision of the Automation Driver, it supports the full suite of traditional desktop input, basically all keyboard and mouse-related inputs. In the future, we may expand this to include touch gestures, controller input, and even motion detection.

The Automation Driver specializes in simulating this input in a fluent, readable way that is easy to maintain and relatively non-brittle. And most importantly, because the Automation Driver simulates input at the platform layer, its public API is not dependent on Slate. With a little work, it can be extended to work with scene actors or beyond.

This feature is also platform agnostic, so it can be used on any platform as long as it can simulate the primary input types for that platform.

## How does it work?

Within [Core](/documentation/en-us/unreal-engine/API/Runtime/Core), there is a set of interfaces that nearly all external input goes through. The Automation Driver creates shim implementations of these interfaces, and via some basic dependency injection, it can swap out the real implementations with its "pass-through" variations. These "pass-through" variations then have the opportunity to delegate what platform input gets through to the application and what does not, as well as faking its own input entirely, which is how the Automation Driver does its work.

## How do I use it?

By default, the Automation Driver is disabled. You can activate it by calling the `Enable()` function on the Module API. You can disable it by calling the `Disable()` function.

```
	`IAutomationDriverModule::Get().Enable();  	//@todo simulate user behavior here  	IAutomationDriverModule::Get().Disable();`

Copy full snippet
```
IAutomationDriverModule::Get().Enable(); //@todo simulate user behavior here IAutomationDriverModule::Get().Disable();

Once activated, the Automation Driver begins blocking nearly all platform input received by the application. At this point, you can now create your own driver instance.

```
	`FAutomationDriverPtr Driver = IAutomationDriverModule::Get().CreateDriver();`

Copy full snippet
```
FAutomationDriverPtr Driver = IAutomationDriverModule::Get().CreateDriver();

Once you have your own driver instance, you can start simulating input. Here is a quick example of how you might simulate input for a sign-up form:

```
	`FDriverElementRef SignUpForm = Driver->FindElement(By::Id("Form")); 	FDriverElementRef SubmitBtn = Driver->FindElement(By::Path("#Form//Submit"));  	FDriverSequenceRef Sequence = Driver->CreateSequence(); 	Sequence->Actions() 		.Focus(SignUpForm) 		.Type(TEXT("FirstName\tLastName\[[email protected]](/cdn-cgi/l/email-protection)")) 		.Click(SubmitBtn); 	Sequence->Perform();`

Copy full snippet
```
FDriverElementRef SignUpForm = Driver->FindElement(By::Id("Form")); FDriverElementRef SubmitBtn = Driver->FindElement(By::Path("#Form//Submit")); FDriverSequenceRef Sequence = Driver->CreateSequence(); Sequence->Actions() .Focus(SignUpForm) .Type(TEXT("FirstName\\tLastName\\tFirstName.LastName@example.com")) .Click(SubmitBtn); Sequence->Perform();

### Using the API

There are two primary APIs for interacting with the Automation Driver - a synchronous and an asynchronous API. The synchronous API is the easiest to write code for, but you cannot run the code on the GameThread. This is because the synchronous API blocks and waits for the input simulation to complete before continuing. While the input simulation is still queued as latent logic to run on the GameThread, the blocking synchronous driver API ensures the simulated input never gets handled by creating a deadlock - avoid doing this.

All of the examples in this primer are going to use the synchronous API, assuming the logic is not being executed on the GameThread.

If you find this a challenging concept, you should read about the new [Automation Spec](/documentation/en-us/unreal-engine/automation-spec-in-unreal-engine) test types.

### Finding Elements

The first step to generating any useful input is going to be identifying key parts of the application to interact with. The Automation Driver does this via Locators, and there are a handful of fluent ways to use some of the existing locators that are capable of discovering Slate-based elements.

#### By::Id()

Locating elements based by Id is the most ideal method of doing so. It is significantly less likely to break as it requires that a programmer tag a widget with an explicit Automation Driver metadata Id.

Tagging a widget is trivial and can be done like the following:

```
	`SNew(STextBlock) 	.Text(InViewModel, &IViewModel::GetFirstName) 	.AddMetaData(FDriverMetaData::Id("SignUpFormFirstNameField"))`

Copy full snippet
```
SNew(STextBlock) .Text(InViewModel, &IViewModel::GetFirstName) .AddMetaData(FDriverMetaData::Id("SignUpFormFirstNameField"))

It is best that Ids be as specific as possible so that they are unlikely to collide with any other Id, making them much easier to reference. Ids can be referenced by path, and thus scoped by other Ids and elements. But it is best to generate a unique Id so that the test does not have to rely on a brittle scope context.

For example, if your Id is guaranteed unique, then you can locate that widget like so:

```
	`FDriverElementRef FirstNameField = Driver->FindElement(By::Id("SignUpFormFirstNameField"));`

Copy full snippet
```
FDriverElementRef FirstNameField = Driver->FindElement(By::Id("SignUpFormFirstNameField"));

And if your Id is not unique, but represents a unique set of elements, then you can locate all those elements at once using the following:

```
	`FDriverElementCollectionRef SignUpFormFields = Driver->FindElements(By::Id("SignUpFormField")); 	TArray<FDriverElementRef> Fields = SignUpFormFields->GetElements();`

Copy full snippet
```
FDriverElementCollectionRef SignUpFormFields = Driver->FindElements(By::Id("SignUpFormField")); TArray<FDriverElementRef> Fields = SignUpFormFields->GetElements();

Invoking the `GetElements()` method on the element collection is what actually initiates element discovery, so be aware of that in case the elements you are looking for come and go. You may need to explicitly wait for them to appear.

#### By::Path()

Locating elements by path is the most brittle and powerful way to type of location currently available. The `By::Path()` locator enables you obtain specific elements via a hierarchy of tag, id and/or type matching.

Here are some examples of the syntax:

```
	`By::Path("#SignUpFormFirstNameField") 	By::Path("FormField")) 	By::Path("Documents//Tiles") 	By::Path("<SAutomationDriverSpecSuite>") 	By::Path("#Piano//#KeyB/<STextBlock>") 	By::Path("#Suite//Form//Rows//#A1//<SEditableText>")`

Copy full snippet
```
By::Path("#SignUpFormFirstNameField") By::Path("FormField")) By::Path("Documents//Tiles") By::Path("<SAutomationDriverSpecSuite>") By::Path("#Piano//#KeyB/<STextBlock>") By::Path("#Suite//Form//Rows//#A1//<SEditableText>")

##### Path Syntax

| Syntax | Description |
| --- | --- |
| `#SignUpFormFirstNameField` | `#` represents that the following text is an explicit Id. In the case of an `SWidget`, it needs to be tagged with the Automation Driver Id metadata. |
| `FormField` | Plain text represents general tags, and in the case of a `SWidget`, it needs to have a `Tag` or `TagMetadata` with a matching plain text value. |
| `<STextBlock>` | `<>` represents types, and in the case of a `SWidget`, it should be the explicit type used in the `SNew` construction. You can easily create paths using types by looking at the Widget Reflector. |
| `/` | Hierarchy is represented by forward slashes, and a single forward slash represents that the next value must match a direct child of the element matched before it. |
| `//` | Hierarchy is represented by forward slashes, and a double forward slash represents that the next value must match any descendant of the element matched before it. |

In the future, more syntax options will be added to the path locator, but these are the options that are currently available.

There is no support for escape characters, which means that the path locator cannot successfully match Tags or Ids that contain preceding `<` or `#` characters.

To check out additional syntax usage examples, read through: `Engine/Source/Developer/AutomationDriver/Private/Specs/AutomationDriver.spec.cpp`

#### By::Cursor()

This locator returns the element directly under the cursor's current position.

```
	`FDriverElementRef ElementUnderCursor = Driver->FindElement(By::Cursor());`

Copy full snippet
```
FDriverElementRef ElementUnderCursor = Driver->FindElement(By::Cursor());

#### By::Delegate()

If none of these existing locators can do what you need them to do, you can pass your own delegate or lambda via `By::Delegate()` or its various overloads. The Automation Driver will then invoke that block of code on the game thread when attempting to locate the elements.

```
	`FDriverElementRef CustomElement = Driver->FindElement(By::WidgetLambda([this](TArray<TSharedRef<SWidget>>& OutWidgets){ 		OutWidgets.Add(SpeciallyCachedWidget); 	}));`

Copy full snippet
```
FDriverElementRef CustomElement = Driver->FindElement(By::WidgetLambda(\[this\](TArray<TSharedRef<SWidget>>& OutWidgets){ OutWidgets.Add(SpeciallyCachedWidget); }));

### Performing Actions

There are two primary ways to perform actions with the Automation Driver. When working with a single element (or a small set of elements), the easiest way is to use the actions available directly on `FDriverElementRef`. The other option is to create a `FDriverSequenceRef`, which enables you to queue up a long series of actions that can be performed against many different elements (or no specific elements at all).

#### Elements

Several available actions can be performed directly from it after a driver element reference is obtained, for example:

```
	`Driver->FindElement(By::Id("Submit"))->Click();`

Copy full snippet
```
Driver->FindElement(By::Id("Submit"))->Click();

In this example, after obtaining the reference to the `#Submit` element, we are directly invoking the default `Click` method. All actions directly available off a driver element reference only impact the element they are being invoked from. So with the above `Click` example, the Automation Driver will first attempt to move the cursor to the `#Submit` element. If the element does not exist in the Slate DOM, then the driver will wait for up to the implicitly configured timespan defined in the Automation Driver Configuration. If the element appears before timing out, then it will attempt to move the cursor over the element. If the element is off screen, the driver will attempt to locate a method of moving the element onto the screen, such as scrolling it into view. Once in view, the cursor is moved over the element, and only then is the full click simulated.

All driver element reference methods work in this fashion, so their actions attempt to only impact the element.

#### Sequences

A driver sequence is a more robust way of issuing actions for the driver. With a sequence, you can perform actions ignorant of the elements it may be affecting, or you can perform actions against a specific set of elements. Additionally, sequences can be invoked multiple times, which makes them very reusable and great for helper libraries.

```
	`FDriverSequenceRef Sequence = Driver->CreateSequence(); 	Sequence->Actions() 		.MoveToElement(By::Id("Submit")) 		.Click(EMouseButtons::Left); 	Sequence->Perform();`

Copy full snippet
```
FDriverSequenceRef Sequence = Driver->CreateSequence(); Sequence->Actions() .MoveToElement(By::Id("Submit")) .Click(EMouseButtons::Left); Sequence->Perform();

A sequence does not perform its actions until `Perform()` is called. Once an action has been added to the sequence, it cannot be removed. Additional actions cannot be added to a sequence while it is being performed, but more can be added once it finishes.

If any action fails, then the whole sequence fails and execution stops at that point in the series.

#### Actions

For full details on all the types of actions that can simulated, refer to the following files:

-   `Engine/Source/Developer/AutomationDriver/Public/IDriverElement.h`
-   `Engine/Source/Developer/AutomationDriver/Public/IDriverSequence.h`

The set of actions is currently limited to keyboard and mouse input, which generally includes:

-   Mouse Move
-   Mouse Wheel Scrolling
-   Click
-   Double Click
-   Press and Hold Button
-   Release Button
-   Type
-   TypeChord Convenient for performing keyboard shortcuts like **Ctrl**+**Shift**+**S**.
-   Press and Hold Key
-   Release Key
-   Focus

This includes supplemental intelligent actions, such as scrolling until a specific element comes into view, getting the text, size or location displayed by an element, and more.

Although we are not actively developing this feature, we may add support for the following:

-   Scene/Actor interaction
-   Controller Input
-   Touch Input/Gesture
-   Motion Detection

#### Waiting

When building user-simulating automation tests, it is common to wait for various events to happen, and the Automation Driver has built-in support to make the act of waiting easier.

All Automation Driver actions automatically wait the configured `ImplicitWait` timespan for any dependent scenarios to occur before timing out and failing an action. An example of this would be waiting for an element to exist and become visible before simulating a click event for it.

You can configure the `ImplicitWait` timespan dynamically and adjust it mid-simulation as needed via the configuration options on the Automation Driver. For example:

The current default `ImplicitWait` timespan is 3 seconds, and you can also perform explicit or conditional waits, for example:

```
	`Driver->Wait(FTimespan::FromSeconds(2));  	FDriverSequenceRef Sequence = Driver->CreateSequence(); 	Sequence->Actions() 		.Wait(Until::ElementExists(ElementA, FWaitTimeout::InSeconds(3))) 		.Focus(ElementA);  	Driver->Wait(Until::ElementIsVisible(ElementA, FWaitInterval::InSeconds(0.25), FWaitTimeout::InSeconds(1)));  	Driver->Wait(Until::ElementIsInteractable(ElementA, FWaitInterval::InSeconds(0.25), FWaitTimeout::InSeconds(1)));  	Driver->Wait(Until::ElementIsScrolledToBeginning(ScrollBox, FWaitTimeout::InSeconds(3)));`

Copy full snippet
```
Driver->Wait(FTimespan::FromSeconds(2)); FDriverSequenceRef Sequence = Driver->CreateSequence(); Sequence->Actions() .Wait(Until::ElementExists(ElementA, FWaitTimeout::InSeconds(3))) .Focus(ElementA); Driver->Wait(Until::ElementIsVisible(ElementA, FWaitInterval::InSeconds(0.25), FWaitTimeout::InSeconds(1))); Driver->Wait(Until::ElementIsInteractable(ElementA, FWaitInterval::InSeconds(0.25), FWaitTimeout::InSeconds(1))); Driver->Wait(Until::ElementIsScrolledToBeginning(ScrollBox, FWaitTimeout::InSeconds(3)));

You can also specify your own delegate or lambda conditional that must be successful before continuing with the simulation. Finally, every wait has a required timeout argument and an optional interval timespan, which defines how frequently the wait condition should be reevaluated.

## Putting It All Together

Since the Automation Driver API cannot be executed on the `GameThread`, it can be a bit challenging to write simulations, but if you couple the Automation Driver with the new Spec test type, this becomes trivial.

Here is a snippet of one of the over one hundred and twenty tests to spec expectations (tests), which are used to ensure that the Automation Driver itself is functioning properly.

Read the [Automation Spec](/documentation/en-us/unreal-engine/automation-spec-in-unreal-engine) test type documentation to better understand what is going on in the following snippet:

```
	`BEGIN_DEFINE_SPEC(FAutomationDriverSpec, "System.Automation.Driver", EAutomationTestFlags::ProductFilter | EAutomationTestFlags::ApplicationContextMask) 		TSharedPtr<SWindow> SuiteWindow; 		TSharedPtr<SAutomationDriverSpecSuite> SuiteWidget; 		TSharedPtr<IAutomationDriverSpecSuiteViewModel> SuiteViewModel; 		FAutomationDriverPtr Driver; 	END_DEFINE_SPEC(FAutomationDriverSpec) 	void FAutomationDriverSpec::Define() 	{ 		BeforeEach([this]() { 			if (IAutomationDriverModule::Get().IsEnabled()) 			{ 				IAutomationDriverModule::Get().Disable(); 			}  			IAutomationDriverModule::Get().Enable();  			if (!SuiteViewModel.IsValid()) 			{ 				SuiteViewModel = FSpecSuiteViewModelFactory::Create(); 			}  			if (!SuiteWidget.IsValid()) 			{ 				SuiteWidget = SNew(SAutomationDriverSpecSuite, SuiteViewModel.ToSharedRef()); 			}  			if (!SuiteWindow.IsValid()) 			{ 				SuiteWindow = FSlateApplication::Get().AddWindow( 					SNew(SWindow) 					.Title(FText::FromString(TEXT("Automation Driver Spec Suite"))) 					.ClientSize(FVector2D(600, 540)) 					[ 						SuiteWidget.ToSharedRef() 					]); 			}  			SuiteWidget->RestoreContents(); 			SuiteWindow->BringToFront(true); 			SuiteViewModel->Reset();  			Driver = IAutomationDriverModule::Get().CreateDriver(); 		});  		Describe("Element", [this]() 		{ 			Describe("Type", [this]() 			{ 				It("should focus the element and type the characters of the specified string", EAsyncExecution::ThreadPool, [this]() 				{ 					FDriverElementRef Element = Driver->FindElement(By::Id("A1")); 					Element->Type(TEXT("ABCDEFGHIJKLMNOPQRSTUVWXYZ")); 					TEST_EQUAL(SuiteViewModel->GetFormString(EFormElement::A1), TEXT("ABCDEFGHIJKLMNOPQRSTUVWXYZ")); 				}); 			}); 		});  		AfterEach([this]() { 			Driver.Reset(); 			IAutomationDriverModule::Get().Disable(); 		}); 	}`

Copy full snippet
```
BEGIN\_DEFINE\_SPEC(FAutomationDriverSpec, "System.Automation.Driver", EAutomationTestFlags::ProductFilter | EAutomationTestFlags::ApplicationContextMask) TSharedPtr<SWindow> SuiteWindow; TSharedPtr<SAutomationDriverSpecSuite> SuiteWidget; TSharedPtr<IAutomationDriverSpecSuiteViewModel> SuiteViewModel; FAutomationDriverPtr Driver; END\_DEFINE\_SPEC(FAutomationDriverSpec) void FAutomationDriverSpec::Define() { BeforeEach(\[this\]() { if (IAutomationDriverModule::Get().IsEnabled()) { IAutomationDriverModule::Get().Disable(); } IAutomationDriverModule::Get().Enable(); if (!SuiteViewModel.IsValid()) { SuiteViewModel = FSpecSuiteViewModelFactory::Create(); } if (!SuiteWidget.IsValid()) { SuiteWidget = SNew(SAutomationDriverSpecSuite, SuiteViewModel.ToSharedRef()); } if (!SuiteWindow.IsValid()) { SuiteWindow = FSlateApplication::Get().AddWindow( SNew(SWindow) .Title(FText::FromString(TEXT("Automation Driver Spec Suite"))) .ClientSize(FVector2D(600, 540)) \[ SuiteWidget.ToSharedRef() \]); } SuiteWidget->RestoreContents(); SuiteWindow->BringToFront(true); SuiteViewModel->Reset(); Driver = IAutomationDriverModule::Get().CreateDriver(); }); Describe("Element", \[this\]() { Describe("Type", \[this\]() { It("should focus the element and type the characters of the specified string", EAsyncExecution::ThreadPool, \[this\]() { FDriverElementRef Element = Driver->FindElement(By::Id("A1")); Element->Type(TEXT("ABCDEFGHIJKLMNOPQRSTUVWXYZ")); TEST\_EQUAL(SuiteViewModel->GetFormString(EFormElement::A1), TEXT("ABCDEFGHIJKLMNOPQRSTUVWXYZ")); }); }); }); AfterEach(\[this\]() { Driver.Reset(); IAutomationDriverModule::Get().Disable(); }); }

The main takeaway is that the lambda passed to `BeforeEach()` executes on the `GameThread` and is setting up the scenario for the test, creating the Widgets, and positioning the window accordingly. The `It()` lambda is where the actual input simulation is happening, and if you look closely, you can see that this one passes the `EAsyncExecution::ThreadPool` value to the `It()`. This causes the lambda to be executed on a thread separate from the `GameThread`, where it is safe to simulate input. Because of this, you can put a breakpoint in your Automation Driver code and step through the various actions as they are performed. Finally, `AfterEach()` cleans up the environment, and it is executed back on the `GameThread`.

### Final Notes

Always be mindful when working with Automation Driver code that you aren't working on the `GameThread` and therefore, it is not safe to make copies of non-thread safe [SharedPtrs](/documentation/en-us/unreal-engine/shared-pointers-in-unreal-engine). This is an important callout because Slate exclusively uses non-thread safe `SharedPtrs`.

If you must access something using a non-thread safe `SharedPtr`, you should make the dedicated `BeforeEach()` blocks for your test, which can enable you to bounce between threads while simulating and checking behavior.

If you know the `SharedPtr` will not be destroyed while executing the test, the other alternative is to cache it on the test class itself, so the `SharedPtr` can be accessed by the lambdas but not cloned, thus not causing race conditions with the reference counting. We do this with the `SuiteViewModel` in the above snippet.

It is generally best to perform all your Automation Driver simulation in a dedicated `BeforeEach()` block, and then do your expectation checking in the `It()` on the `GameThread`.