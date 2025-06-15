# Known Limitations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/known-limitations-of-containers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/known-limitations-of-containers-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:00

---

Official support for containers in Unreal Engine is still in Beta and is subject to a number of limitations.

## Windows Development Images

The container images that are included with Unreal Engine currently only include Linux development images and not Windows development images. This is due to both technical and legal limitations that currently prevent us from distributing Windows development images.

For a discussion on the technical issues that affect Windows development images, see the blog post [Preview the future of the ue4-docker project](https://adamrehn.com/articles/preview-the-future-of-ue4-docker/) by Adam Rehn.

## Support for AMD GPUs in Container-Based Pixel Streaming

Windows runtime images that support [Pixel Streaming](/documentation/en-us/unreal-engine/pixel-streaming-in-unreal-engine) support GPU acceleration with both NVIDIA and AMD GPUs. Linux images only support NVIDIA GPUs, but support for AMD GPUs is planned for a future release.