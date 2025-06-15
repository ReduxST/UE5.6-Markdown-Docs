# How to Use the ML Deformer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-the-machine-learning-deformer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-the-machine-learning-deformer-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:31

---

Creating accurate, non-linear deformer systems for skinned [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) objects is a complex and computationally-intensive process, especially when calculating these deformation simulations in real-time. Using **Unreal Engine**’s **Machine Learning** (**ML**) **Deformer** Framework, you can train a ML Deformer Model, using externally pre-generated mesh deformation simulation data, to make Morph Target selections in order to approximate high quality mesh deformations at runtime. This workflow greatly improves the quality of in-game mesh deformations without the computational cost of real-time deformation generation.

This document provides an example workflow of generating mesh deformation simulation data in Autodesk Maya, and then using that data in Unreal Engine to train the **Neural Morph ML Deformer Model** to generate a set of Morph Targets that the framework can use to make selections in order to approximate a character's mesh deformations at runtime.

For a more comprehensive overview and reference of the ML Deformer Framework, Editor, and ML Deformer Models, see the following documentation:

#### Prerequisites

-   The **ML Deformer Framework** is a [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) and must be enabled prior to use. Navigate in the Unreal Engine menu to **Edit > Plugins**, locate **ML Deformer Framework** in the **Animation** section, and enable it. After enabling the plugin, you will need to restart the editor.

![ml deformer framework plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2022ebbd-6d3f-41bc-a0a2-b6c889f464a9/plugin1.png)

-   The **ML Deformer Neural Morph Model** is a [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) and must be enabled prior to use. Navigate in the Unreal Engine menu to **Edit** > **Plugins**, locate **ML Deformer Neural Morph Model** in the **Animation** section, and enable it. After enabling the plugin, you will need to restart the editor.

![ml deformer neural morph model plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3427085b-0728-454c-9455-3f4f7f7336b5/plugin2.png)

-   In order to generate the necessary mesh deformation data needed to train the ML Deformer model, you must have access to a robust Digital Content Creation (DCC) tool such as **Autodesk Maya**. We have provided a plugin for Maya that you can use to generate the necessary deformation data for the ML Deformer training process. However, the generated content could come from any DCC using a script that generates random poses and corrected mesh deformation data.
    
-   You have a skinned character in both Unreal Engine and Autodesk Maya.
    

#### ML Deformer Models

The ML Deformer framework uses ML Deformer Models to train and drive skinned mesh deformations at runtime. This workflow uses the Neural Morph Model, you can optionally use a different model that better suits your project’s goals. Each model has benefits and specific use cases and can be accessed by installing their respective plugin. For more information about the different ML Deformer Models, see the [ML Deformer Models](/documentation/en-us/unreal-engine/ml-deformer-framework-in-unreal-engine#mldeformermodels) documentation.

#### ML Deformer Example Content

Additionally, you can download the **Machine Learning** (**ML**) **Deformer Sample Project** that features a showcase of full body character mesh deformations using the ML Deformer system. The sample project includes an interactive cinematic of a [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) driven animated character, that you can observe and compare linear skinned mesh playback against ML Deformer generated deformations. Additionally, you can manipulate the character using alternative animations, **Control Rig** edits, toggle clothing and skin visibility, and observe the effect of different ML Deformer Models in order to observe changes to the mesh and learn more about the ML Deformer system and capabilities.

You can download the [ML Deformer sample project](https://www.fab.com/listings/4c1f2eee-3004-4466-8c86-796e2e94d562) from Fab.

![ml deformer sample project in Fab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70e63904-e281-4fc3-85e2-19414f0c03a2/fab-maya-deformer.png)

## Autodesk Maya Plugin Setup

You will need to download and install the **ML Deformer Data Generation Maya Plugin**. To do this, first navigate to the [Maya ML Deformer - Data Generation Maya Plugin](https://www.fab.com/listings/c3b46f42-2563-4c17-83d9-e7b573974f5b) Fab listing and download the plugin. This workflow example uses the Epic Games developed Maya Plugin to generate random poses for our character. However, these generated random poses could come from any DCC. You can optionally write a script that generates random poses in other DCC applications as well.

![maya ml deformer data generation maya plugin in Fab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54c1a43b-003f-4414-96ee-a9b834a3db18/fab-ml-deformer-sample.png)

When the plugin is installed, it will be located in the **Plugins** folder of your Unreal Engine install directory. By default, it is located under the following path:

`…\Engine\Plugins\Marketplace\MayaMLDeformer\Content\MayaMLDeformer.zip`

Unzip the contents of `MayaMLDeformer.zip` to `C:\Users\"user name"\Documents\maya\modules`.

If the `modules` folder does not exist, you can create it.

![file explorer maya modules ml deformer mod](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/190c6264-e537-4c00-8447-a5bacc0e994c/marketplace2.png)

Now when you open Autodesk Maya, you should see **UE MLDeformer** in the main menu bar.

![ue ml deformer maya toolbar menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/397323cc-c166-4eca-ac6c-7cd93369fcff/mayaresult.png)

## Training Data Generation in Maya

The ML Deformer plugin creates training data for characters by setting procedural keyframes on bones that produce a useful data set for machine learning algorithms. To start the training data generation process, you must first open the tool.

In Maya's main menu bar, click **UE ML Deformer > Data Generator**, which will open the **Training Data Generation Setup** window.

![maya ue ml deformer data generator training data generation setup window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d4ff0fe-48e0-4e6d-ab06-6cb120395ea5/mayatraining1.png)

Also import or open your skinned character in the Maya scene. For this example workflow, a [MetaHuman](https://docs.metahuman.unrealengine.com/en-US) is used.

![example skeletal mesh metahuman bone view maya](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51ef09b6-2721-41a9-8b77-4270174b8da8/mayatraining2.png)

### Adding Bone Parameters

In order to train your joints, you must add a list of nodes and attributes to modify, along with the range of values that these attributes can adopt.

Select all of the mesh's Joints you want to add and click **Add (+)** in the **Parameters** section of the **Training Data Generation Setup** window.

![add bone parameter to training data generation setup using green add button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f99e264-186b-4fa7-8a05-b150c2e37122/boneparams1.png)

After selecting **Add** (**+**) with the mesh's joints selected, the **Add Parameters** window will open, where you can further refine which joint attributes you want to use in the training. You can also click **Refresh** to refresh the parameter list with your current selection.

![add parameters maya window specify motion methods for data generation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c876acc5-9fbe-44b0-a4e1-2e44b8c029fb/boneparams2.png)

Select the joint attributes you want to add as parameters, then click **Add Selected Parameters** to add them to the Training Data Generation Setup. In most cases, only the rotation attributes are necessary from joints.

![add parameters maya window specify rotation methods for data generation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7de3bf3-949e-472f-bd8d-753199620035/boneparams3.png)

You can use the **Attributes Filter** section to automatically refine and exclude attributes. Click **Add (+)** to add a new entry and name it according to the attributes you want to exclude. In this example workflow, add the following entries to the list: lockInfluenceWeights, scaleX, scaleY, scaleZ, translateX, translateY, translateZ, visibility, dropoff, and smoothness.

![add parameters maya window specify methods for the ignore list data generation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71d8335d-fdc7-47db-8b1e-49bf9ba0ae30/boneparams4.png)

### Configure Bone Parameters

With the attributes added, you will now need to configure the range of motion for each axis. This is done by selecting each attribute and specifying the **Minimum** and **Maximum** range of movement for that axis in the **Parameter Properties**. These values should be as realistic as possible, depending on the complexity and type of character. Defining this data is necessary for the accuracy and quality of the ML Deformer training process. The plugin will automatically initialize the values to the joint limits that are configured in Maya, if they are set up for that joint. You can also provide defaults for given parameter types.

![set minimum and maximum rotation values -45 and 45](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a893b006-c36a-4283-a8d2-db92ef4d8c9b/boneconfigure1.png)

Correctly configuring these parameters can be time consuming, so we recommend you save your progress as a `.json` file by clicking **File > Save Config**.

![save config using file save config](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25e9d79c-3c2c-4a4d-9e69-5c3f9db7b41d/boneconfigure2.png)

You can restore a saved configuration by selecting **File > Load Config**. Configuration files are based on node and attribute names, and can be used in any Maya scene with matching names.

### Configure Mesh

To finalize the training data, you must specify a **Base Mesh**, and optionally a **Target Mesh**.

The **Base Mesh** is the mesh bound to the skeleton, and is the same as the Skeletal Mesh asset used throughout Unreal Engine and will use linear skinning.

The **Target Mesh** is a separate mesh that contains the same vertices and topology as the Base Mesh, but is used for deformation. For example, the Target Mesh might use volume preservation techniques and muscle simulation to create realistic deformation. The target mesh can exist inside Maya, or it can be created in an external program such as Houdini. The Target Mesh is exported as an alembic cache `.abc`.

To specify your Base and Target Meshes, click **Add (+)** in the **Mesh Settings** area. A window will appear where you can click the **Select** button and specify each mesh, with the Target Mesh being optional unless you have it in your scene.

![select base mesh using add button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/568d87b5-989b-40ff-91f7-249a97d5d1da/configuremesh1.png)

Select your meshes and click **OK** to add them to the Mesh Settings list.

![select base lod 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09dd2fc6-4272-4b0e-88ad-5dd22e526873/configuremesh2.png)

If your Skeletal Mesh is composed of multiple meshes, you should add each individual mesh to the Mesh Settings list. Typically you would only need to do this if you are using [modular characters](/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine).

### Start Pose Generation

Lastly, you must specify **Generator Settings** to determine the training length and configuration. A keyframe will be created for every attribute in the parameter list, for each **Num Poses**.

![select generator settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64fc9500-88ac-4eed-a7a3-61f5ea095005/generator.png)

| Name | Description |
| --- | --- |
| **Num Poses** | 
The number of random poses to create, which creates animation for those frames. The recommended range is **5,000 - 25,000**, however in typical cases you can set this to **15,000**.

Training requires a large amount of data to give good results. Approximately 15,000 frames of animation data is expected to correspond with the default training settings in Unreal. Although it is possible to train with smaller data sets, the results are likely to be worse. The higher the Num Poses value, the slower the training will be. You might want to start with smaller values like 5000 to see if you already get good results.



 |
| **Start Frame** | The frame number where the randomly generated poses will start. You can combine existing animation data with the generated frames by setting a value greater than 0. |
| **Active Parameters** | The amount of randomness of the pose between each frame. In most cases, you should set this to around **75%**, with higher values resulting in better quality. Setting this to **100%** can cause simulation issues, however. A value of 100 means that every attribute in the parameter list will be randomized every frame, where a value of 40 means that only 40% of the parameters are randomized per frame. |

Click **Generate** to start the training data generation process in Maya. If you are using a **Target Mesh** and **Target Alembic File**, then this process can take a very long time. Make sure you also have enough free disk space, as the Alembic file can become very large (around 50 to 100 gigabytes), depending on the vertex count and Num Poses setting.

![generate mesh deformations using generate button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fca13a5a-09d9-4371-ac89-f4ee3c03dc72/generate.png)

Once the training data is finished generating, you should now have an exported `.fbx` and `.abc` file if you specified a **Target Alembic File**.

![finished generating training data files saved to local computer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f218f40-2e00-4ba2-995d-39401136afe8/generate2.png)

Your FBX and Alembic files must contain the same number of frames, and each frame must correspond to the same skeletal pose.

## ML Deformer Asset Setup in Unreal Engine

You can now bring your completed training files into Unreal Engine.

### Import Alembic File

Start by importing the `.abc` file that you either created in the training process, or in a different external deformer tool. In the **Content Browser**, click **Import**, then select your `.abc` file and click **Open**.

![import alembic file to unreal engine using the import button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c014722d-7c11-4a6c-add7-aa9070abf11b/importabc1.png)

In the import settings dialog window, set the following parameters for the import:

-   Set **Import Type** to **Geometry Cache**.
    
-   **Disable Flatten Tracks**. This is required in order to match FBX meshes with the Alembic Geometry Cache tracks. If you have just a single mesh, you can keep Flatten Tracks enabled, but are not required to do so. It is important that your Alembic Track names start with the same name as the name you see in the outliner in Maya.
    
-   Set **Compressed Position Precision** to **0.001** to ensure greater accuracy. If you keep the default, the ML Deformer may learn errors introduced by compression.
    
-   **Enable Store Imported Vertex Numbers**. This is required in order to match vertices between the Skeletal Mesh and the Geometry Cache. If you forget to do this the ML Deformer editor will show you a warning, and you will have to re-import the Geometry Cache again.
    

![set alembic cache import option in unreal engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86dd94f8-c3ed-45b5-84c6-e0362b76d810/importabc2.png)

Once these parameters are set, click **Import** to import the geometry cache. This process can take a very long time due to the size of the alembic file.

### Import Trained FBX

Next, you will need to import the FBX file that was created from the Maya training data. In the **FBX Import Options** dialog window, set the following parameters for the import:

-   If you have already imported your character into Unreal Engine, set the **Skeleton** field to use the skeleton of the character.
    
-   **Enable Import Animations**.
    
-   Set **Animation Length** to **Exported Time**.
    

![set fbx import option in unreal engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81c01545-55e6-4caf-bb6c-f172b962f556/importfbx1.png)

Once these parameters are set, click **Import** to import the FBX. This process can take a very long time due to the size of the FBX file.

### Create ML Deformer Asset

Next, you must create the **ML Deformer Asset** in order to contain and correlate both the Alembic and FBX sequences. In the **Content Browser**, use **Add (+)** to select **Animation > Deformers > ML Deformer**. **Name** and open the asset.

![create ml deformer asset using add animation deformers ml deformer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8f91088-4153-42fd-b515-af2c562aa905/mlasset1.png)

After opening the ML Deformer asset, you can select the data model for the asset that is used to train your character's mesh deformations. The model selected will have the most substantial impact on your final results.

| ML Deformer Model | Description |
| --- | --- |
| **Neural Morph Model** (**NMM**) | 
This model works best when working with flesh-like meshes and general deformation such as volume preserving deformation or other correctives. It is recommended to use this model by default.



 |
| **Nearest Neighbor Model** (**NNM**) | 

This model is designed to work best for cloth deformations.

For more information about the Nearest Neighbor Model, see the [Nearest Neighbor Mode EDC blog post](https://dev.epicgames.com/community/learning/tutorials/2lJy/unreal-engine-nearest-neighbor-model).



 |
| **Vertex Delta Model** (**VDM**) | 

This model is an example model that you can use to learn how to create your own deformer model.

This model should not be used in production.



 |

Make sure the **Neural Morph Model** is selected, using the drop down menu, and ensure the ML Defromer Mode is set to **Training**.

![select the neural morph model and training modes for the ml deformer asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f13a979-2126-463c-89b4-e7a7060be6fd/selectmodes.png)

In the **Details** panel of the **ML Deformer Editor**, assign both the Skeletal Mesh of your character and the imported trained FBX Animation Sequence to their respective properties. This will cause the mesh to appear under the **Training Base** viewport label.

![select skeletal mesh and generated animation sequence in the ml deformer assets details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f60f253d-d0b8-432b-a499-d9b95b845a71/mlasset2.png)

Also assign the imported Geometry Cache asset from the Alembic file to the **Geometry Cache** property. This will cause the target mesh to also appear in the viewport under the Training Target label.

![select geometry cache asset in the ml deformer assets details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66738a8e-a237-4b96-a0af-4e028265aaa9/mlasset3.png)

A green debug render will appear over the Training Base model's mesh. This render represents the deltas, or differences, between the base and target mesh. Ensure the render looks correct, as the deformer model will learn from these deltas during training. If your target mesh is rotated or otherwise offset from to your training base, you can use the **Alignment Transform** to align them. They do not need to overlap, only the rotation and scale needs to match.

Dragging on the timeline playhead will scrub both sequences together, so that you can verify their animation poses are matching. Make sure the green debug render (deltas) looks correct every frame that you preview.

![scrubbing animation sequence with training base and training mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77b4cbe4-95c4-44e6-85e2-1505f5d293be/mlasset4.gif)

## Training the Mesh Deformation

After creating and setting up the ML Deformer asset with the Neural Morph Model training data model, you can set up inputs to influence and control the results of the trained mesh deformations.

### Set Inputs and Outputs

Using the **Inputs and Outputs** section of the ML Deformer asset's **Details** panel, you can specify bones or curves from the mesh's Skeleton you want to reference to better train the model. The ML Deformer will use the rotations of the selected bones, or the deltas of the curves, to learn how to deform the mesh.

When using bone inputs, it is recommended to exclude **twist** and **roll** rotations as well as other helper bones from the training. Additionally, deformation training only uses the specified bone's rotation values, so bone **translation** or **scale** data does not influence training results. Your skeleton can still contain those kinds of helper bones in areas where the ML Deformer has a hard time approximating the target deformation.

You can manually assign bones in the **Bone Include List** property using (**+**) Add, and selecting bones using the drop down menu.

Alternatively you can use the **Animated Bones Only** button to automatically populate the Bone Include List property with all of the Skeletal Mesh's bones that contain animation data.

![select animated bones in the ml deformer assets details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fa6abda-b840-4c14-8559-f370036c3686/animatedbonesonly.png)

However, if you do not remove any bones from the automatically generated list, all bones in the skeleton will be used as inputs. Generally, this does not result in the best deformation results, so it is recommended that you only designate the minimum set of bones on which your deformation depends.

For example, you may want to exclude the finger bones from the **Bone Include List**, in order to not perform complex mesh deformations of the hands. Complex deformations on smaller parts of the body, such as hands or feet, have little effect on the overall results of the mesh's appearance, and can be computationally and resource expensive. Linear skinning is still performed on the mesh in conjunction with the ML Deformer, so bones excluded from the Bone Include List will still deform as usual.

Similar to bone inputs, you can also provide a set of input [curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) to influence the mesh deformation training. Using Curves you are able to influence the deformation training using data other than bone rotations. For example, curves can be useful when dealing with facial animations, where a curve value is used to control how open or closed an eye-lid is, or how much the left inner eyebrow is raised.

### Set Bone and Curve Groups

The **Local Mode** of the Neural Morph Model primarily looks at deformations caused by individual bones. This can cause some issues when deformations in certain parts of the mesh depend on the multiple bones or curves. For example, the area on the back of a character could be influenced by both left and right clavicle bones.

To accommodate for this, the Neural Morph Model in Local Mode supports the use of **Bone Groups** and **Curve Groups**. You can use these groups to create sets of bones or curves that work together to create a more realistic deformation. For example, when creating a Bone Group to accommodate for a character's clavicle, you can use (**+**) **Add** to create a new bone group and select the **Upper Arm** and **Spine** bones using the drop down menu.

Here is an example image showing a bone group that consists of the left and right thigh bones.

![example bone group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cc49f1b-6961-4464-ba83-54a7f6988450/examplebonegroup.png)

Each bone or curve group generates the same number of morph targets as defined by the **Num Morph Targets Per Bone/Curve** property.

### Train the Model

In the ML Deformer Editor's **Details** panel, set the Training Settings's Mode property to **Local**.

By default the Mode property will be set to Local when creating a new ML Deformer asset using the Neural Morph Model.

![set the training mode to local in the detail panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d50affd6-6556-438c-9204-7ab0f29616ff/localmode.png)

The Training Settings **Mode** can drastically change the way the deformer operates and what types of deformation can be used. When training a deformer model you can select from the following modes:

| Training Settings Mode | Description |
| --- | --- |
| **Local** | 
This mode is optimized to learn deformations around individual joints, and requires the least amount of training data. This option should be used by default unless you encounter difficulty reconstructing the training data.

Each bone or curve will create a set of morph targets in this model. The total number of morph targets generated will be: `(num_bones + num_bone_groups) * num_morphs_per_bone_or_curve + (num_curves + num_curve_groups) * num_morphs_per_bone_or_curve + 1` The `+ 1` at the end is just one morph target that is always created and is used for normalization of the data. This is always the first morph target in the list of generated morph targets.

The Local mode can handle structured data, such as structured ROM's better than the **Global** mode.



 |
| **Global** | 

This mode learns deformation from coordinated movement of multiple joints, but requires more training data.

This mode acts similar to the Local mode, but acts like all bones are in one big bone group. This works best with randomized poses as training data.



 |

After setting the Training Settings Mode, select the **Train Model** button in the ML Deformer Editor toolbar to start training.

Depending on the complexity of your mesh and training data, this process can take a long time.

![use the train model button to train the ml deformer asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbcbb28a-9de0-4add-864c-5bf6ac5d46b3/mlasset5.png)

After the training process of the model is complete, you can use the properties contained within the ML Deformer asset's **Compression** settings, located in the **Details** panel, to reduce the overall memory usage and improve the performance of the deformer asset.

![set the ml deformer compression settings in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5a13ea8-4da0-4524-8054-32a79124307e/compressionsettings.png)

Here you can reference a list of the Compression settings, and a description of their functionality:

| Property | Description |
| --- | --- |
| **Delta Zero Threshold** | 
You can use this property to set a threshold, in centimeters (**cm**) to ignore deltas with a length below the set value. These small deltas may not have a large impact on the visual deformation quality, when training the model. The set value will remove all deltas with a length smaller than the given value, and can significantly reduce the amount of memory required as well as increasing GPU performance of your project. Higher values will cause more deltas to be removed, while smaller values will ignore fewer deltas. A value of 0 will use all deltas, so will give the maximum quality, but also using the most amount of memory and with the slowest performance. It is recommended to increase this value as much as possible while retaining the visual fidelity of your deformation goals.

Setting a functional value for this property will have one of the most significant effects on the runtime performance and memory of your project when using ML Deformer assets.



 |
| **Compression Level** | 

You can use this property to compress the ML Deformer asset's deltas. Higher values will result in better compression, but also lower the quality. It is recommended to increase this value as much as possible while retaining the visual quality of your deformation goals.

It is good practice to first adequately set the **Delta Zero Threshold** property for your project, before tweaking the Compression Level property.



 |

You can monitor the results of your compression settings by navigating in the ML Deformer Editor's **Details panel** to the **Statistics** property section.

![monitor the ml deformers memory usage in the statistics panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddc832b6-2c9a-4460-ba7b-6fba44e0c0ef/memoryusage.png)

The **CPU Performance**, **Model - Cooked**, and **GPU Memory** Statistics, give insights into your ML Deformer asset' s performance in game. Here you can reference a list of the available **Memory** and **Performance** statistics relevant to the ML Deformer asset, and a description of their functionality:

Listed values are estimates, actual values can vary.

| Statistic | Description |
| --- | --- |
| **CPU Performance** | Here you can reference the CPU performance in microseconds (**μs**), so for example, a value of `100` means `0.1` milliseconds. However, most computation time will occur on the GPU and can be viewed in the **GPU Memory** (**Morph Targets**) property or using [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) using the **Morph Targets** category. |
| **Main Memory** | 
-   **Model - Cooked**: Displays the estimated amount of memory, in megabytes (**mb**), that the ML Deformer model is using when cooked.
-   **Model - In Editor**: Displays the estimated amount of memory, in megabytes (**mb**), that the ML Deformer model is using in the editor.



 |
| **GPU Memory** (**Morph Targets**) | Displays the amount of video memory, in megabytes (**mb**), the ML Deformer model is using on the GPU at runtime. When monitoring your ML Deformer's memory usage, this statistic is the most consequential. |

After the training process is complete you can view the results in the ML Deformer's **Testing** mode.

![view the ml deformer results using the testing mode in the toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db3ddbec-fa21-434a-94b0-c98b003b02d8/testing.png)

You can adjust the **Weight** property in the **Visualization** panel to observe the effect of the ML Deformer mesh (right) compared to the linear skinned mesh (left).

![set weight to view ml deformer results in the visualization panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c563dfd0-843f-443d-8f70-fb8b9f94670f/weight.gif)

Enable the **Show Heat Map** property and adjust the Heat Map options in the **Visualization** panel to see a visual representation of the areas of the mesh being deformed by the ML Deformer.

![use the heat map properties to view results in the visualization panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e7d4a84-aad4-405c-b54a-2155143d9ae9/heat.png)

## Deformer Blueprint Setup

In order to start using the ML Deformer on a character in a level, you will need to set up the character using the **ML Deformer Component** in Blueprints.

Start by creating an **Actor Blueprint**. In the **Content Browser**, click **Add (+)** \> **Blueprint Class**, then select **Actor**. Open the Blueprint after it is created.

![create a new blueprint actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/afa24277-9798-47a4-bb2e-3f8956201509/blueprintsetup1.png)

Add your Skeletal Mesh to the Blueprint by dragging it from the Content Browser into the **Components** panel.

![add skeletal mesh to actor blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f88ae9b1-46c8-4047-930a-b216bfbbd048/blueprintsetup2.png)

Next, add the **MLDeformer Component** by clicking **Add (+)** in the **Components** panel and selecting **MLDeformer**.

![add ml deformer component to actor blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/577e4234-d0ed-41da-823f-c582538e3a61/blueprintsetup3.png)

Select the **MLDeformer Component** and specify your **ML Deformer Asset** in the **Details** panel.

![add ml deformer asset to ml deformer component in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3787180-6693-4b22-a77b-7d02b245b7b1/blueprintsetup4.png)

Lastly, select the **Skeletal Mesh Component** and specify a **Deformer Graph** in the **Mesh Deformer** property.

![add ml deformer graph to the skeletal mesh component in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d45c9f6-7597-41aa-8266-2250b2b33a4f/blueprintsetup5.png)

If you do not have a Deformer Graph, you can use the example **DefaultMLDeformerGraph** located in the **Engine > Plugins > MLDeformer Content > Deformers** content folder. To access this folder, click on **Settings** in the Content Browser and enable both **Show Engine Content** and **Show Plugin Content**.

![set content browser filter to show engine content and show plugin content](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c6af14c-c4bc-4aa1-a4e1-e37186044bb8/blueprintsetup6.png)

## More Information

See the following resource for more information about the ML Defoamer system in Unreal Engine.

### ML Deformer Framework

For a more comprehensive overview and reference of the ML Deformer Framework, Editor, and ML Deformer Models, see the following documentation:

### ML Deformer Example Project

For an interactive example project, that you can use to observe how different models and edits affect the ML Deformer's mesh deformations of a MetaHuman, see the [ML Deformer Sample Project](https://unrealengine-gamedev.ol.epicgames.net/marketplace/en-US/product/ml-deformer-sample).

### Nearest Neighbor Resources

For more information about the experimental Nearest Neighbor ML Deformer training model, see the [Nearest Neighbor Mode EDC blog post](https://dev.epicgames.com/community/learning/tutorials/2lJy/unreal-engine-nearest-neighbor-model).

### Game Developers Conference ML Deformer Demo

To learn more about the ML Deformer system and see a live demo, showcasing the capabilities and functionality of the ML Deformer, see the [State of Unreal | GDC 2023](https://www.youtube.com/live/teTroOAGZjM?feature=share&t=19000) talk.