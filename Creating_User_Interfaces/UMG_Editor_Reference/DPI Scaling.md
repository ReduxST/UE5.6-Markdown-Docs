# DPI Scaling

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dpi-scaling-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dpi-scaling-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:15

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f231af35-0f22-4ce0-9ed2-23df8a273829/dpiscaling.png)

**UMG** supports automatic scaling for resolution-independent UI. There are default DPI scaling settings applied to every project. You can configure it by the **Project Settings** menu under the **User Interface** section. You can change **Application Scale** value via the input box, choose option of **DPI Scale Rule** and adjust **DPI Curve**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/059073e8-0158-4590-bd07-d3501f5706a5/projectsettings.png)

You can set the **DPI Scale Rule** to one of four options:

-   **Shortest Side**: Evaluates the scale curve based on the shortest side of the viewport (Most Common Setting).
-   **Longest Side**: Evaluates the scale curve based on the longest side of the viewport.
-   **Horizontal**: Evaluates the scale curve based on the X axis of the viewport.
-   **Vertical**: Evaluates the scale curve based on the Y axis of the viewport.

Right-click on the DPI Curve graph allows you to add points to the curve by selecting the **Add Key** option. After that you can set the resolution and its corresponding scale value via the input boxes. Also, you can supply an external **Float Curve** or create a Float Curve based on the currently applied settings by expanding the **DPI Curve** option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87a3c79d-90c8-4389-87a9-51bc155cbb20/externalcurve.png)