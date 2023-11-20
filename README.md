# Cloud Native Geospatial
This repository holds educational material about Cloud Native Geospatial. We cover topics such as formats (COG, COPC, Zarr), cloud computing platforms, and cataloging (STAC). The material is presented in a Github page using the MKDocs material theme. The website is currentely hosted at https://www.gillanscience.com/cloud-native-geospatial/

# To Development this Material Locally

Download this repo to your local machine

`git clone https://github.com/jeffgillan/cloud-native-geospatial.git`

`cd cloud-native-geospatial`

`pip install -r requirements_mkdocs.txt`

`mkdocs serve` 

Go to a browser and type `localhost:8000`

## Workshop Ideas

* Create a COG using GDAL or Cyverse App
* Put a COG into Cyverse Data Store and share it out
* Bring a COG into QGIS (container) and do some basic analysis
* Create a COPC using PDAL (either in container or locally)
* Upload COPC into Cyverse and share out to the COPC Viewer and QGIS
* How to containerize geospatial scripts and create a processing pipeline
* How to use STAC and do API calls 
