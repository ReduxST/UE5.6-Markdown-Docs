# Georeferencing a Level

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/georeferencing-a-level-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/georeferencing-a-level-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:40

---

**Georeferencing** means to associate an environment with locations in physical space. The term is commonly used in the geographic information systems field to describe the process of associating a physical map or raster image of a map with spatial locations. Once the environment has been georeferenced, Unreal Engine can express actual geographic coordinates (such as latitude/longitude or UTM coordinates).

#### Prerequisites

-   The GeoReferencing plugin must be enabled to use the features described here.

## Theoretical Background

### Coordinate Reference Systems (CRS) and Ellipsoids

When it comes to locating objects on a planet, one must choose a Coordinate Reference System (CRS) to express the location.

What makes it complicated is that planets are neither planes nor spheres: they are ellipsoids. There are different ellipsoid models (called datums), the most well-known one being the WGS84 for Earth.

![ellipsoid 3D model, axes relation diagram, and formula](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61a8c92f-e349-4118-8ca0-82995b0cbe61/ellipsoid-math-references.png)

For example, with the WGS84 ellipsoid, there is an approximate 22km of difference between the lengths of the axes!

-   a = 6 378 137.0 m
-   b = 6 356 752.314 245 m
-   1/f = 298.257 223 563

Each Coordinate Reference System defines locations using the ellipsoid model it is based on. However, there are different kinds of CRS, each with additional properties.

### Geographic CRS

A geographic CRS uses polar coordinates to express the location of one point on the planet.

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea7ef69b-3925-47e2-9d0c-1c50aa5c3fd4/geographic-crs.png" alt="Geographic CRS representation" loading="lazy" width="600"></td><td><div><ul><li>Latitude = Elevation in degrees to the Equator</li><li>Longitude = Azimuth in degrees to the Prime Meridian (Greenwich)</li><li>Altitude = Height in meters to the reference ellipsoid.</li></ul><p>Angles are expressed in decimal degrees, or DMS (Degrees, Minutes, Seconds).</p></div></td></tr></tbody></table>

There are, in fact, two kinds of latitude definitions; when the datum is not a sphere, local normal to the ellipsoid model is involved, which makes for more complex calculations, but that is out of scope here.

### Geocentric CRS

A geocentric CRS uses Cartesian coordinates to define the location of any point on the planet, with the origin located at the planet center.

The following image shows the Earth-Centered, Earth-Fixed (ECEF) CRS, which is the standard reference CRS used in distributed simulation protocols such as DIS/HLA.

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cefb20e4-aea3-493c-89d0-978ddc25fd65/geocentric-crs.png" alt="Geocentric CRS representation" loading="lazy" width="600"></td><td><div><ul><li>Origin = Earth center</li><li>X Axis points to the Equator/Prime Meridian (Greenwich) intersection.</li><li>Z Axis aligns with the Earth's axis of rotation.</li><li>Y Axis is orthogonal to the former two axes.</li></ul><p>Coordinates are expressed in meters.</p></div></td></tr></tbody></table>

### Projected CRS

A projected coordinate system is a Geographic Coordinate System in which the planet has been "flattened" using a map projection. This is what we have always used when looking at paper maps. There are different ways to project a sphere to a plane, so there are lots of possible map projections, with more or less deformation, depending on the area mapped.

Most basic projections are using planar, conical or cylindrical shapes.

<table class="table" style="--columns-count: 3;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdaaef20-5679-44b0-9526-a83122a0e8e1/planar-projection-1.png" alt="" loading="lazy"></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04235fc5-8d37-4181-9258-05b4156b0798/cone-projection-1.png" alt="" loading="lazy"></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7115503d-42e5-44cd-ab09-d5cd5bc4dd80/cylinder-projection-1.png" alt="" loading="lazy"></td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba216c54-3868-44f8-ae5c-2c49e1678f38/planar-projection-2.png" alt="" loading="lazy"></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60309346-ff48-4cf6-a2a1-53f2cc14f684/cone-projection-2.png" alt="" loading="lazy"></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d5b30c4-3503-4f4c-9bca-c3e8cf2e864b/cylinder-projection-2.png" alt="" loading="lazy"></td></tr></tbody></table>

One of the most frequently used projections is the Mercator projection, which has several variants.

For instance, there is the Universal Transverse Mercator projection, widely used in the Simulation Industry. This CRS divides Earth into 60 parts, or *zones*, and projects each of these north / south-oriented zones using a cylindrical projection that is tangent to the central meridian of each zone.

![Earth showing meridian zones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a86d4682-40aa-42b1-b891-b781b3523c2c/image_1.png)![Cylinder mapping to earth for the projection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/259cb84a-c2ed-4915-98bc-730346b33829/image_2.png)

This is a Cartesian coordinate system, but in addition to the XYZ coordinates, it needs a Zone and Hemisphere identifier to define the origin. Specific assumptions are necessary to make sure all coordinates are positive.

Each 6°-wide UTM zone has a central meridian located by definition at X=500,000 meters. This central meridian is an arbitrary value convenient for avoiding any negative coordinates. All easting values will be greater than this central value, and all westing values will be lower, but all values will be positive.

If you're in the Northern Hemisphere, the equator has a northing value of 0 meters. In the Southern Hemisphere, the equator starts at 10,000,000 meters. This is because all values south of the equator will be subtracted from this value while being kept positive. This is called a false northing because y-coordinates in the Southern Hemisphere will avoid negative values.

There are derivatives of this system such as the Military Grid Reference System (MGRS).

### How to Describe a CRS

There are so many possible projection systems that conventions have been defined to declare their particular settings, such as Ellipsoid, Units, Meridians, Projections, and so on. This data can be saved in various formats, with the most-used being Well-Known-Text (WKT) and the European Petroleum Survey Group (EPSG) code.

Several websites, like [http://epsg.io/](http://epsg.io/), give information about each CRS, the details of which are outside the scope of this document.

It is very important to know the CRS that you want to use to convert coordinates to the right values.

### References

For more information about *geodesy* (the field of mathematics that deals with the shape and area of Earth), you can have a look at the following links.

-   CRS: [https://en.wikipedia.org/wiki/Geographic\_coordinate\_system](https://en.wikipedia.org/wiki/Geographic_coordinate_system)
-   Geographic CRS : [https://en.wikipedia.org/wiki/World\_Geodetic\_System#WGS84](https://en.wikipedia.org/wiki/World_Geodetic_System#WGS84)
-   ECEF: [https://en.wikipedia.org/wiki/ECEF](https://en.wikipedia.org/wiki/ECEF)
-   Mercator Projection : [https://en.wikipedia.org/wiki/Mercator\_projection](https://en.wikipedia.org/wiki/Mercator_projection)
-   UTM Projection: [https://en.wikipedia.org/wiki/Universal\_Transverse\_Mercator\_coordinate\_system](https://en.wikipedia.org/wiki/Universal_Transverse_Mercator_coordinate_system)
-   MGRS: [https://en.wikipedia.org/wiki/Military\_Grid\_Reference\_System](https://en.wikipedia.org/wiki/Military_Grid_Reference_System)

## Georeferencing Plugin

Unreal Engine comes with a **Georeferencing** plugin that you can use to define the level origin coordinates in one specific CRS, and provides functions to convert coordinates between each different CRS. In Unreal Engine, each **Actor** has coordinates defined relative to this level origin, so to know an arbitrary georeferenced location, you need to locate the engine origin on Earth.

Consider these two different cases:

-   **Flat Planet**: Your Unreal Engine environment is small enough to be approximated by a flat ground surface (smaller than some hundreds of km). In that case, you can model the ground in a *projected mode*, and define all coordinates in a projected CRS with one simple translation offset.
-   **Round Planet**: Your Unreal Engine environment is so big that you need to take into account the planet curvature (this is almost certainly the case if you are using the [Large World Coordinates](/documentation/en-us/unreal-engine/large-world-coordinates-in-unreal-engine-5) feature). In that case, your environment geometry can cover the whole planet, with a spherical or ellipsoidal shape. In this case, there are two ways to place your origin: at the center of the planet shape, or at any point on the surface. In the latter case, Unreal Engine assumes the Z-axis is pointing up, and normal to the ellipsoid at this point.

These cases can be illustrated by the image below.

-   On a Flat Planet, your environment is the green square. The modeling origin chosen for your level is the P point. It's an arbitrary location on the planet, and it can be defined using Geographic coordinates (latitude and longitude), or using Cartesian coordinates, but in a specific projected CRS. The XYZ coordinates are then represented within the CRS as east / north / up directions.
    
-   On a Round Planet, you have two different choices:
    
    -   Locate your Level origin at the planet center. This is the ECEF case, there is no geometry at the origin, but instead at coordinates with large values depending on the planet radius. The ECEF CRS is a Cartesian coordinate system, and its axes are aligned to the Unreal Engine axes.
    -   Locate your Level origin at an arbitrary point on the planet surface. As in the Flat Planet case, these coordinates can be expressed in a Geographic or Projected CRS. It is more convenient to keep the Up direction of the level aligned with the ellipsoid normal at this location, and make sure you orient the plane geometry in such a way that the Front and Right vectors are matching the North and East vectors.

![Flat plane mapped to a round planet](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/120025ce-64fa-40ac-a505-2cf17c4a1e8f/image_3.png)

In the geospatial industry, most coordinates are expressed in right-handed frames, but Unreal Engine uses a left-handed coordinate system. To remain consistent with geospatial usage, the Georeferencing plugin expresses coordinates using right-handed logic. This means that it inverts the Y coordinate at some point when converting coordinates (this is transparent to the end user).

For the Georeferencing plugin, we chose the following default axes conventions:

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7632e826-d2de-42fb-802c-0f26011c5e42/flat-coordinate-convention.png" alt="flat coordinate axes convention" loading="lazy" width="400"></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7cc9d5a-2595-40c4-895b-938dd7e92d2b/ecef-coordinate-convention.png" alt="ecef coordinate axes convention" loading="lazy" width="400"></td></tr><tr><td><p class="figure-caption is-separated">When the Unreal Engine Frame matches the Tangent Frame</p></td><td><p class="figure-caption is-separated">When the Unreal Engine Frame matches the ECEF Frame</p></td></tr></tbody></table>

If you prefer to use another convention, you will have to perform a coordinate swap before invoking the Georeferencing functions.

Unreal Engine automatically handles the World Origin offset shifting you activate when you use World Composition or when you perform a manual rebasing.

### Setting up the Georeferencing System

From the main menu, go to **Edit > Plugins**, then enable the **Georeferencing** plugin. Restart Unreal Engine.

![Georeferencing plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3afdc3f8-96a6-441e-ba56-c8bf8faad837/image_4.png)

Once enabled, you can use this plugin to convert coordinates between four systems:

-   The Unreal Engine coordinate system
-   A Projected CRS of your choice
-   A Geographic CRS of your choice
-   The standard ECEF CRS

From the **Place Actors** panel, find the **Geo Referencing System Actor**, drag it into your level, then select it to view its properties in the **Details** panel.

![Geo Referencing System Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cd49e4e-d519-4c0f-b123-f6891f18ad22/image_5.png)

#### Geo Referencing

| Property | Description |
| --- | --- |
| Planet Shape | Flat or Round. This depends only on your project geometry shape/scale. |
| Projected CRS | Identified by a string. This can be any CRS supported by the PROJ library. Refer to the [https://epsg.io/](https://epsg.io/) website to find appropriate CRS definitions. |
| Geographic CRS | Identified by a string. This can be any CRS supported by the PROJ library. Refer to the [https://epsg.io/](https://epsg.io/) website to find appropriate CRS definitions. |

#### Origin Location

| Property | Description |
| --- | --- |
| Origin Location in Projected CRS | Determines whether the Origin is defined using the Projected or the Geographic CRS coordinates. |
| Origin at Planet Center | Round Planet only. Determines whether the origin is defined as the planet center. |
| Origin Projected Coordinates Easting | Origin east-west coordinate when using Projected CRS coordinates. |
| Origin Projected Coordinates Northing | Origin north-south coordinate when using Projected CRS coordinates. |
| Origin Projected Coordinates Up | Origin up-down coordinate when using Projected CRS coordinates. |
| Origin Latitude | Origin north-south coordinate when using Geographic CRS coordinates. |
| Origin Longitude | Origin east-west coordinate when using Geographic CRS coordinates. |
| Origin Altitude | Origin up-down coordinate when using Geographic CRS coordinates. |

Using invalid strings for the CRS projection identifications will generate an error message. Make sure you are using a correct CRS definition as defined on [https://epsg.io/](https://epsg.io/).

![Editor error message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc30426e-5955-4799-8633-334b7464f7e3/crs-error-1.png) ![Log error message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff03b240-72c9-4257-85fd-c33957697a29/crs-error-2.png) 

In the screenshot below, the geometry is flat, then modeled in a projected CRS. The EPSG Code 32617 is for UTM North Zone 17, and the coordinates correspond to a location near Epic Games HQ. EPSG:4326 is the WGS84 ellipsoid, meaning that all geographic coordinates in latitude, longitude, and altitude will be defined in relation accordingly.

![Origin Location in Projected CRS enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb29bbae-90a0-4f6d-abef-1b98b47afbd8/image_6.png)![Origin Location in Projected CRS disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c820adc-687a-45f1-a518-2ddca6dd05a0/image_7.png)

For floating point accuracy reasons, these origin values have to be integers to avoid bad roundings. Consider this constraint when modeling your environment. Internally, the Georeferencing plugin does all its computations in double precision to maintain accuracy at any planet location.

When **Round Planet** is selected, an extra checkbox is displayed to set up your origin location.

-   If you check **Origin at Planet Center**, it means that you are using the ECEF case. The origin is explicitly defined at the planet center as [described previously](/documentation/en-us/unreal-engine/georeferencing-a-level-in-unreal-engine#planetcases), and no further information is required.
-   Otherwise, you can set the **Level Origin** at an arbitrary location on the ellipsoid using the CRS of your choice.

![Origin at Planet Center enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff50e8ec-4ba5-4484-bf84-349df34cb0eb/image_8.png)![Origin at Planet Center disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3085ad76-6d2f-4166-9fc0-6d011bc17b09/image_9.png)

### Converting Coordinates

In order to convert coordinates, you need to access the Georeferencing system, then call one of the functions in the Georeferencing category.

![Find georeferencing Blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e81671a7-72da-49a2-a94f-f25f8de17da0/image_10.png)

![Georeferencing output function nodes 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c1ed82a-3791-47f8-a357-22cef8ff8327/image_11.png)![Georeferencing output function nodes 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a59ec9bc-29f6-4cc0-ae7c-461fc85d09ff/image_12.png)

The possible conversions are explained in the picture below.

![Conversion paths](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5c45f54-4b0d-407d-baa8-7e8304d30fe7/image_13.png)

It is important you remember the Georeferencing system works in double precision, and cannot directly expose the coordinates in the Blueprint system that only support single precision floating values. The system outputs specific structures (`FCartesianCoordinates`, `FGeographicCoordinates`), and we recommend using these structures during all computations, then getting their float approximations at the final step.

**Unreal Engine CRS** is your level coordinate system. Every Actor has its coordinates in `FVector` variables. The first step is for you to transform these coordinates into a Georeferenced CRS, but still using Cartesian coordinates, (ECEF or Projected), depending on your case. You then have the ability to convert this location to geographic coordinates.

When you transform Unreal Engine coordinates into Projected or ECEF coordinates, the computation path depends on the Flat Planet / Round Planet property.

For example, if you are on a Round Planet and ask for an **Engine to Projected** conversion, it first converts the coordinates to ECEF (basic translation), then to Projected (complex projection). These intermediate steps are illustrated by the Green and Red circular arrows. That means, if you are interested in getting the geographic coordinates only, the optimal path for performance will be **UE > ECEF > Geographic** if you are on a Round Planet, and **UE > Projected > Geographic** on a Flat Planet.

![Optimal Blueprint paths for conversions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba9c84d9-86c7-4a82-b1f3-5e6bf8ab21fd/image_14.png)

### Obtaining Values

Once you have the `FCartesianCoordinates` or `FGeographicCoordinates`, you have different options to get the values:

-   In Blueprint, by calling ToFloatApproximation (this approximation corresponds to the conversion from double precision to Blueprint single precision).
-   By using custom C++ code to do your own processing; if you want to maintain the full double precision, we recommend getting these values by writing functions that will directly take one of the `FCartesianCoordinates` or `FGeographicCoordinates` structures.
-   By converting them to a display text, with possible rounding options.

![Blueprint node options for obtaining values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82aacd70-7f94-462e-8c04-6b06af0e690f/image_15.png)

| Formatting | FCartesianCoordinates | FGeographicCoordinates |
| --- | --- | --- |
| To Compact Text | (\[X\], \[Y\], \[Z\]) | 
(\[Latitude\], \[Longitude\], \[Altitude\]m)

With Latitude, Longitude possibly written as \[Degree\]° \[Minutes\]' \[Seconds\]"



 |
| To Full Text | X=\[X\], Y=\[Y\], Z=\[Z\] | 

Latitude=\[Latitude\] Longitude=\[Longitude\] Altitude=\[Altitude\]m

With Latitude, Longitude possibly written as \[Degree\]° \[Minutes\]' \[Seconds\]"



 |
| To Separate Texts | 

\[X\]

\[Y\]

\[Z\]



 | 

\[Latitude\]

\[Longitude\]

\[Altitude\]



 |

### Tangent Vectors and Transforms

You can use the Georeferencing system to get the **Tangent** vectors (East, North, Up) expressed in the Unreal Engine CRS by using the **Get ENUVectors at Geographic Location** node. You can use this, for example, to move a pawn that will follow the planet surface.

![Get ENUVectors at Geographic Location Blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/531cca16-bfd4-4ee8-8af5-0e1df6157c82/image_16.png)

You can also get the **Tangent Transform** at any location on the planet using the **Get Tangent Transform at Geographic Location** node. Combining this transformation with a local object transformation will get the world-space transformation of your object to the Unreal Engine CRS.

![Get Tangent Transform at Geographic Location Blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09f8142b-0984-4075-b0c2-f55fe94e4414/image_17.png)

A very specific function node is also provided: **Get Planet Center Transform**. If you have your own ellipsoidal planet mesh that you want to position in a way that it will be tangent to the origin that you declared in your Georeferencing settings, call this function to set this Actor transformation and it will be oriented to the location you defined.

![Get Planet Center Transform Blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f245e301-9b3c-4d20-b381-c2c4ca54ff33/image_18.png)

## Additional Tools and Content

The Georeferencing system comes with additional tools located in the **Georeferencing Content** folder in the **Content Browser**. You can display these if you select **Show Plugin Content** in the **View Options** dropdown menu.

### Georeferencing Status Bar

You can find a sample **UMG widget** in `/GeoReferencing/UI/UMG_GeoStatusBar`, which, once added to the viewport, will display the current view location in various CRS: Projected, Geographic, and ECEF.

![Georeferencing widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8bfc072-df01-46fb-9bb4-4d4319c8cb8c/image_19.png)

You can duplicate it and customize it to your liking.

![Georeferencing widget in action in Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/149bf727-f4ec-40f1-9cba-7d197aca1f1b/image_20.png)

### Coordinates Inspector Utility Widget

You can find a special **Editor Utility Widget** in `/GeoReferencing/UtilityWidgets/EUW_CoordinatesInspector`. If you run it inside the editor, it displays a panel where you can control the georeferenced coordinates of your view, and of the point located under your mouse.

![Coordinates Inspector widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/091c6816-2d95-4310-87d6-c0b0899c54a0/image_21.png) ![Coordinates Inspector widget in action in Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2aa2d5a-517f-4876-9cd4-6b4e750e9d09/image_22.png)

### Location Probes and Rebasing Actors

In the `GeoReferencing/Models/LocationProbe/BP_LocationProbe` folder, you can find a **BP\_Location Probe** Blueprint for performing in-game coordinate measurements.

Drop it in your level, add it to any location, and it will display its coordinates in each CRS.

You can even spawn a grid of probes using one of the provided Spawner Blueprints to automate the process.

![Location Probe and Rebasing Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7e36a12-6037-4fee-a13c-efd79d4ea10b/image_23.png)![Location Probe Blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0088ead0-70e7-49fd-a2e5-7ab08a0baf31/image_24.png)

![Location Probes in action in Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9328499-8481-44c3-818e-cad08d2269be/image_25.png)

To deal with large coordinates, you can have Unreal Engine shift the origin to ensure accuracy.

This rebasing system is automatically used during World Composition, but you can also control it directly. For that purpose, a **BP\_Rebasing** Actor is provided as an example to demonstrate how you can control this system.

The Georeferencing system always considers the current origin offset in its computations.