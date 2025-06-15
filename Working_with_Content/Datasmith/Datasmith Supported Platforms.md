# Datasmith Supported Platforms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-supported-platforms](https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-supported-platforms)  
**Processed:** 2025-06-14 16:19:04

---

This page describes which features of Datasmith work on which different platforms when you download Unreal Engine through the Epic Games Launcher, and when you build the engine yourself from its source code distribution.

## Supported File Formats by Platform

Some components used internally by the different Datasmith importers only work on selected Unreal Engine platforms.

| Source format | 64-bit Windows | Mac OS X | Linux |
| --- | --- | --- | --- |
| **.udatasmith files** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86e2ed4d-ac2f-40be-93f5-eec7c977018f/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/596117d6-e32f-4c88-ab0d-bbb7d2757596/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68cf064e-bb46-4497-a656-0cff0655c536/checkpoint_checked.png "Supported") |
| **CAD file formats** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d664144c-efec-4e70-b427-5f78b8f16443/checkpoint_checked.png "Supported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cbed263-83d1-45e4-b0d8-c8ec38149e93/checkpoint.png "Unsupported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b00c4b7-821d-4f2a-8ec3-086ba48782db/checkpoint_checked.png "Supported") |
| **Alias .wire** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89442f97-9d25-4ef5-9b78-580303da0b8f/checkpoint_checked.png "Supported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/637780ae-2e90-4ea7-b5c0-691b94f7fb93/checkpoint.png "Unsupported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9187276d-3f3a-4876-bf29-c797fe1bb83d/checkpoint.png "Unsupported") |
| **Rhino** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f40e0185-74ff-4552-bcae-b76c79fb8a57/checkpoint_checked.png "Supported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2128e74-0a18-40b9-815a-136d63393b72/checkpoint.png "Unsupported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a1e33dc-54c2-464b-98f3-72bb5824126e/checkpoint.png "Unsupported") |
| **Cinema 4D** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f0329e8-c144-4d03-9531-1b97aaabd59f/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7e1b697-0c96-48fb-8010-068d287f2312/checkpoint_checked.png "Supported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d66896f-6ab2-4c05-a140-bf3456eeaf69/checkpoint.png "Unsupported") |
| **AxF** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f25497fa-d692-48e6-b353-342cf3115f1a/checkpoint_checked.png "Supported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/633fc884-0912-4e24-8ce0-1ec95f281155/checkpoint.png "Unsupported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9efc7afb-7ea1-4642-856c-995609961e7a/checkpoint.png "Unsupported") |
| **MDL** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe0829c5-7073-4a15-bbd9-b2b1747f8336/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6592b01e-d56b-4753-be4f-f702bf003312/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/793475f2-eff1-42dd-88f7-9fd24781971d/checkpoint_checked.png "Supported") |
| **IFC** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79524ab2-ead9-42e0-89a9-a2ffe185ec35/checkpoint_checked.png "Supported") | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f176455c-31d7-42a1-a7db-add35c618963/checkpoint.png "Unsupported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89aa78b0-8630-4f76-978a-3b11d817c293/checkpoint_checked.png "Supported") |
| **Deltagen and VRED** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d756909e-db12-41ea-8532-e175ba71d858/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bec62036-1821-4e05-b49e-249715ec2b90/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7becb7e-1921-4418-9fb9-d0d49139b171/checkpoint_checked.png "Supported") |

## Rebuilding Unreal Engine from Source

Some components used internally by the Datasmith importers are not redistributable as part of the Unreal Engine source code. Therefore, you can't rebuild Unreal Engine yourself with support for the features provided by these components.

When you rebuild Unreal Engine yourself from its source code distribution, the Datasmith import plugins support the following formats:

| Source format | Rebuildable? |
| --- | --- |
| **.udatasmith files** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbf8ea5b-33e7-49be-a680-a83f9d346e94/checkpoint_checked.png "Supported") |
| **CAD file formats** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6db99aa-62b0-4248-a58f-3c81ef4d0482/checkpoint.png "Unsupported") |
| **Alias .wire** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f794cbf-8fdb-482e-ad57-12ef2b42364a/checkpoint.png "Unsupported") |
| **Rhino** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1ba3e1a-8cfd-4fe5-a4c6-5f7b403d382e/checkpoint.png "Unsupported") |
| **Cinema 4D** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/147764bd-eb3d-4324-a465-b687a34723f1/checkpoint.png "Unsupported") |
| **AxF** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20d5e258-4b13-4adf-80de-39e87f2e6d6f/checkpoint.png "Unsupported") |
| **MDL** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3343f0ec-2fe6-47b0-ac6d-22c914f05008/checkpoint.png "Unsupported") |
| **IFC** | ![Unsupported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e135b9d-d4d7-463a-88da-1251427dae47/checkpoint.png "Unsupported") |
| **Deltagen and VRED** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3c615d3-769e-45b1-98d0-e2807aa67021/checkpoint_checked.png "Supported") |

You may be able to compile Unreal Engine with some of the unsupported features listed above if you download and install the required software development kits from third parties.

Support for gITF is now native to UE.

## Datasmith Export Plugins

The pre-built versions of the Datasmith Exporter Plugins on the [Datasmith export plugins](https://www.unrealengine.com/en-US/datasmith/plugins) download page support the following platforms:

| Source application | 64-bit Windows | Mac OS X |
| --- | --- | --- |
| **SketchUp Pro** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89c35fb8-b5bc-4ff3-a279-c76d60bbc1f5/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fccf827-d948-467c-81f2-dc9b4985c7d9/checkpoint_checked.png "Supported") |
| **3ds Max** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da7bcbe-4bb5-4ff8-9d40-6e5ae2c14bda/checkpoint_checked.png "Supported") | n/a \* |
| **Revit** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/983ab030-bcc9-419a-ac10-aa0ca6ab9871/checkpoint_checked.png "Supported")\*\* | n/a \* |
| **Navisworks** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29fe350f-8b61-4064-a811-310b6aeab019/checkpoint_checked.png "Supported") | n/a \* |
| **Rhino** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aed1e30-7394-4255-b9e3-4252631394c5/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fe5ad84-7f88-48e0-8677-93666f1222c4/checkpoint_checked.png "Supported") |
| **Archicad** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bb24a00-0a60-403f-9080-4181b55e1fbe/checkpoint_checked.png "Supported") | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1613c6c4-05d2-41c4-b089-0e119c4c2562/checkpoint_checked.png "Supported") |
| **Solidworks** | ![Supported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f81c8a7-4ad2-41ef-a14d-6edab890bf5a/checkpoint_checked.png "Supported") | n/a \* |

\* Not available on macOS.

\*\* As of Unreal Engine 5.3, Autodesk now manages newer versions of the Revit exporter plugin and is shipped directly in Revit 2024+. UE still supports this plugin and you can get older versions of the plugin from the download page.

When you rebuild Unreal Engine yourself from its source code distribution, you can rebuild the Datasmith Exporter Plugins for Windows. However, you need to download and install the SDK for your source application from [Trimble](https://extensions.sketchup.com/en/developer_center/sketchup_sdk) or [Autodesk](https://www.autodesk.com/developer-network/overview).