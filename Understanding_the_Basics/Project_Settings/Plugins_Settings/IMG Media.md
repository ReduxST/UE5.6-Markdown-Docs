# IMG Media

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/img-media-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/img-media-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:29:50

---

## IMG Media

### General

| **Setting** | **Description** |
| --- | --- |
| **Default Frame Rate** | 
Default frame rate to use if none was specified in image sequence or media source (default = 1/24). You can choose from the following options:

-   **12 fps (animation)**
-   **15 fps**
-   **24 fps (film)**
-   **25 fps (PAL/25)**
-   **30 fps**
-   **48 fps**
-   **50 fps (PAL/50)**
-   **60 fps**
-   **100 fps**
-   **120 fps**
-   **23.976 fps (NTSC/24)**
-   **29.97 fps (NTSC/30)**
-   **59.94 fps (NTSC/60)**
-   **Custom**



 |

### Caching

| **Setting** | **Description** |
| --- | --- |
| **Cache Behind Percentage** | Percentage of cache to use for frames behind the play head (default = 25%). |
| **Cache Size GB** | Maximum size of the look-ahead cache (in GB; default = 1 GB). |
| **Cache Threads** | Maximum number of image caching threads to use (0 = number of cores, default = 8). |
| **Global Cache Size GB** | 
Maximum size of the global look-ahead cache (in GB; default = 1 GB).

Must be greater or equal to `CacheSizeGB`.



 |
| **Use Global Cache** | If enabled, uses the global cache. |
| **Cache Thread Stack Size KB** | Size of the stack for each caching thread (in kB; default = 128). |

### EXR

| **Setting** | **Description** |
| --- | --- |
| **Exr Decoder Threads** | Number of worker threads to use when decoding EXR images (0 = auto). |

### Proxies

| **Setting** | **Description** |
| --- | --- |
| **Default Proxy** | 
Name of default media source proxy URLs (default = `proxy`).

Image sequence media sources may contain more than one media source URL. Additional URLs are called media source proxies, and they are generally used for switching to lower-resolution media content for improved performance during development and testing.

Each proxy URL has a name associated with it, such as `proxy`, `lowres`, or any other user-defined tag. It is up to the media source to interpret this value and map it to a media source URL. For example, a media source consisting of a sequence of uncompressed images may use a proxy name as the name of the sub-directory that contains proxy content, such as low-res version of the image sequence.

When default proxies are enabled via the `UseDefaultProxy` setting, media players will first try to locate the proxy content identified by the `DefaultProxy` tag. If no such proxy content is available, they will fall back to the media source's default URL.

See **Use Default Proxy** on this page.



 |
| **Use Default Proxy** | 

Defines whether to enable image sequence proxies (default = false).

Image sequence media sources may contain more than one media source URL. Additional URLs are called media source proxies, and they are generally used for switching to lower resolution media content for improved performance during development and testing.

Each proxy URL has a name associated with it, such as `proxy`, `lowres`, or any other user defined tag. It is up to the media source to interpret this value and map it to a media source URL. For example, a media source consisting of a sequence of uncompressed images may use a proxy name as the name of the sub-directory that contains proxy content, such as low-res version of the image sequence.

When default proxies are enabled via the `UseDefaultProxy` setting, media players will first try to locate the proxy content identified by the `DefaultProxy` tag. If no such proxy content is available, they will fall back to the media source's default URL.

See **Default Proxy** on this page.



 |