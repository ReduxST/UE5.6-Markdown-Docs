# Slate Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/slate-overview-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/slate-overview-for-unreal-engine)  
**Processed:** 2025-06-14 16:51:04

---

![Unreal Editor is built with the Slate UI framework](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55a37f40-54b1-4e36-8c1c-580b2bb61dcf/editor.png)

**Slate** is a completely custom and platform agnostic user interface framework that is designed to make building the user interfaces for tools and applications such as Unreal Editor, or in-game user interfaces, fun and efficient. It combines a declarative syntax with the ability to easily design, lay out, and style components that allows for easily creating and iterating on UIs.

The Slate UI solution makes it extremely easy to put together graphical user interfaces for tools and applications and iterate on them quickly.

## Declarative Syntax

Slate's declarative syntax makes building UIs accessible to programmers without adding layers of indirection. A complete set of macros are provided to simplify the process of declaring and creating new widgets.

```
	`SLATE_BEGIN_ARGS( SSubMenuButton ) 		: _ShouldAppearHovered( false ) 		{} 		/** The label to display on the button */ 		SLATE_ATTRIBUTE( FString, Label ) 		/** Called when the button is clicked */ 		SLATE_EVENT( FOnClicked, OnClicked ) 		/** Content to put in the button */ 		SLATE_NAMED_SLOT( FArguments, FSimpleSlot, Content ) 		/** Whether or not the button should appear in the hovered state */ 		SLATE_ATTRIBUTE( bool, ShouldAppearHovered ) 	SLATE_END_ARGS()`
Copy full snippet
```
SLATE\_BEGIN\_ARGS( SSubMenuButton ) : \_ShouldAppearHovered( false ) {} /\*\* The label to display on the button \*/ SLATE\_ATTRIBUTE( FString, Label ) /\*\* Called when the button is clicked \*/ SLATE\_EVENT( FOnClicked, OnClicked ) /\*\* Content to put in the button \*/ SLATE\_NAMED\_SLOT( FArguments, FSimpleSlot, Content ) /\*\* Whether or not the button should appear in the hovered state \*/ SLATE\_ATTRIBUTE( bool, ShouldAppearHovered ) SLATE\_END\_ARGS()

## Composition

Slate's composition framework makes it simple to re-arrange UI elements quickly for prototyping and iteration.

Here is an example of a piece of the UI being composed:

```
	`// Add a new section for static meshes 	ContextualEditingWidget->AddSlot() 	.Padding( 2.0f ) 	[ 		SNew( SDetailSection ) 		.SectionName("StaticMeshSection") 		.SectionTitle( LOCTEXT("StaticMeshSection", "Static Mesh").ToString() ) 		.Content() 		[ 			SNew( SVerticalBox ) 			+ SVerticalBox::Slot() 			.Padding( 3.0f, 1.0f ) 			[ 				SNew( SHorizontalBox ) 				+ SHorizontalBox::Slot() 				.Padding( 2.0f ) 				[ 					SNew( SComboButton ) 					.ButtonContent() 					[ 						SNew( STextBlock ) 						.Text( LOCTEXT("BlockingVolumeMenu", "Create Blocking Volume") ) 						.Font( FontInfo ) 					] 					.MenuContent() 					[ 						BlockingVolumeBuilder.MakeWidget() 					] 				] 			]  		] 	];`

Copy full snippet
```
// Add a new section for static meshes ContextualEditingWidget->AddSlot() .Padding( 2.0f ) \[ SNew( SDetailSection ) .SectionName("StaticMeshSection") .SectionTitle( LOCTEXT("StaticMeshSection", "Static Mesh").ToString() ) .Content() \[ SNew( SVerticalBox ) + SVerticalBox::Slot() .Padding( 3.0f, 1.0f ) \[ SNew( SHorizontalBox ) + SHorizontalBox::Slot() .Padding( 2.0f ) \[ SNew( SComboButton ) .ButtonContent() \[ SNew( STextBlock ) .Text( LOCTEXT("BlockingVolumeMenu", "Create Blocking Volume") ) .Font( FontInfo ) \] .MenuContent() \[ BlockingVolumeBuilder.MakeWidget() \] \] \] \] \];

The composition above creates the UI elements below:

![Rendered UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04411044-0cb2-4a43-bdee-3a7e8d306762/slate_composition.png)

## Styles

Styles can be created and applied to the various parts of a widget. This makes it easy to iterate on the look of the components in the UI, as well as share and reuse styles.

```
	`// Tool bar 	{ 		Set( "ToolBar.Background", FSlateBoxBrush( TEXT("Common/GroupBorder"), FMargin(4.0f/16.0f) ) );  		Set( "ToolBarButton.Normal", FSlateNoResource() );		// Note: Intentionally transparent background 		Set( "ToolBarButton.Pressed", FSlateBoxBrush( TEXT("Old/MenuItemButton_Pressed"), 4.0f/32.0f ) ); 		Set( "ToolBarButton.Hovered", FSlateBoxBrush( TEXT("Old/MenuItemButton_Hovered"), 4.0f/32.0f ) );  		// Tool bar buttons are sometimes toggle buttons, so they need styles for "checked" state 		Set( "ToolBarButton.Checked", FSlateBoxBrush( TEXT("Old/MenuItemButton_Pressed"),  4.0f/32.0f, FLinearColor( 0.3f, 0.3f, 0.3f ) ) ); 		Set( "ToolBarButton.Checked_Hovered", FSlateBoxBrush( TEXT("Old/MenuItemButton_Hovered"),  4.0f/32.0f ) ); 		Set( "ToolBarButton.Checked_Pressed", FSlateBoxBrush( TEXT("Old/MenuItemButton_Pressed"),  4.0f/32.0f, FLinearColor( 0.5f, 0.5f, 0.5f ) ) );  		// Tool bar button label font 		Set( "ToolBarButton.LabelFont", FSlateFontInfo( TEXT("Roboto-Regular"), 8 ) ); 	}`

Copy full snippet
```
// Tool bar { Set( "ToolBar.Background", FSlateBoxBrush( TEXT("Common/GroupBorder"), FMargin(4.0f/16.0f) ) ); Set( "ToolBarButton.Normal", FSlateNoResource() ); // Note: Intentionally transparent background Set( "ToolBarButton.Pressed", FSlateBoxBrush( TEXT("Old/MenuItemButton\_Pressed"), 4.0f/32.0f ) ); Set( "ToolBarButton.Hovered", FSlateBoxBrush( TEXT("Old/MenuItemButton\_Hovered"), 4.0f/32.0f ) ); // Tool bar buttons are sometimes toggle buttons, so they need styles for "checked" state Set( "ToolBarButton.Checked", FSlateBoxBrush( TEXT("Old/MenuItemButton\_Pressed"), 4.0f/32.0f, FLinearColor( 0.3f, 0.3f, 0.3f ) ) ); Set( "ToolBarButton.Checked\_Hovered", FSlateBoxBrush( TEXT("Old/MenuItemButton\_Hovered"), 4.0f/32.0f ) ); Set( "ToolBarButton.Checked\_Pressed", FSlateBoxBrush( TEXT("Old/MenuItemButton\_Pressed"), 4.0f/32.0f, FLinearColor( 0.5f, 0.5f, 0.5f ) ) ); // Tool bar button label font Set( "ToolBarButton.LabelFont", FSlateFontInfo( TEXT("Roboto-Regular"), 8 ) ); }

Styles used in composition:

```
	`SNew( SBorder ) 	.BorderImage( FEditorStyle::GetBrush( "ToolBar.Background" ) ) 	.Content() 	[ 		SNew(SHorizontalBox)  		// Compile button (faked to look like a multibox button) 		+SHorizontalBox::Slot() 		[ 			SNew(SButton) 			.Style(TEXT("ToolBarButton")) 			.OnClicked( InKismet2.ToSharedRef(), &FKismet::Compile_OnClicked ) 			.IsEnabled( InKismet2.ToSharedRef(), &FKismet::InEditingMode ) 			.Content() 			[ 				SNew(SVerticalBox) 				+SVerticalBox::Slot() 				.Padding( 1.0f ) 				.HAlign(HAlign_Center) 				[ 					SNew(SImage) 					.Image(this, &SBlueprintEditorToolbar::GetStatusImage) 					.ToolTipText(this, &SBlueprintEditorToolbar::GetStatusTooltip) 				] 				+SVerticalBox::Slot() 				.Padding( 1.0f ) 				.HAlign(HAlign_Center) 				[ 					SNew(STextBlock) 					.Text(LOCTEXT("CompileButton", "Compile")) 					.Font( FEditorStyle::GetFontStyle( FName( "ToolBarButton.LabelFont" ) ) ) 					.ToolTipText(LOCTEXT("CompileButton_Tooltip", "Recompile the blueprint")) 				] 			] 		] 	]`

Copy full snippet
```
SNew( SBorder ) .BorderImage( FEditorStyle::GetBrush( "ToolBar.Background" ) ) .Content() \[ SNew(SHorizontalBox) // Compile button (faked to look like a multibox button) +SHorizontalBox::Slot() \[ SNew(SButton) .Style(TEXT("ToolBarButton")) .OnClicked( InKismet2.ToSharedRef(), &FKismet::Compile\_OnClicked ) .IsEnabled( InKismet2.ToSharedRef(), &FKismet::InEditingMode ) .Content() \[ SNew(SVerticalBox) +SVerticalBox::Slot() .Padding( 1.0f ) .HAlign(HAlign\_Center) \[ SNew(SImage) .Image(this, &SBlueprintEditorToolbar::GetStatusImage) .ToolTipText(this, &SBlueprintEditorToolbar::GetStatusTooltip) \] +SVerticalBox::Slot() .Padding( 1.0f ) .HAlign(HAlign\_Center) \[ SNew(STextBlock) .Text(LOCTEXT("CompileButton", "Compile")) .Font( FEditorStyle::GetFontStyle( FName( "ToolBarButton.LabelFont" ) ) ) .ToolTipText(LOCTEXT("CompileButton\_Tooltip", "Recompile the blueprint")) \] \] \] \]

## Input

Slate has support for accepting mouse and keyboard input. It provides a flexible key binding system that makes it possible to bind any key combination to any command; including the ability to dynamically modify those bindings.

## Output

Slate uses target agnostic rendering primitives allowing it to potentially run on any platform. It currently targets the Unreal Engine 4 (UE4) Rendering Hardware Interface (RHI) so it can run on any platform that UE4 runs on.

## Layout Primitives

Layout Primitives make it easy to build static and dynamic layouts.

```
	`FString DefaultLayout = 					TEXT( "	{" ) 					TEXT( "		\"type\": \"tabstack\"," ) 					TEXT( "		\"sizecoeff\": 1," ) 					TEXT( "		\"children\":" ) 					TEXT( "		[" ) 					TEXT( "			{" ) 					TEXT( "				\"type\": \"tab\"," ) 					TEXT( "				\"content\": \"Widget Inspector Tab\"" ) 					TEXT( "			}," ) 					TEXT( "			{" ) 					TEXT( "				\"type\": \"tab\"," ) 					TEXT( "				\"content\": \"Plugin Manager Tab\"" ) 					TEXT( "			}," ) 					TEXT( "			{" ) 					TEXT( "				\"type\": \"tab\"," ) 					TEXT( "				\"content\": \"Debug Tools\"" ) 					TEXT( "			}" ) 					TEXT( "		]" ) 					TEXT( "	}" );`

Copy full snippet
```
FString DefaultLayout = TEXT( " {" ) TEXT( " \\"type\\": \\"tabstack\\"," ) TEXT( " \\"sizecoeff\\": 1," ) TEXT( " \\"children\\":" ) TEXT( " \[" ) TEXT( " {" ) TEXT( " \\"type\\": \\"tab\\"," ) TEXT( " \\"content\\": \\"Widget Inspector Tab\\"" ) TEXT( " }," ) TEXT( " {" ) TEXT( " \\"type\\": \\"tab\\"," ) TEXT( " \\"content\\": \\"Plugin Manager Tab\\"" ) TEXT( " }," ) TEXT( " {" ) TEXT( " \\"type\\": \\"tab\\"," ) TEXT( " \\"content\\": \\"Debug Tools\\"" ) TEXT( " }" ) TEXT( " \]" ) TEXT( " }" );

The layout above creates the UI below:

![UI Layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d97094f0-e5c2-4abf-a531-4583fe792317/slate_layout.png)

## User Driven Layout

Slate's docking framework puts the power into the user's hands by allowing its tabbed panels to be rearranged and docked into virtually any layout imaginable. The ability to customize their environment lets the user work with the tools they want to work with the way they want to work with them.

Floating tab:

![Docking](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42f8b723-2137-4020-b5df-4b1390f556d2/docking_before.png)

Drag tab to docking target:

![Drag to Docking Area](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72c13888-a28b-4fe5-8301-6668bcf92347/docking_place.png)

Docked tab:

![Docked](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e77ac416-c625-4c2b-878a-f2a26f0a3d18/docking_after.png)

## Developer tools

The **Slate Widget Reflector** provides a means of debugging and analyzing the UI and associated code. This helps track down bugs and undesirable behavior as well as profile and optimize your user interface.

![Widget Inspector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa6e35e6-279c-48d4-838b-b5de9d7d0982/widget_inspector.png)

## Engine Access

The Slate UI system provides direct access to engine and editor for programmers; making it much easier to implement new features and tools to accommodate the workflow of any development team and requirements of any project.