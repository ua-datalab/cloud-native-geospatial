<figure markdown>
  ![Image title](images/cog_logo.png){ width="200" }
  <figcaption> </figcaption>
</figure>

### Background

The [TIFF file format (Tagged Image File Format)](https://en.wikipedia.org/wiki/TIFF){target=_blank} is an old format dating back to 1992. TIFF are great for high-resolution verbatim [raster images](https://en.wikipedia.org/wiki/Raster_graphics){target=_blank}. TIFF are still used a bit in high-end photography, but where it has really grown a second life is in digital cartography. The variation called [GeoTIFF](https://en.wikipedia.org/wiki/GeoTIFF){target=_blank} has been widely adopted as a way to share satellite images and other satellite data.

While the GeoTIFF file format has long been thought of as only suitable for raw data: if you wanted to display it on a map, you’d convert it into tiles. If you wanted a static image, you’d render it into a PNG or JPEG. But ***Cloud-Optimized GeoTIFF*** means that GeoTIFFs can be a bit more accessible than they used to be. 

### Cloud Optimized GeoTIFF (COG)
A [Cloud Optimized GeoTIFF (COG)](https://www.cogeo.org/){target=_blank} is a regular [GeoTIFF file](https://www.ogc.org/standards/geotiff){target=_blank}, aimed at being hosted on a HTTP file server, with an internal organization that enables more efficient workflows on the cloud. In other words, we can stream the content of a GeoTIFF file from a server into a client application without having to download the full file.


COGs have three major features that are baked into the file: 

* [Internal tiling](#tiling)
* [Internal overview structures](#overviews)
* [HTTP GET Range Requests](#https-get-range-request)

### Tiling

Tiles are small, regular, and independent parts of a larger map. They are typically 256x256 pixels in size. COGs have tiles explicitly specified in their format structure, whereas regular GeoTIFFs may not. Tiling is a way to speed up map display because only the tiles that are visible in the current view need to be loaded.


### Overviews 

Overviews are downsampled thumbnail images of the tile. A COG will have many overviews matched to each [Zoom Level](https://wiki.openstreetmap.org/wiki/Zoom_levels){target=_blank}.

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geotiff_pyramid.png" target="blank" rel="geotiff_pyramid">![geotiff_pyramid](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geotiff_pyramid.png){ width="500" } </a>
    <figcaption>GeoTIFF pyramid by Zoom Level</figcaption>
</figure>

### HTTP(s) GET Range Request

The HTTP GET Range Request, also known as [Byte Serving](https://en.wikipedia.org/wiki/Byte_serving){target=_blank}, allows a client to request specific chunks of the COG using a combination of the tiles and overviews. If you are zoomed into a specific portion of the COG, then you only request the tiles that are visible in the current view. This is the same technology that enables streaming of other media types like video and audio. 


Check out the [COG Specification](https://github.com/cogeotiff/cog-spec/blob/master/spec.md){target=_blank}

## Where Can I Find COG examples on the internet?
There are numerous cloud based data stores hosting COGs, take a look through a few of these:


[Microsoft Planetary Computer Catalog](https://planetarycomputer.microsoft.com/catalog){target=_blank} - most of the imagery datasets in Planetary Computer are hosted as COGs. You can also view the catalog through the Planetary Computer [STAC API browser](https://radiantearth.github.io/stac-browser/#/external/planetarycomputer.microsoft.com/api/stac/v1/){target=_blank} 



[ESA Sentinel-2 COGs](https://registry.opendata.aws/sentinel-2-l2a-cogs/){target=_blank}


[Planet](https://www.planet.com/) is streaming out their imagery as COGs. You can also do simple analysis of COGs direclyt within the Planet platform. 


## What applications can I stream a COG into?

This example COG is a drone orthomosaic that is hosted in Cyverse Data Store. We can stream it to this viewer. [Example COG in Cogeo Map](https://www.cogeo.org/map/#/url/https%3A%2F%2Fdata.cyverse.org%2Fdav-anon%2Fiplant%2Fhome%2Fjgillan%2FSTAC_drone%2F22_2_ortho_cog.tif/center/-110.84602,31.78408/zoom/18){target=_blank}

The COG is on Cyverse Data Store: https://data.cyverse.org/dav-anon/iplant/home/jgillan/STAC_drone/22_2_ortho_cog.tif


Here is another [example](https://www.cogeo.org/map/#/url/https%3A%2F%2Foin-hotosm.s3.us-east-1.amazonaws.com%2F64d1bd4419cb3a000147a56a%2F0%2F64d1bd4419cb3a000147a56b.tif/center/-90.68608,42.49636/zoom/17){target=_blank} of drone imagery COG from [OpenAerialMap](https://openaerialmap.org/){target=_blank}. The data is hosted on AWS and streamed to the cogeo viewer 


https://www.cogeo.org/map/

[COGEO.xyz](https://cogeo.xyz/){target=_blank}



Stream into Qgis

open a COG in QGIS

* Open QGIS

* In the "Layers" then "Add Layer" and then "Add Raster Layer" 

* Choose the Source Type and select "Protocol: HTTP(s), cloud, etc" for a file on your computer

* Enter a valid `https://` in the `URl` field for a COG you found online

Stream into ArcGIS Pro

Stream into ArcGIS Online

What kind of analysis can I do on a COG?



## How Can I create a COG?
gdal

* [`cogger`](https://github.com/airbusgeo/cogger){target=_blank} is a rapid COG generator from GeoTIFF

Python library Rio-cogeo - RasterIO plugin to create and validate COGs

Can QGIS output COG? Not that I know of

Can ArcGIS Pro output COG?

GEE can output COGs



create a COG from a GeoTIFF

Open a console and check your `gdal` installation

``` bash
gdalinfo --version
```

Make sure that you're operating on at least `v3.1` of GDAL (current latest `v3.5.1`)

[Sample USGS GeoTIFFs](https://pubs.usgs.gov/ds/121/prescott/prescott.html){target=_blank}

``` bash
gdal_translate p_ndvi_cor.tif p_ndvi_cor_cog.tif \
-b 1 -b 2 -b 3  \
-of COG \
-co TILING_SCHEME=GoogleMapsCompatible \
-co COMPRESS=JPEG \
-co OVERVIEW_QUALITY=100 \
-co QUALITY=100
```

Check the file size of your example file and your output file. Which is larger?

Now, if we want to add overviews to the output `p_ndvi_cor_cog.tif`:

``` bash
gdaladdo \
  --config COMPRESS_OVERVIEW JPEG \
  --config JPEG_QUALITY_OVERVIEW 100 \
  --config PHOTOMETRIC_OVERVIEW YCBCR \
  --config INTERLEAVE_OVERVIEW PIXEL \
  -r average \
  p_ndvi_cor_cog.tif \
  2 4 8 16
```


## GDAL

The lastest versions of [GDAL](https://gdal.org){target=_blank} (>v3.1) have [COG generator](https://gdal.org/drivers/raster/cog.html){target=_blank} installed by default.

[Most GIS software](https://gdal.org/software_using_gdal.html#software-using-gdal){target=_blank} use GDAL.

??? Tip "Install GDAL"

    GDAL installation can at times be difficult. When different older python environments are installed on a desktop or laptop GDAL can become broken or incompatiblity issues can come up when installing it.

    [USGS Windows GDAL Installation Guide](https://apps.nationalmap.gov/raster-conversion/gdal-installation-and-setup-guide.html){target=_blank} 

    [Official GDAL Install Guide](https://gdal.org/download.html){target=_blank} 

    [QGIS](https://www.qgis.org/en/site/){target=_blank} installs GDAL by default

    [Anaconda](https://anaconda.org/conda-forge/gdal){target=_blank} and its package management `conda`

    [Docker `osgeo/gdal`](https://hub.docker.com/r/osgeo/gdal){target=_blank} images are maintained on the Docker Hub



## Example COGs in WebGL

[Open Layers COGs](https://openlayers.org/en/latest/examples/cog.html){target=_blank}

[Open Layers WebGLTile Pyramid from COG](https://openlayers.org/en/latest/examples/cog-pyramid.html){target=_blank}








Try adding the `https://` URL of the COG that you found on the internet into the viewer.





## **Step 5** Optional: upload the file to a public `https://` endpoint

If you have your own web server, or public cloud bucket, you can upload your new COG and view it using one of the example viewers, or try loading it using QGIS.

Here is an [example using the CyVerse Data Store and the CoGEO viewer](https://www.cogeo.org/map/#/url/https%3A%2F%2Fdata.cyverse.org%2Fdav-anon%2Fiplant%2Fhome%2Ftswetnam%2Fagic-2022%2Fp_ndvi_cor_cog.tif/center/-112.9834,34.4884/zoom/14){target=_blank}


[COGS in Production blog post by Sean Rennie](https://sean-rennie.medium.com/cogs-in-production-e9a42c7f54e4){target=_blank}





### If I have COGs, do I still need a tile server? 
There are a few reasons why you might still want to use a tile server with COGs:

* Performance: Tile servers can cache tiles in memory, which can improve performance by reducing the number of times that tiles need to be read from disk.

* Scalability: Tile servers can be scaled to handle large numbers of requests.

* Security: Tile servers can be used to encrypt tiles, which can help to protect them from unauthorized access. If you are streaming COGs to a large number of clients or if you need to ensure that your tiles are secure, then I recommend using a tile server. However, if you are only streaming COGs to a small number of clients and you do not need to worry about security, then you can use the built-in tiles in COGs.


WMTS - Web Map Tile Service - best for use with desktop applications

XYZ - best for use with web applications

WMTS and XYZ tiles are primarily designed for efficient map display in web environments. Their main goal is to provide quick and seamless map visualizations over the internet by serving small, pre-defined tiles at multiple zoom levels. These tiles are ideal for web maps where users might pan and zoom around the globe, as the small tiles can be fetched and displayed rapidly.

However, for analysis purposes – where users might want to compute statistics, apply algorithms, or extract detailed information from imagery or raster data – these tiling methods are not optimal. The reason is that analysis often requires access to raw, high-resolution data rather than the downsampled or potentially lossy representations provided by these tiles.

That's where formats like Cloud Optimized GeoTIFFs (COGs) come into play. COGs are designed to allow for efficient access to high-resolution raster datasets, making them more suited for analytical purposes. With COGs, one can access and process only specific portions of a large raster without downloading the entire file, making it efficient for cloud-based analysis workflows.



