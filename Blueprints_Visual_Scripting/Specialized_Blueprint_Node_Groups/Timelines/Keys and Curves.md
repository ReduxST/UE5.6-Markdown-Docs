# Keys and Curves

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/keys-and-curves-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/keys-and-curves-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:58

---

Programming Language

×C++

Select an option from the dropdown to see content relevant to it.

A **Curve** (**[UCurveBase](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Curves/UCurveBase?application_version=5.5)**) defines a track of interpolated points to evaluate over a given range. Curves can be **vectors**, **floats**, and **colors**. Each track can have any number of **keys** that define a time and value. The data can be interpolated between these keys to calculate the value at any point during the Timeline.

## Working with Keys and Curves

In this example, you will create a **[UCurveFloat](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Curves/UCurveFloat?application_version=5.5)** that defines a curve of interpolated float points to evaluate over a given range.

To create and instantiate a `UCurveFloat` to a **Timeline Component**, follow the steps below:

1.  Navigate to the **Content Browser**, click **C++ Classes** folder, then click **Add (+)** button and select **New C++ Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/44c98a2c-cb88-460a-86f6-10a2b8d6eae4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/44c98a2c-cb88-460a-86f6-10a2b8d6eae4?resizing_type=fit)
    
2.  Select **Actor** as a **Parent Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4d2664ad-0824-44ef-a79d-14f01721a659?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4d2664ad-0824-44ef-a79d-14f01721a659?resizing_type=fit)
    
    Click image for full size.
    
3.  Name created Actor as **ExampleTimelineComponent**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/20ebda25-dc05-4e2c-b394-e114ce9af0e7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/20ebda25-dc05-4e2c-b394-e114ce9af0e7?resizing_type=fit)
    
    Click image for full size.
    
4.  When new Actor is created, **Visual Studio** automatically opens `ExampleTimelineComponent.h` and `ExampleTimelineComponent.cpp` files. Navigate to the `ExampleTimelineComponent.h` file and add the following to the `#include` section:
    
    ExampleTimelineComponent.h
    
    C++
    
    `#include "Components/TimelineComponent.h"`
    
    #include &quot;Components/TimelineComponent.h&quot;
    
    Copy full snippet(1 line long)
    
5.  Next, in the `ExampleTimelineComponent` class definition, add the following code:
    
    ExampleTimelineComponent.h
    
    C++
    
    `protected:           UPROPERTY(EditAnywhere, BlueprintReadWrite)          UTimelineComponent* ExampleTimelineComp;       public:           UPROPERTY(EditAnywhere)          UCurveFloat* ExampleTimelineCurve;`
    
    protected: UPROPERTY(EditAnywhere, BlueprintReadWrite) UTimelineComponent\* ExampleTimelineComp; public: UPROPERTY(EditAnywhere) UCurveFloat\* ExampleTimelineCurve;
    
    Copy full snippet(9 lines long)
    
6.  Compile your code.
    
7.  Navigate to the **Content Browser**, select **Add (+) > Miscellaneous > Curve**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/56ad9c6f-d047-431f-8ca8-b3d1ca5137cb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/56ad9c6f-d047-431f-8ca8-b3d1ca5137cb?resizing_type=fit)
    
8.  Select **CurveFloat** and name it **ExampleFloatTrack**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/7d793b11-63ac-4ab2-9b45-ad3551dd699d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7d793b11-63ac-4ab2-9b45-ad3551dd699d?resizing_type=fit)
    
9.  In **Content Browser** navigate to the folder with your **ExampleTimelineComponent** class, right click it and select **Create Blueprint Class based on ExampleTimelineComponent**. Name it **BP\_ExampleTimelineComponent**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/5d7972b5-b8d3-45e4-8e57-f2047139acaf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5d7972b5-b8d3-45e4-8e57-f2047139acaf?resizing_type=fit)
    
10.  Open the **BP\_ExampleTimelineComponent** class defaults, navigate to the **Detail** panel and assign your **Example Timeline Curve** with your **ExampleFloatTrack**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/9e4b8db9-3b09-420a-b80f-4a3ce433c60a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9e4b8db9-3b09-420a-b80f-4a3ce433c60a?resizing_type=fit)
    
11.  Double-click your **Example Float Track** from the Content Browser to open the **Timeline Editor**.
    

## Adding Keys

Keys are added by pressing the **Enter** key, or by right clicking on the gray bar and selecting the action **Add Key** from the context menu.

[![](https://dev.epicgames.com/community/api/documentation/image/9970ea3a-9072-4893-a946-f294b6ce116f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9970ea3a-9072-4893-a946-f294b6ce116f?resizing_type=fit)

## Editing Keys

The time and value of the key can be set by clicking the key and entering the values into the time and value fields near the top of the track.

[![](https://dev.epicgames.com/community/api/documentation/image/6d4e5b9f-5fb3-4467-9874-2d3ab3ee0ad0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6d4e5b9f-5fb3-4467-9874-2d3ab3ee0ad0?resizing_type=fit)

## Deleting Keys

Selected keys can be deleted by pressing the **Delete** key on the keyboard, or by right clicking on the key you want to delete and selecting the action **Delete** from the context menu.

## Moving Keys

To move a key along the timeline, select the key, then drag it. Multiple keys can be selected using the **Ctrl** key. Dragging horizontally will update the **Time** value of the key, while dragging vertically will update the **Value**.

## Key Interpolation

By right-clicking a key, a context menu menu appears to choose the interpolation type for selected key.

[![](https://dev.epicgames.com/community/api/documentation/image/0e91265a-7f18-4eea-997a-5c5b36c0f2e7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0e91265a-7f18-4eea-997a-5c5b36c0f2e7?resizing_type=fit)

Key interpolation only affects the curve between the key you interpolate for and the next key after that. For example, with all other keys set to **Linear**, and the center key set to **Cubic-Auto**, the track will look similar to the image below.

[![](https://dev.epicgames.com/community/api/documentation/image/01de5f84-dd04-4ef1-bf03-361ed7126715?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/01de5f84-dd04-4ef1-bf03-361ed7126715?resizing_type=fit)

Available interpolation types are:

-   **Auto**
    
    [![](https://dev.epicgames.com/community/api/documentation/image/d39c25e0-9184-42fb-bf7b-9bebf08bc3c9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d39c25e0-9184-42fb-bf7b-9bebf08bc3c9?resizing_type=fit)
    
-   **User**
    
    [![](https://dev.epicgames.com/community/api/documentation/image/501477e1-8e4b-4202-9cec-c1b01998b6d6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/501477e1-8e4b-4202-9cec-c1b01998b6d6?resizing_type=fit)
    
-   **Break**
    
    [![](https://dev.epicgames.com/community/api/documentation/image/7aaec65a-025c-439e-8e03-5b1ae1178980?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7aaec65a-025c-439e-8e03-5b1ae1178980?resizing_type=fit)
    
-   **Linear**
    
    [![](https://dev.epicgames.com/community/api/documentation/image/d3da9870-209f-40ff-9c55-407bf44a4132?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d3da9870-209f-40ff-9c55-407bf44a4132?resizing_type=fit)
    
-   **Constant**
    
    [![](https://dev.epicgames.com/community/api/documentation/image/fb089950-8e79-4d69-aabf-f97033f47adf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fb089950-8e79-4d69-aabf-f97033f47adf?resizing_type=fit)