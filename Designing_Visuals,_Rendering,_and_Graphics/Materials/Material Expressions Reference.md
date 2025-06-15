# Material Expressions Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference)  
**Processed:** 2025-06-14 16:56:51

---

This page is a reference index for all **Material expression** nodes available in the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide). Material Expressions are the building blocks for creating fully functional Materials in Unreal Engine.

Each Material expression is a self-contained black box that either outputs a set of one or more specific values, or performs a single operation on one or more inputs and then outputs the results of that operation.

## Parameters

Certain Material expressions are parameters, meaning you can modify their values (dynamically during runtime in some cases) in a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) of the base material containing the parameter.

You should assign all parameters a unique name using the **Parameter Name** details property. This name is used to identify each specific parameter when you edit an instance in the [Material Instance Editor](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui).

If two parameters of the same type have the same name within a Material, they are treated as the same parameter. Changing the value of one parameter in the Material Instance would change the value of both parameter expressions in the Material. You can set a default value for your parameters in the Details Panel. This default value is used in the Material Instance unless it is overridden and modified there.

## Material Expression Properties

All Material Expression nodes contain the same properties that provide different kinds of information. Below, we use a Texture Sample node to highlight these on properties.

![Material Expression breakdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3074e534-51cc-4eff-ab1b-bcecee78b539/multiply-node.png)

| Number | Property Name | Description |
| --- | --- | --- |
| 1 | Description | All materials expressions have a common **Desc** (Description) property, which is accessible from the Details Panel. Any text entered into this in this property displays in the Material Editor just above the expression in the workspace. It can be used for any purpose, but usually serves as a good way to leave short notes about the purpose or function of the expression. |
| 2 | Title bar | Displays the name and/or pertinent information about the the Material Expression. |
| 3 | Inputs | Links to any values used by the Material Expression. |
| 4 | Outputs | Links that output the results of the Material Expression operation. |
| 5 | Preview | Displays a preview of the values that are output by the Material Expression. This updates automatically when realtime update is enabled and can be manually updated using the Spacebar. |

### Material Expression Types

These reference pages are organized according to the categories in the Material Editor palette.

## Expression Index

This is a reference list of many, but not all, Material Expressions. All links shown here can also be accessed through the Expression Types pages listed above. Additionally, you can use **Ctrl+F** to find the expression node you need and follow the link to its description.

[**Atmosphere**](/documentation/en-us/unreal-engine/atmosphere-material-expressions-in-unreal-engine)

-   [AtmosphericFogColor](/documentation/en-us/unreal-engine/atmosphere-material-expressions-in-unreal-engine#atmosphericfogcolor)

[**Color**](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine)

-   [Desaturation](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#desaturation)

[**Constants**](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine)

-   [Constant](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#constant)
-   [Constant2Vector](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#constant2vector)
-   [Constant3Vector](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#constant3vector)
-   [Constant4Vector](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#constant4vector)
-   [DistanceCullFade](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#distancecullfade)
-   [PerInstanceFadeAmount](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#perinstancefadeamount)
-   [PerInstanceRandom](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#perinstancerandom)
-   [Time](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#time)
-   [TwoSidedSign](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#twosidedsign)
-   [VertexColor](/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine#vertexcolor)

[**Coordinates**](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine)

-   [ActorPositionWS](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#actorpositionws)
-   [CameraPositionWS](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#camerapositionws)
-   [LightmapUVs](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#lightmapuvs)
-   [ObjectOrientation](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#objectorientation)
-   [ObjectPositionWS](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#objectpositionws)
-   [ObjectRadius](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#objectradius)
-   [Panner](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#panner)
-   [ParticlePositionWS](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#particlepositionws)
-   [PixelNormalWS](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#pixelnormalws)
-   [Rotator](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#rotator)
-   [SceneTexelSize](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#scenetexelsize)
-   [ScreenPosition](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#screenposition)
-   [TextureCoordinate](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#texturecoordinate)
-   [VertexNormalWS](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#vertexnormalws)
-   [ViewSize](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#viewsize)
-   [WorldPosition](/documentation/en-us/unreal-engine/coordinates-material-expressions-in-unreal-engine#worldposition)

[**Custom**](/documentation/en-us/unreal-engine/custom-material-expressions-in-unreal-engine)

-   [Custom](/documentation/en-us/unreal-engine/custom-material-expressions-in-unreal-engine)

[**Depth**](/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine)

-   [DepthFade](/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine#depthfade)
-   [PixelDepth](/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine#pixeldepth)
-   [SceneDepth](/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine#scenedepth)

[**Font**](/documentation/en-us/unreal-engine/font-material-expressions-in-unreal-engine)

-   [FontSample](/documentation/en-us/unreal-engine/font-material-expressions-in-unreal-engine#fontsample)
-   [FontSampleParameter](/documentation/en-us/unreal-engine/font-material-expressions-in-unreal-engine#fontsampleparameter)

[**Functions**](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine)

-   [FunctionInput](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine#functioninput)
-   [FunctionOutput](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine#functionoutput)
-   [MaterialFunctionCall](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine#materialfunctioncall)
-   [StaticBool](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine#staticbool)
-   [StaticSwitch](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine#staticswitch)
-   [TextureObject](/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine#textureobject)

[**MaterialAttributes**](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine)

-   [BreakMaterialAttributes](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine#breakmaterialattributes)
-   [MakeMaterialAttributes](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine#makematerialattributes)

[**Math**](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine)

-   [Abs](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#abs)
-   [Add](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#add)
-   [AppendVector](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#appendvector)
-   [Ceil](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#ceil)
-   [Clamp](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#clamp)
-   [ComponentMask](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#componentmask)
-   [Cosine](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#cosine)
-   [CrossProduct](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#crossproduct)
-   [Divide](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#divide)
-   [DotProduct](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#dotproduct)
-   [Floor](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#floor)
-   [Fmod](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#fmod)
-   [Frac](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#frac)
-   [If](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#if)
-   [LinearInterpolate](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#linearinterpolate)
-   [Multiply](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#multiply)
-   [Normalize](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#normalize)
-   [OneMinus](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#oneminus)
-   [Power](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#power)
-   [Sine](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#sine)
-   [SquareRoot](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#squareroot)
-   [Subtract](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine#subtract)

[**Parameters**](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine)

-   [CollectionParameters](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#collectionparameters)
-   [DynamicParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#dynamicparameter)
-   [FontSampleParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#fontsampleparameter)
-   [ScalarParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#scalarparameter)
-   [StaticBoolParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#staticboolparameter)
-   [StaticSwitchParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#staticswitchparameter)
-   [StaticComponentMaskParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#staticcomponentmaskparameter)
-   [VectorParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#vectorparameter)
-   [TextureObjectParameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#textureobjectparameter)
-   [TextureSampleParameter2D](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#texturesampleparameter2d)
-   [TextureSampleParameterSubUV](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#texturesampleparametersubuv)
-   [TextureSampleParameterCube](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#texturesampleparametercube)
-   [TextureSampleParameterMovie](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#texturesampleparametermovie)

[**Particles**](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine)

-   [DynamicParameter](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#dynamicparameter)
-   [ParticleColor](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlecolor)
-   [ParticleDirection](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particledirection)
-   [ParticleMacroUV](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlemacrouv)
-   [ParticleMotionBlurFade](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlemotionblurfade)
-   [ParticlePositionWS](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlepositionws)
-   [ParticleRadius](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particleradius)
-   [ParticleRelativeTime](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlerelativetime)
-   [ParticleSize](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlesize)
-   [ParticleSpeed](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlespeed)
-   [SphericalParticleOpacity](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#sphericalparticleopacity)
-   [ParticleSubUV](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#particlesubuv)
-   [TextureSampleParameterSubUV](/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine#texturesampleparametersubuv)

[**Terrain**](/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine)

-   [LandscapeLayerBlend](/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine#landscapelayerblend)
-   [LandscapeLayerCoords](/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine#landscapelayercoords)
-   [LandscapeLayerSwitch](/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine#landscapelayerswitch)

[**Texture**](/documentation/en-us/unreal-engine/texture-material-expressions-in-unreal-engine)

-   [FontSample](/documentation/en-us/unreal-engine/texture-material-expressions-in-unreal-engine#fontsample)
-   [FontSampleParameter](/documentation/en-us/unreal-engine/texture-material-expressions-in-unreal-engine#fontsampleparameter)
-   [SceneColor](/documentation/en-us/unreal-engine/texture-material-expressions-in-unreal-engine#scenecolor)
-   [TextureObject](/documentation/en-us/unreal-engine/texture-material-expressions-in-unreal-engine#textureobject)
-   [TextureSample](/documentation/en-us/unreal-engine/texture-material-expressions-in-unreal-engine#texturesample)

[**Utility**](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine)

-   [BlackBody](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#blackbody)
-   [BumpOffset](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#bumpoffset)
-   [ConstantBiasScale](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#constantbiasscale)
-   [DDX](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#ddx)
-   [DDY](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#ddy)
-   [DepthFade](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#depthfade)
-   [DepthOfFieldFunction](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#depthoffieldfunction)
-   [Desaturation](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#desaturation)
-   [Distance](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#distance)
-   [Fresnel](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#fresnel)
-   [LightmassReplace](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#lightmassreplace)
-   [LinearInterpolate](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#linearinterpolate)
-   [Noise](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#noise)
-   [QualitySwitch](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#qualityswitch)
-   [RotateAboutAxis](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#rotateaboutaxis)
-   [SphereMask](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#spheremask) \*[Thin Translucent](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#thintranslucent)
-   [AntialiasedTextureMask](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#antialiasedtexturemask)

[**VectorOps**](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine)

-   [AppendVector](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#appendvector)
-   [ComponentMask](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#componentmask)
-   [CrossProduct](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#crossproduct)
-   [DeriveNormalZ](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#derivenormalz)
-   [DotProduct](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#dotproduct)
-   [Normalize](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#normalize)
-   [Transform](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#transform)
-   [TransformPosition](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine#transformposition)

[**Vectors**](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine)

-   [ActorPositionWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#actorpositionws)
-   [CameraPositionWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#camerapositionws)
-   [CameraVectorWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#cameravectorws)
-   [Constant2Vector](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#constant2vector)
-   [Constant3Vector](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#constant3vector)
-   [Constant4Vector](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#constant4vector)
-   [LightVector](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#lightvector)
-   [ObjectBounds](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#objectbounds)
-   [ObjectOrientation](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#objectorientation)
-   [ObjectPositionWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#objectpositionws)
-   [ParticlePositionWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#particlepositionws)
-   [PixelNormalWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#pixelnormalws)
-   [ReflectionVectorWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#reflectionvectorws)
-   [VertexNormalWS](/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine#vertexnormalws)