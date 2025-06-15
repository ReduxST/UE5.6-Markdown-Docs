# Setting Up a Project to use Grooms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-project-for-grooms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-project-for-grooms-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:05

---

Before you can start using grooms in your Unreal Engine projects, you'll first need to enable some project settings and plugins that help you import and render them.

## Project Settings

When you enable grooms for your project, a basic skinning system is embedded for forwarding skin deformation to the groom system. However, this system only supports bone-based deformation. To use more advanced skin deformation, such as morph targets and deformers, you'll want to enable the [Skin Cache](/documentation/en-us/unreal-engine/skeletal-mesh-rendering-paths-in-unreal-engine) system.

In the **Project Settings** under **Rendering > Optimizations**, you can enable the Skin Cache system by checking the box for **Support Compute Skin Cache**.

This setting requires the editor to be restarted.

![Groom Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ee3a4eb-4e36-4ff6-9669-f43f5be6f54a/grooms-project-settings.png)

## Groom Plugins

The **Plugins** browser includes required and optional plugins that support using grooms in your Unreal Engine projects. You can open it from the main menu under the **Edit** menu.

The following Groom plugins are available:

![Groom Plugins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a55f795b-27e8-4f33-bbb4-e62f81c897e0/groom-plugins-browser.png)

Enabling these plugins requires the editor to be restarted.

| Plugin Name | Description | Default Status |
| --- | --- | --- |
| Geometry |   |   |
| **Alembic Groom Importer** | Enables you to import Alembic (\*.abc) files that contain groom data sets into Unreal Engine. | Disabled |
| **Groom** | Enables rendering and simulation of imported grooms. | Disabled |
| \[Optional\] **Hair Card Generator** | Enables generation of cards from strands in your groom. You can configure parameters to determine how the cards are generated from your groom, which can also be used to generate different levels of detail. To learn more about how to generate groom cards, see [Groom Cards and Meshes](/documentation/en-us/unreal-engine/setting-up-cards-and-meshes-for-grooms-in-unreal-engine) | Disabled |
| Animation |   |   |
| \[Optional\] **Deformer Graph** | Enables deformation graphs that you can use to perform and customize mesh deformations for any skinned mesh. To learn more about how to use this with your grooms, see [Groom Deformer](/documentation/en-us/unreal-engine/setting-up-a-groom-deformer-graph-in-unreal-engine). | Enabled |