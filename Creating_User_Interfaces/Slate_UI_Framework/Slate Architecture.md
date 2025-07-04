# Slate Architecture

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-slate-ui-architecture-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-slate-ui-architecture-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:48

---

## How to Read This Page

Core ideas guiding **Slate** design are found here. They are found in no particular order. There is no rigid structure or grand theory here; it is just a collection of principles that arise from UI tinkering experience.

You may find it helpful to re-read this page from time to time as you gain experience with Slate.

## Motivation

The motivations for Slate arise from observations about off-the-shelf UI solutions available at the time. Some follow here:

-   Building up UIs from widgets is already easy in most toolkits. What is hard:
    -   UI Design and iteration.
    -   Controlling the flow of data: usually thought of as binding between widgets (view) and underlying data (model).
    -   Learning a foreign language for describing UIs.
-   IMGUI : Immediate Mode Graphics User Interface
    -   Pros:
        -   Programmers like that UI description is "close" to the code; easy to get at the data.
        -   Invalidation is usually a non-issue; just poll data directly.
        -   Easy to procedurally build interfaces.
    -   Cons:
        -   Adding animation and styling is harder.
        -   UI description is imperative code, so no chance to make it data-driven.
-   Desired Slate Characteristics:
    -   Easy access to model's code and data.
    -   Support procedural UI generation.
    -   UI description should be hard to screw up.
    -   Must support animation and styling.

## Core Tenets

Design for developer efficiency where possible. A programmer's time is expensive; CPUs are fast and cheap.

-   Avoid opaque caches and duplicated state. Historically, UIs cache state and require explicit invalidation. Slate uses following approaches (from preferred to least preferred):
    1.  Polling
    2.  Transparent caches
    3.  Opaque caches with low-grain invalidation
-   When UI structure is changing, prefer polling to notification. (When notification is necessary, prefer low-grain notifications to fine-grain notifications.)
-   Avoid feedback loops. E.g. all layout is computed from programmer settings; never rely on previous layout state.
    -   Only exceptions are when UI state becomes the model; e.g. ScrollBars visualize UI state.
    -   This is done for correctness and programmer sanity rather than performance.
-   Plan for the messy, ad-hoc UIs that require a ton of one-offs to work. Generalize these into nice systems later, when the use-cases are understood.

## Polling Data Flow and Delegates

UIs visualize and manipulate Models. Slate uses delegates as a flexible conduit for widgets that need to read and write the Model's data. Slate widgets read the Model's data when they need to display it. When a user performs some actions, Slate widgets invoke the write delegate in order to modify the data.

Consider **STextBlock** - a Slate widget that displays text. The STextBlock must be told where to get the data to display. The data could be set statically. However, a more flexible way to accomplish this is a delegate (a function specified by the user). The STextBlock uses a delegate called **Text** for this purpose.

![Diagram showing relationship between float data and STextBlock](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/faeccaef-3807-49df-9d38-3acca13cf4b9/stextblock.png)

The STextBlock reads the framerate as a string.

Consider also that in the example above the Text is a string, while the framerate is most likely stored as a `float` or an `integer`. The use of delegates offers us the flexibility to perform the conversion whenever the value is read. This immediately conjures up performance concerns which are addressed in the [Performance Considerations](/documentation/en-us/unreal-engine/understanding-the-slate-ui-architecture-in-unreal-engine#performanceconsiderations) section below.

**SEditableText** is a Slate widget responsible for both input and output. Just like STextBlock, it uses the Text delegate for visualizing data. The user types some text into the editable text field, and when they hit enter, SEditableText invokes the **OnTextChanged** delegate. The assumption is that the programmer has attached the functionality appropriate for validating the input and mutating the Model's data to OnTextChanged.

![Diagram showing two-way relationship between SEditableText and text data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e591d3a8-9844-4438-bfcb-49834c4ee8ac/seditabletext.png)

The SEditable text reads the item name. When the user hits enter, the new text is sent to OnTextChanged where it will be validated and assigned to item name if appropriate.

During the next frame, the SEditableText will read from the Model's data. In the example above, `item name` will have been mutated by the OnTextChanged delegate and will be read for visualization via the Text delegate.

### Attributes and Arguments

Using a delegate is not always desirable. Depending on the use case, the arguments to Slate widgets may need to be constant values or functions. We encapsulate this notion via the `TAttribute < T >` class. An attribute can be set to a constant or to a delegate.

## Performance Considerations

After reading the [Polling Data Flow and Delegates](/documentation/en-us/unreal-engine/understanding-the-slate-ui-architecture-in-unreal-engine#pollingdataflowanddelegates) section, one might have serious concerns about performance.

Consider the following observations:

-   UI complexity is bounded by the number of live widgets.
-   Scrolling content is virtualized whenever possible; this mostly avoids live widgets off-screen.
    -   Large numbers of off-screen widgets can easily tank Slate performance.
-   Assumption: users with big screens have beefy machines to drive those screens; they can handle a large number of widgets.

## Invalidation vs Polling

Sometimes polling is either not performant or functionally incorrect. This is often the case with non-trivial values that cannot be expressed as a combination of simpler, trivial values. We usually invalidate in scenarios where the structure of the Model changes drastically. It is then reasonable to scrap an existing UI and recreate it. However, doing so assumes state loss, so we should not do it unless necessary.

Invalidation is - as a rule - reserved for infrequent, low-granularity events.

Consider the example of the Blueprint Editor, which displays nodes on a graph. When an update is requested, all the **Graph** Panel widgets are cleared and re-created. This is preferable to fine-grain invalidation because it is simpler and more maintainable.

## Child Slots

All Slate widgets store children in child slots. (As opposed to storing a plain array of child widgets.) Child slots always store a valid widget; by default they store the **SNullWidget**, which is a widget with no visualization or interaction. Each type of widget can declare its own type of child slot, which caters to its specific needs. Consider that **SVerticalSlot** arranges its children completely differently than an **SCanvas**, which is quite different from SUniformGridPanel. The Slots allow each type of panel to ask for a set of per-child settings that affect the arrangement of the children.

## Widget Roles

Widgets come in three flavors.

-   **Leaf Widgets** - widgets with no child slots. e.g. STextBlock displays a piece of text. It has native knowledge of how to draw text.
-   **Panels** - widgets with a dynamic number of child slots. e.g. **SVerticalBox** arranges any number of children vertically given some layout rules.
-   **Compound Widgets** - widgets with a fixed number of explicitly named child slots. e.g. **SButton** has one slot called Content which contains any widgets inside the button.

## Layout

Slate layout is accomplished in two passes. The two-pass breakdown is an optimization, but unfortunately not a transparent one.

1.  Pass 1: **Cache Desired Size** - the relevant functions are **SWidget::CacheDesiredSize** and **SWidget::ComputeDesiredSize**
2.  Pass 2: **ArrangeChildren** - the relevant function is **SWidget::ArrangeChildren**

In more detail:

#### Pass 1: Cache Desired Size

The goal of this pass is to figure out how much space each widget wants to occupy. Widgets with no children (i.e. leaf widgets) are asked to compute and cache their desired size based on their intrinsic properties. Widgets that combine other widgets (i.e. compound widgets and panels) use special logic to determine their desired size as a function of the size of their children. Note that each type of widget is only required to implement **ComputeDesiredSize();** the caching and traversal logic are implemented by Slate. Slate guarantees that when ComputeDesiredSize() is called on a widget, its children have already computed and cached their desired size. Thus, this is a bottom-up pass.

In the below example, we examine a horizontal box that arranges two children - a piece of text and an image.

![Diagram showing a horizontal box that arranges two children](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/790cdb36-6cba-406d-b50b-f14ba0d2ad14/cachesize.png)

A horizontal box arranges two children - a text block and an image.

An STextBlock widget would compute its desired size by measuring the string that it is displaying. The SImage widget would determine its size based on the image data it is showing. Assume that the text inside the textblock requires 14 slate units of space, and the image requires 8. The horizontal panel arranges widgets horizontally, and therefore requires 14 + 8 = 22 units of space.

#### Pass 2: ArrangeChildren

ArrangeChildren is a top-down pass. Slate begin at the top-level windows and asks each window to arrange its children based on the constraints provided by the programmers. When the space allotted for each child is known, Slate can recur and arrange the children's children. The recursion continues until all the children are arranged.

![Diagram showing a horizontal panel arranging two children](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cb1c173-013e-45c2-bc53-ca89c4d9b779/arrangechildren.png)

A horizontal panel arranges two children, a text block and an image.

In the example above, the panel was allotted 25 units by its parent. The first slot indicates that it wants to use the desired size of the child, and is allotted 14 units of space. The second slot indicates that it wants to fill the available width, and is allotted the balance (11 units of space). Note that in the actual SHorizontalBox widget, the alignment of the SImage within its slot would be driven by the **HAlign** property, which can be Left, Center, Right, or Fill.

In practice, Slate never performs a full ArrangeChildren pass. Instead, this functionality is used to implement other functionality. Key examples are hit detection and painting.

## Drawing Slate : OnPaint

During the paint pass, Slate iterates over all the visible widgets and produces a list of draw elements which will be consumed by the rendering system. This list is produced anew for every frame.

We begin at the top level windows and recur down the hierarchy, appending the draw elements of every widget to the draw list. Widgets tend to do two things during paint: they output actual draw elements or figure out where a child widget should exist and ask the child widget to paint itself. Thus, we can think of a simplified general-case **OnPaint** function as being:

```
	`// An arranged child is a widget and its allotted geometry 	struct ArrangedChild 	{ 		Widget; 		Geometry; 	}; 	 	OutputElements OnPaint( AllottedGeometry ) 	{ 		// Arrange all the children given our allotted geometry 		Array<ArrangedChild> ArrangedChildren = ArrangeChildrenGiven( AllottedGeometry ); 	 		// Paint the children 		for each ( Child in ArrangedChildren ) 		{ 			OutputElements.Append( Child.Widget.OnPaint( Child.Geometry ) ); 		} 	 		// Paint a border 		OutputElements.Append( DrawBorder() ); 	}`
Copy full snippet
```
// An arranged child is a widget and its allotted geometry struct ArrangedChild { Widget; Geometry; }; OutputElements OnPaint( AllottedGeometry ) { // Arrange all the children given our allotted geometry Array<ArrangedChild> ArrangedChildren = ArrangeChildrenGiven( AllottedGeometry ); // Paint the children for each ( Child in ArrangedChildren ) { OutputElements.Append( Child.Widget.OnPaint( Child.Geometry ) ); } // Paint a border OutputElements.Append( DrawBorder() ); }

## Anatomy of a SWidget

The key functions that define an SWidget's behavior in Slate are:

-   ComputeDesiredSize() - responsible for desired size.
-   ArrangeChildren() - responsible for arrangement of children within the parent's allotted area.
-   OnPaint() - responsible for appearance.
-   Event handlers - these are of the form OnSomething. These are functions that may be invoked on your widget by Slate at various times.

## Composition

Composition is the notion that any slot should be able to contain arbitrary widget content. This affords users of Slate a great deal of flexibility. Composition is used whenever possible in core Slate widgets.

If you are ever thinking that you want a widget to take a string argument to be used as a label, ask yourself if it would not be better off taking an SWidget instead.

Specific use-cases often demand that widgets contain children of a specific type, in which case composition requirements no longer apply. These should never be widgets in the core of slate, but rather domain-specific widgets that are not intended for reuse outside of that domain.

## Declarative Syntax

We wanted Slate to be accessible directly from code. Experience dictated that we needed a declarative language for describing UI, but we also wanted it to be compile-time checked for binding to C++ functions.

The solution was to build a declarative UI-description language as a subset of C++.

Examples abound in the codebase.