# Using Composure with Camera Calibration

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-composure-with-camera-lens-calibration-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-composure-with-camera-lens-calibration-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:34

---

1.  Go to **Window > Virtual Production > Composure Compositing** to open the **Composure** window.
    
    ![Open Composure Compositing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a03d4163-8cb0-4e1b-abde-6938a3ddd796/01-open-composure-window.png "Open Composure Compositing")
2.  Right-click inside the **Composure** window and select **Create New Comp** from the menu. Click the **Empty Comp Shot** button to create a new empty composition.
    
    ![Create a new Comp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/160c217f-6f79-4adc-9d71-a15b795a5c2b/02-create-new-comp.png "Create a new Comp") ![Create an Empty Comp Shot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f706612c-8c9f-4bfd-8e22-8345f19d8c05/03-empty-comp-shot.png "Create an Empty Comp Shot")
3.  Right-click the composure and select **Add Layer Element**. Click the **Media Plate** button. This media plate will use the live video feed from your camera.
    
    ![Add Layer Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c46322ce-1735-4be3-97a8-ee6f880c058e/03-add-layer-element-1.png "Add Layer Element") ![Add a Media Plate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1271dd9-6742-48a2-80bb-c76a25b1f36f/04-create-media-plate.png "Add a Media Plate")
4.  Navigate to **Content Browser > Your project folder for MediaIO >** and drag **MediaBundle-01** into your Level.
    
    Click image to expand.
    
5.  Select the **media plate** in the **Composure** window and go to the **Details** panel. Scroll down to the **Composure** section and expand the **Input** category. Click the **Media Source** dropdown and select **T\_MediaBundle-01\_BC** from the list. You should now see the live video feed streamed on the media plate.
    
    ![Select the Media Plate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76978d3a-a221-4a6f-8251-13a81a29a82a/06-select-media-plate.png "Select the Media Plate")
    
    Click image to expand.
    
6.  Right-click the composure and select **Add Layer Element**. Click the **CG Layer** button.
    
    ![Add a CG Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59ecd8f5-7e96-48bc-9673-57dcd6b6c5b3/09-new-cg-layer.png "Add a CG Layer")
7.  Go to **Window > Layers** to open the **Layers** window.
    
    ![Open the Layers Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdbaf9a9-55d1-4865-b30f-1792a0824749/11-open-layers-window.png "Open the Layers Window")
8.  Select the **BP\_UE\_Tracker3** and the **CameraCalibrationCheckerboard** Blueprints from the **Outliner**. Go to the **Layers** window then right-click and select **Add Selected Actors to New Layer** from the menu. Name the layer **cglayer**.
    
    Click image to expand.
    
    You can also find **BP\_UE\_Tracker3** in the Content Browser under Engine content folder.
    
    Click image to expand.
    
9.  Select the **cg element** layer in the **Composure** window and go to the **Details** panel. Scroll down to the **Composure** section and click the **+** button to expand the **Capture Actors** options. Click the **ActorSet** dropdown and select **cglayer** from the list.
    
    Click image to expand.
    
10.  With the **cg element** layer selected, scroll down to the **LensDistortion** section and select the **Distortion Source** as the **LumixLens** file.
    
    ![Apply Distortion to the CG Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38eace81-ba37-43bf-9010-c2d4e2faa99c/14-select-lens-file.png "Apply Distortion to the CG Layer")
11.  Right-click in the **Content Browser** and select **Material** from the **Create Basic Asset** section. Name the Material **M\_SimpleComp**.
    
    ![Create a New Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dab7bf6-2795-4e57-9bdc-890d8181a38c/15-create-new-material.png "Create a New Material")
12.  Double-click **M\_SimpleComp** to open it. Select the Material node and go to the **Details** panel. Set the **Shading Model** to **Unlit**.
    
    ![Set the Material to Unlit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15659c40-0b05-46c8-8da9-368d8f56596c/15-unlit-shading-model.png "Set the Material to Unlit")
13.  Right-click in the graph then search for and select **TextureSample**. Right-click the **Texture Sample** node and select **Convert to Parameter**. Name it **CGLayer**. Go to the **Details** panel and add a texture to the **CG Layer** dropdown.
    
    ![Add a Texture Sample](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2668841-304c-451e-a377-01183d130937/16-new-texture-sample.png "Add a Texture Sample") ![Convert the Texture to a Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f93e99e3-a98a-4ff2-813a-93bf320205ee/17-convert-to-parametr.png "Convert the Texture to a Parameter") ![Add a Texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6231802-762a-4d10-a528-e6b88c36c2e3/18-new-material-texture-base.png "Add a Texture")
14.  Repeat the previous step and add another **Texture Sample**. Name the parameter **MediaPlate**.
    
    Click image to expand.
    
15.  Right-click in the graph then search for and select **Over**. Connect the **RGBA** pins of both nodes to the **A** and **B pins** of the **Over** node. Finally, connect the **RGBA** pin of the **Over** node to the **Emissive Color** pin of the Material node.
    
    ![Add an Over Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e553801-0205-4f69-bf29-631fa0e7a6de/20-add-over-node.png "Add an Over Node")
    
    Click image to expand.
    
16.  Select your composition from the **Composure** window and go to the **Details** panel. Scroll down to the **Transform / Compositing Passes** section and expand **Transform Passes**. Add the **M\_SimpleComp** Material to the **Material** slot.
    
    Click image to expand.
    
17.  Expand **Input Elements** and add Media Plate and CG Element layers to their corresponding slots. You should now have the video feed streamed to the Media Plate and your selected Actors displayed in the CG Elements layer.
    
    Click image to expand.
    

## Section Results

In this guide you learned how to use Composure with the Camera Calibration plugin.