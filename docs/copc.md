## Overview of :material-file-cloud: Cloud Optimized Point Cloud (COPC)

<a href="https://copc.io" style="float:center" target="blank" rel="copc">![copc](https://copc.io/COPC_IO-Logo-2color.png){ width="200" } </a> 


![point_cloud](images/lidar_tree.png){ align="right" width="200" height="300" }


The [Cloud Optimized Point Cloud](https://copc.io/){target=_blank} developed by [HOBU](https://hobu.co/){target=_blank} is similar in concept to the [COG](cog.md). It is an `.laz`(lasZip) format with additional point data organized in a clustered [octree](https://en.wikipedia.org/wiki/Octree){target=_blank}. This allows for http streaming of point cloud data from cloud storage (AWS S3, Google Cloud Storage, Azure Blob Storage, etc.) to a web browser or other applications. Just like a [COG](cog.md), it eliminates the need to download large datasets to a local machine for visualization and analysis. 


COPC is based on the open source compression file format, `*.LAZ`, which was developed by Martin Isenburg ([RIP](https://lidarmag.com/2021/10/30/in-memoriam-martin-isenburg-1972-2021/){target=_blank}) and is licensed by his company [RapidLASso](https://rapidlasso.de/){target=_blank} 

<a href="https://hobu.co/" target="blank" rel="hobu">![hobu](images/hobu.png){ align="" width="100" } </a>
<a href="https://rapidlasso.de/" target="blank" rel="rapidlasso">![rapidlasso](https://rapidlasso.de/wp-content/uploads/rapidlasso_square_256x2561.png){ align="center" width="100" } </a>



For technical information on the formats, see the [COPC Specification](https://copc.io/copc-specification-1.0.pdf){target=_blank} and the [LAS Standard](https://www.asprs.org/a/society/committees/standards/LAS_1_4_r13.pdf){target=_blank}


___

## Example COPCs Online

Here is a drone-based point cloud in the COPC format. It is 686 mb and stored in Cyverse Data Store [here](https://data.cyverse.org/dav-anon/iplant/home/jgillan/USGA/imagery_products/hole17_point_cloud.copc.laz){target=_blank}. You can view it [here](https://viewer.copc.io?state=ee15e0b9ae036865eaada9f398c2d27de94c2cde71bd92cf117156296bf46ab0){target=_blank} using the [COPC Viewer](https://viewer.copc.io/){target=_blank}.


<a href="https://viewer.copc.io?state=ee15e0b9ae036865eaada9f398c2d27de94c2cde71bd92cf117156296bf46ab0" style="float:center" target="blank" rel="copc">![copc](images/copc1.png){ width="400" } </a> 



[Here](https://viewer.copc.io/?copc=https://data.cyverse.org/dav-anon/iplant/home/tswetnam/agic-2022/USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019.copc.laz){target=_blanck} is another COPC example. It is 3DEP lidar data over Prescott, AZ. It is also stored in the Cyverse Data Store [here](https://data.cyverse.org/dav-anon/iplant/home/tswetnam/agic-2022/USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019.copc.laz){target=_blank}.





___
## Applications that can Read COPC
COPCs are just a special case of `laz`, so any application that can read `laz` can read COPC.

QGIS, CloudCompare, Argis Pro, and PDAL can all read COPC


<a href="https://entwine.io" target="blank" rel="entwine">![entwine](https://entwine.io/_images/entwine_logo_2-color.png){ width="100" } </a>

[Entwine](https://entwine.io){target=_blank} is a data organization library for massive point clouds, designed to conquer datasets of trillions of points as well as desktop-scale point clouds.

HoBu was contracted by the USGS to process all of the 3DEP lidar data, these are now hosted on commercial cloud in both reqestor pays buckets and FOR FREE as Entwine Point Tiles: [https://usgs.entwine.io/](https://usgs.entwine.io/)

* More information about these datasets can be found at https://registry.opendata.aws/usgs-lidar/ and at its GitHub page at https://github.com/hobu/usgs-lidar/

* [USGS National Datasets Downloads](https://www.usgs.gov/faqs/can-national-map-data-be-downloaded-direct-links){target=_blank}

<a href="https://copc.io" target="blank" rel="copc">![copc](https://copc.io/COPC_IO-Logo-2color.png){ width="100" } </a>


??? Tip "Installing Open Source Lidar tools"

    [LASTools](https://rapidlasso.com/lastools/){target=_blank} is available for both open source and a paid licensed version

    [PDAL.io](https://pdal.io/en/stable/download.html#current-release-s){target=_blank} - suggest using a Binary install using a package manager like `conda`.

___    
## Create your own COPC

![blah](https://pdal.io/_images/pdal_logo.png){ width="100" align="right" }

The best toolset to creat your own COPC point clouds is PDAL. [Point Data Abstraction Library (PDAL)](https://pdal.io){target=_blank} is a C++ library for translating and manipulating point cloud data.



These data were converted from USGS 3DEP EPT data using PDAL `pipeline` 

??? Tip "processing AWS EPT with PDAL"

    USGS 3DEP data are all freely available over `https://` using the Entwine protocol. 

    These data can be re-processed to become COPC using PDAL's `writers.copc` function.

    Example [`ept2copc.json`](https://raw.githubusercontent.com/tyson-swetnam/agic-2022/main/assets/json/ept2copc.json){target=_blank} script for running directly from the internet to your computer or local host

    **Warning** you must have a fast internet connection and a large amount of RAM on your machine to process large datasets (spatial extent / dense point clouds)

    ``` bash
    conda activate pdal
    ```

    ??? info "ept2copc.json"

        Contents of [`ept2copc.json`](https://raw.githubusercontent.com/tyson-swetnam/agic-2022/main/assets/json/ept2copc.json){target=_blank} 

        ``` json
            {
                "pipeline": [
                    {
            "bounds": "([-12521659, -12513587], [4099398, 4107470], [1500, 3200])",
            "filename": "https://s3-us-west-2.amazonaws.com/usgs-lidar-public/USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019/ept.json",
            "type": "readers.ept",
            "requests": 128,
            "tag": "readdata"
                    },
                    {
                        "type":"filters.outlier",
                        "method":"statistical",
                        "mean_k":12,
                        "multiplier":2.2
                    },
                    {
                        "type":"filters.smrf",
                        "scalar":1.2,
                        "slope":0.2,
                        "threshold":0.45,
                        "window":16.0
                    },
                    {
                        "type": "filters.range",
                        "limits": "Classification![7:7],Z[2000:2700]"
                    },
                    {
                        "type":"filters.hag_delaunay"
                    },
                    {
                        "in_srs": "EPSG:3857",
                        "out_srs": "EPSG:26912",
                        "tag": "reprojectUTM",
                        "type": "filters.reprojection"
                    },
                    {
                        "filename": "USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019.copc.laz",
                        "inputs": [ "reprojectUTM" ],
                        "tag": "writerscopc",
                        "type": "writers.copc"
                    },
                    {
                        "filename": "USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019_dem.tif",
                        "gdalopts": "tiled=yes, compress=deflate",
                        "inputs": [ "writerscopc" ],
                        "nodata": -9999,
                        "output_type": "min",
                        "resolution": 1.0,
                        "type": "writers.gdal",
                        "window_size": 6
                    }
                ]
            }
        ```


    ```
    pdal -v 5 pipeline ept2copc.json
    ```

    When the pdal script completes, you will have two files: (1) a new `.laz` file with COPC baked into it, and (2) a digital elevation model GeoTIFF generated by GDAL.


[Planetary Computer 3DEP Jupyter Notebook](https://github.com/microsoft/PlanetaryComputerExamples/blob/main/datasets/3dep-lidar/3dep-lidar-copc-example.ipynb){target=_blank}

## Reference Material

[Library of Congress LAS definition](https://www.loc.gov/preservation/digital/formats/fdd/fdd000418.shtml){target=_blank}

[OGC LAS Standard](https://www.ogc.org/standards/LAS){target=_blank}

[USGS NGS Lidar Base Specification](https://www.usgs.gov/ngp-standards-and-specifications/lidar-base-specification-online){target=_blank}


