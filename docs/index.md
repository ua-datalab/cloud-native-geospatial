[![license](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by.svg)](https://creativecommons.org/licenses/by/4.0/){target=_blank} 

# :material-cloud-braces: Introduction to Cloud Native Geospatial

<figure markdown>
  ![Image title](images/cloudy.gif){ width="300" }
  <figcaption> </figcaption>
</figure>

#### Instructors(s): 

[Tyson Lee Swetnam PhD](https://tysonswetnam.com/){target=_blank} [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](http://orcid.org/0000-0002-6639-7181){target=_blank},
[Carlos Lizárraga-Celaya PhD](https://github.com/carloslizarragac){target=_blank} [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](https://orcid.org/0000-0002-0893-4268){target=_blank},
[Jeffrey Gillan PhD](http://www.gillanscience.com){target=_blank} [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](http://orcid.org/0000-0002-0731-3048){target=_blank}




## About This Course
Welcome! This is an introductory course on Cloud Native Geospatial. This course is for GIS professionals, researchers, remote sensing professionals, and anyone that creates, analyzes, and shares geospatial data. Throughout, we will emphasize Open Science principles such as [FAIR](https://www.go-fair.org/fair-principles/){target=_blank} and [CARE](https://www.gida-global.org/care){target=_blank}, and highlight primarily Open Source tools. 


<br/> Here are the topics we will cover:

* [An overview of Cloud Storage, Sharing, and Computing](#lets-use-the-cloud)
* [Integrated Development Environments (IDEs)](ide.md)
* Vector formats such as [GeoJSON](geojson.md)
* Raster formats such as [Cloud Optimized GeoTIFF (COG)](cog.md), [xarray](xarray.md), and [zarr](zarr.md)
* Point cloud format [Cloud Optimized Point Cloud (COPC)](copc.md)
* [SpatioTemporal Asset Catalogs (STAC)](stac.md)

<br/>
Each topic will contain easy-to-understand descriptions, useful real-world examples, as well as hands-on exercises to create, use, and share cloud native formats. 

<br/>
 Helpful skills to have

* a basic understanding of the [Command Line Interface (UNIX)](https://swcarpentry.github.io/shell-novice/){target=_blank}
* a basic understanding of [Python3](https://www.geeksforgeeks.org/introduction-to-python3/#:~:text=Python%20is%20a%20high%2Dlevel,them%20readable%20all%20the%20time.){target=_blank}

## Let's Use the Cloud!

<img align="right" width="300" height="300" src="images/cloud_graphic.png">

GIS and Remote Sensing have become essential tools in many industries and fields of study. The amount of data being collected, analyzed, and available on the web is growing exponentially. So much so that the traditional model of downloading data to your individual desktop computers (for analysis and storage) is becoming a major limitation. 

Cloud Native Geospatial aims to shift the 'Download' model by moving many aspects of data storage, sharing, and compute onto the web using cloud infrastructure. These advances hold the potential to foster collaborations, promote data-driven discovery, drive scientific innovation, increase transparency and improve reproducibility.


<img align="right" width="300" height="300" src="images/cloud_storage.png">

### Data Storage
In a Cloud Native model, geospatial data should be stored in cloud object storage and be available to anyone through a public url. Commercial object storage providers include [Amazon S3](https://aws.amazon.com/s3/){target=_blank}, [Google Cloud Storage](https://cloud.google.com/storage){target=_blank}, and [Microsoft Azure Blob Storage](https://azure.microsoft.com/en-us/services/storage/blobs/){target=_blank}. Another storage option is [Cyverse Data Store](https://cyverse.org/data-store){target=_blank}, which was built for the academic and research communities. 

Utilizing existing cloud storage infrastructure eliminates the need for data providers to maintain their own servers (and APIs) and allows them to focus more on their mission. It empowers individuals to easily share their data on the web while eliminating costly local storage. Cloud storage is also a great solution for never losing your data due to hardware failure. [Abernathey et al. (2021)](https://doi.org/10.1109/MCSE.2021.3059437){target=_blank} provides a excellent overview of the benefits of cloud storage.

### Data Sharing 
Sharing of geospatial data from cloud storage can be greatly improved with the use of **Cloud Native Formats**. These formats are designed to be used in the cloud and are built for http streaming. This means that users can view and analyze data without downloading the entire dataset. Analagously, this is like going from the original [Napster](https://en.wikipedia.org/wiki/Napster) model of downloading music to the Spotify model of streaming music.

There is a cloud native format to fit almost any geospatial data type. For example, [GeoJSON](geojson.md) is a cloud native format for vector data, [Cloud Optimized GeoTIFF (COG)](cog.md) is a cloud native format for raster data, and [Cloud Optimized Point Cloud (COPC)](copc.md) is a cloud native format for point cloud data. [Xarray](xarray.md) and [zarr](zarr.md) are cloud native formats that can be used for multi-dimensional raster data.

<center>
<a href="https://geojson.io" style="float:left" target="blank" rel="geojson">![geojson](https://brands.home-assistant.io/_/geo_json_events/logo.png){ width="200" height="25" } </a>

<a href="https://cogeo.org" style="float:right" target="blank" rel="cog">![cog](https://www.cogeo.org/images/logo/Cog-02.png){ width="200" height="50" } </a> 

<a href="https://stacspec.org" style="float:center" target="blank" rel="stac">![stac](https://d33wubrfki0l68.cloudfront.net/22691a3c3002324451ed99f4009de8aab761e1b7/d24da/public/images-original/stac-01.png){ width="200" height="25" } </a>
</center> 

<center>
<a href="https://zarr.readthedocs.io" style="float:left" target="blank" rel="zarr">![zarr](https://zarr.readthedocs.io/en/stable/_static/logo1.png){ width="100" } </a>
<a href="https://docs.xarray.dev" style="float:center" target="blank" rel="xarray">![xarray](https://docs.xarray.dev/en/stable/_static/dataset-diagram-logo.png){ width="200" } </a> 
<a href="https://copc.io" style="float:right" target="blank" rel="copc">![copc](https://copc.io/COPC_IO-Logo-2color.png){ width="200" } </a> 
</center>
<br/>
<br/>
<br/>

Another effort to improve data sharing is the [SpatioTemporal Asset Catalog (STAC)](stac.md). It is a [json](https://en.wikipedia.org/wiki/JSON){target=_blank} based metadata and API standard for geospatial data. It's goal is to make geospatial data more easily worked with, indexed, and discovered. 





### Cloud Compute 
Moving geospatial analysis and computation from your local machine to the cloud has several advantages: 

* With cloud computing, you can avoid the upfront cost and complexity of owning and maintaining your own IT infrastructure.

* Cloud computing allows groups or individuals to scale up (or down) their operations quickly as their computing needs change.

* Cloud computing allows users to access their data and applications from anywhere, on any device, at any time.

* Geospatial in the cloud empowers colleagues to work directly together on the same data, models, and applications. The same way that [Google Docs](https://www.google.com/docs/about/){target=_blank} allows multiple people to work on the same document at the same time.

Google Earth Engine -walled garden  

Microsoft Planetary Computer

ArcGIS Online

Interative computing through jupyter notebooks

<br/>


## Open Architectures

The new approach to data sharing, focused on object storage rather than file downloads. This cloud platform approach is scalable and instead of moving data to processing systems near users as is the tradition, brings processing, computing, analytics and visualization to data – so called data proximate workbench capabilities, sometimes also referred to as server-side processing.

<img src="https://miro.medium.com/max/1400/1*FkR2h8f_Lut00Uo_Pxogvg.png" width=480>

(Open Architecture for scalable cloud-based data analytics. From Abernathey, Ryan (2020): Data Access Modes in Science.)

---

## Resources  

Abernathey, R. P.  et al. (2021) "Cloud-Native Repositories for Big Scientific Data," in Computing in Science & Engineering, vol. 23, no. 2, pp. 26-35, 1 March-April 2021, https://doi.org/10.1109/MCSE.2021.3059437

[Chris Holmes's blog on Cloud Native](https://www.ogc.org/blog-article/towards-a-cloud-native-ogc/){target=_blank}

[Cloud-Native Geospatial Outreach Event - April 2022 - from Open Geospatial Consortium (OGS)](https://www.youtube.com/watch?v=hprPIr9Vt4M&list=PLQsQNjNIDU87yUFyKy1seaiRps389RPwk){target=_blank}

Gentemann, C. L., et al. (2021). “Science Storms the Cloud”. AGU Advances, 2, e2020AV000354. https://doi.org/10.1029/2020AV000354

[Mapscaping Podcast on Cloud Native Geospatial](https://mapscaping.com/podcast/cloud-native-geospatial/){target=_blank}