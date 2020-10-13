# Gravity data compilation for Australia

Playing around with downloading, cleaning, and combining all available
Geoscience Australia gravity data.

> This is based on the compilation by [Wynne (2018)](https://doi.org/10.26186/5c1987fa17078).
> The data are distributed under a CC-BY 4.0 license (see the source).

The metadata records (including the download link) for all surveys were
downloaded manually in batches of 100 (:disappointed:). These records are
available in the `metadata` folder.

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
  conventions).

## License

All source code is made available under a MIT license.
You can freely use and modify the code, without warranty,
so long as you provide attribution to the original authors.

See [LICENSE](LICENSE) for the full license text.
