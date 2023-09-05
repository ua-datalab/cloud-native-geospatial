## Overview of Zarr

[Zarr](https://zarr.readthedocs.io/en/stable/getting_started.html){target=_blank} is a general-purpose, chunked, compressed, N-dimensional array format. It is designed to be efficient for storing and accessing large datasets. Zarr can be used to store a variety of data types, including geospatial raster and vector data. Zarr is also a Python package that provides an implementation of chunked, compressed, N-dimensional arrays.


<figure markdown>
  ![Image title](images/zarr.png){ width="600" }
  <figcaption> </figcaption>
</figure>

Zarr integrates direclty with [Xarray](https://xarray.dev/){target=_blank}.



Zarr dependes on [NumPy](https://numpy.org/){target=_blank}
 and can save data from NumPy arrays. When paired with [Dask](https://www.dask.org/){target=_blank}
, Zarr's parallel processing and file transfers increases the read/write speed of your NumPy array data.


## Examples using Zarr

[Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/docs/quickstarts/reading-zarr-data/){target=_blank}


