# Wrap Box

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/wrapping-umg-widgets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/wrapping-umg-widgets-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:12

---

**Wrap Box** Widget is a widget you can add to the UI layout to arrange child widgets. Arrangement is from left to right. Widgets that exceed the width, will be placed on the next line.

This page gives basic information about using and adjustment the Wrap Box Widget in the UI layout. Also, get familiar with example of using and adjustment the Wrap Box Widget below using **Unreal Motion Graphics UI Designer (UMG)**.

## Details

In the **Details** panel of a Widget that is placed inside a **Wrap Box**, there are some settings that can be used to adjust how the Widget functions which are outlined below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bea18c37-0815-4621-a544-bef76fefe706/wrapboxslotdetails.png)

| Option | Description |
| --- | --- |
| **Padding** | Sets the padding area between the slot and the content it contains. |
| **Fill Empty Space** | Determines if the slot should fill the remaining space on the line. |
| **Fill Span when Less Than** | This states that if the total available space in the wrap box drops below the specified threshold, the slot will attempt to fill the entire line. A value of 0 denotes that no filling will occur. |
| **Horizontal Alignment** | Sets the alignment of the object horizontally. |
| **Vertical Alignment** | Sets the alignment of the object vertically. |
| **Force New Line** | Sets current slot start on a new line. |

## Usage Example

The Wrap Box is useful when you want to arrange items within a container and have those items appear aligned and evenly spaced and automatically format the contents inside it based on the width of the container. Create a widget layout with this hierarchy to work with the example below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fd724e5-35dd-4646-9276-025b331c24e7/wrapbox_hierarchy.png)

Image below represents layout of created a "shop" screen of sorts where several items are presented to the player.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e4282e3-c561-4841-bbd8-3485fb72b7dd/wrapbox1.png)

The white images above could represent different items that the player could buy when clicking on an item, then clicking the purchase button. In our example say we wanted to remove the item from the shop when it has been purchased or add an item to the shop when the "sell" button is pressed (of course you would probably want a pop-up menu to select the item you want to sell but this should convey the idea).

For example, "buying" and removing items would automatically update the window:

As would "selling" and adding items (automatically wrapping when reaching the max width of the window):

It could also be used to keep things inside it arranged when resizing the window:

While the Wrap Box only checks width to determine when to arrange the Widgets within it, you could also use this in combination with a Scroll Box which will add a scroll bar when the amount of Widgets within the window becomes cut off allowing the user to scroll down to see the remaining Widgets.