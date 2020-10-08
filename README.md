# Gravity data compilation for Australia

Playing around with downloading, cleaning, and combining all available
Geoscience Australia gravity data.

> This is based on the compilation by [Wynne (2018)](https://doi.org/10.26186/5c1987fa17078).
> The data are distributed under a CC-BY 4.0 license (see the source).

The metadata records (including the download link) for all surveys were
downloaded manually in batches of 100 (:disappointed:). These records are
available in the `metadata` folder. The notebook `notebooks/catalogue.ipynb`
combines all these records into a single file `metadata/records.csv` and
includes the proper download URL and file size (as returned by the server).

The 1631 surveys total less than 400 MB so it's not a large amount of data. The
notebook `notebooks/download.ipynb` uses
[Pooch](https://www.fatiando.org/pooch/latest/) to download all survey netCDF
files to a `data` folder. The individual surveys will not be included in the
repository to avoid making it too big.
