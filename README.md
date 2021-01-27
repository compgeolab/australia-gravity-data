# Gravity data compilation for Australia

This repository contains code to download, clean, and combine all available
[Geoscience Australia](http://www.ga.gov.au/) gravity data.

> Based on the compilation by [Wynne (2018)](https://doi.org/10.26186/5c1987fa17078),
> which is distributed under a CC-BY 4.0 license (see the source).

You can run and explore the code online through [mybinder.org](https://mybinder.org):

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/compgeolab/australia-gravity-data/main?urlpath=lab/tree/notebooks%2Fexplore.ipynb)


![Map of the gravity disturbance of Australia from the compiled dataset](australia-ground-gravity.png)
*Figure: Preview of the compiled gravity observations, downsampled 
with a blocked mean. Gravity disturbances were calculated from the 
compiled dataset.*

**NOTE:** After I did all of this, I discovered
[GeoscienceAustralia/geophys_utils](https://github.com/GeoscienceAustralia/geophys_utils)
which would have allowed me to download the individual surveys using a web API from Python.
This would have saved the work of finding, downloding, and combining the metadata files.

## Download the data compilation

The data compilation is available for download as a single netCDF file
from *figshare*: https://doi.org/10.6084/m9.figshare.13643837.v1

You can download and cache the data directly from your Python code using
[Pooch](https://www.fatiando.org/pooch/latest/):

```python
import xarray as xr
import pooch

fname = pooch.retrieve(
    url="https://ndownloader.figshare.com/files/26193446",
    known_hash="sha256:50f2fa53c5dc2c66dd3358b8e50024d21074fcc77c96191c549a10a37075bc7e",
    downloader=pooch.HTTPDownloader(progressbar=True),
    fname="australia-gravity.nc",
)

# Load the data with xarray
data = xr.load_dataset(fname)
```

Paste the code above in your Jupyter notebooks or scripts to let Pooch 
automatically download the file (printing a progress bar), store it in a cache
folder, check the download integrity, and return to you the path to the cached
file. The download only happens the first time this code is run. Afterwards,
Pooch finds the data in the cache and only returns the link (so you can use
this code everywhere you need this file).

## Citing this compilation

If you use this dataset in a publication, please cite both the original 
compilation by [Wynne (2018)](https://doi.org/10.26186/5c1987fa17078) and the
figshare archive of this version:

> Wynne, P. (2018). NetCDF Ground Gravity Point Surveys Collection (Version 1.0). Commonwealth of Australia (Geoscience Australia). https://doi.org/10.26186/5C1987FA17078 
>
> Uieda, L. (2021). Ground gravity data compilation for Australia filtered by survey quality and packaged in CF-compliant netCDF [Data set]. figshare. https://doi.org/10.6084/M9.FIGSHARE.13643837.V

## Metadata and download links

The metadata records (including the download link) for all of the 
original surveys were downloaded manually in batches of 100 
(:disappointed:). 
These records are available in the `metadata` folder.

## Notebooks

* [`notebooks/catalogue.ipynb`](https://nbviewer.jupyter.org/github/compgeolab/australia-gravity-data/blob/main/notebooks/catalogue.ipynb):
  combines all these records into a single file
  (`metadata/records.csv`) and includes the proper download URL and file size
  (as returned by the server).
* [`notebooks/download.ipynb`](https://nbviewer.jupyter.org/github/compgeolab/australia-gravity-data/blob/main/notebooks/download.ipynb):
  uses [Pooch](https://www.fatiando.org/pooch/latest/)
  to download all survey netCDF files to a `data` folder. The 1631 surveys total
  less than 400 MB so it's not a large amount of data. The individual surveys
  will not be included in the repository to avoid making it too big.
* [`notebooks/merge.ipynb`](https://nbviewer.jupyter.org/github/compgeolab/australia-gravity-data/blob/main/notebooks/merge.ipynb):
  loads all surveys, selects the more relevant data, filter out unreliable surveys,
  merge them into a single dataset, and standardize the metadata (following CF
  conventions). Saves the data compilation to netCDF in `australia-gravity-data.nc`.
* [`notebooks/explore.ipynb`](https://nbviewer.jupyter.org/github/compgeolab/australia-gravity-data/blob/main/notebooks/explore.ipynb):
  explore the compiled gravity data using plots and maps.

## License

All source code is made available under a MIT license.
You can freely use and modify the code, without warranty,
so long as you provide attribution to the original authors.
See [LICENSE](LICENSE) for the full license text.

The data compilation is distributed under a [CC-BY license](https://creativecommons.org/licenses/by/4.0/).
