# Blueprint Editor Compiler Results

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/compiler-results-in-the-blueprints-visual-scripting-editor-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/compiler-results-in-the-blueprints-visual-scripting-editor-for-unreal-engine)  
**Processed:** 2025-06-14 16:14:32

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a23211af-b3ea-4938-8a8d-04f85e87a33c/compilerwindow.png)

The **Compiler Results** panel provides feedback on the compiling of your Blueprint scripts, telling you whether a Blueprint script compile was successful or if there were errors or warnings. Whenever errors or warnings are found, the **Compiler Results** panel gives information on the error and provides hyperlink access, enabling you to jump the graph view directly to the source of the problem.

## Interface

The UI of the **Compiler Results** panel is very simple, consisting primarily of a self-populated list of compile successes, warnings, and errors (failures). Each entry can be moused over for further information, where applicable, and any warnings or errors will also offer a hyperlink, which will take you to the source of the message.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e6218ed-c801-43fb-8ef7-d61180f38d34/compileresultsui.png)

1.  Result List - This self-populated list shows the results of your compile. Any hyperlinks to errors and warnings will appear. If the compile was successful, you will also see the total compile time in milliseconds.
2.  Pop-up Help - By mousing over any entry in the list, you can get more information about the nature of the entry. In the case of hyperlinks, you will get the path directly to the problematic node.
3.  Clear Button - This simply clears out the existing list of results.

## Opening the Compiler Results Panel

The **Compiler Results** panel will not always be available by default, but can be found within the **Window** menu of the Blueprint Editor. The panel will also open automatically whenever a Blueprint compile results in errors or warnings. Generally, the panel will appear at the bottom of the current **Graph** panel.

## Error and Warning Navigation

Whenever your compile process results in a warning or error, the **Compiler Results** panel enables you to do the following:

-   Mouse over a message to see further detail.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a790f493-b21c-4319-b035-2ee531566cf6/mouseovermessage.png)
-   Mouse over the hyperlink at the end of a message to see a link to the problematic node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70cb103e-30fb-4662-b9bc-b2002f90ffe2/mouseoverlink.png)
-   Click on a message to jump the graph view directly to the problematic node or part of the visual script.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/667883a8-afdb-41ec-9b09-830a45a76199/warningfocus.jpg)
-   Click the **Clear** button at the bottom right corner of the panel to clear out any existing messages.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58fa9946-6704-4ecd-83db-5818ed4957bb/clearbuttons.png)