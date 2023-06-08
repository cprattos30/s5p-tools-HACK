
# S5P-Tools


Downloaded data from satellite [Sentinel-5P](https://www.esa.int/Applications/Observing_the_Earth/Copernicus/Sentinel-5P) from the [Copernicus Open Access Hub](https://scihub.copernicus.eu). The collect is based on the `sentinelsat` [package](https://github.com/sentinelsat/sentinelsat) and the [API Hub Access](https://scihub.copernicus.eu/twiki/do/view/SciHubWebPortal/APIHubDescription). L3 resampling is made with [HARP tools](https://cdn.rawgit.com/stcorp/harp/master/doc/html/harpconvert.html).


## Installation

conda env create --name environment_name --file environment.yml

sentinelsat is not available through conda so we install it using pip
conda activate <envname>
pip install sentinelsat

> **Notes:** `conda` can take a while to resolve dependencies.

## Downloading and processing data

The script `s5p-request.py` is used to query Copernicus Hub, download and process the data. The syntax is the following:

```bash
python s5p-request.py <product-type>
```
where `<product-type>` is a Sentinel-5P product. TROPOMI Level 2 geophysical products are given in the table below.

| Product type | Parameter                                                         |
| ------------ | ----------------------------------------------------------------- |
| L2__O3____   | Ozone (O3) total column                                           |
| L2__NO2___   | Nitrogen Dioxide (NO2), tropospheric, stratospheric, slant column |
| L2__SO2___   | Sulfur Dioxide (SO2) total column                                 |
| L2__CO____   | Carbon Monoxide (CO) total column                                 |
| L2__CH4___   | Methane (CH4) total column                                        |
| L2__HCHO__   | Formaldehyde (HCHO) tropospheric, slant column                    |
| L2__AER_AI   | UV Aerosol Index                                                  |
| L2__CLOUD_   | Cloud fraction, albedo, top pressure                              |

By default, the script downloads all products corresponding to the specified product type for the last 24 hours. Custom date query can be specified with `--date`.

The resulting file is a `netCDF` file in the `processed` folder, binned by time, latitude, longitude, aligned on the same regular grid with resolution 0.01 x 0.01 arc degree by default. For parsing and plotting, we used the Python package `xarray`.

### Options
The script `python s5p-request.py` supports the following optional arguments:


| Option          | Description                                   |
| --------------- | --------------------------------------------- |
| `--date`        | Date used to perform a time interval search   |
| `--aoi`         | Path to the area of interest file (.geojson)  |
| `--unit`        | Unit conversion                               |
| `--qa`          | Quality assurance value threshold             |
| `--resolution`  | L3 grid spatial resolution in arc degrees     |
| `--num-threads` | Number of threads spawned for L2 download     |
| `--num-workers` | Number of processes spawned for L3 conversion |


#### Date
The `--date` option allows to perform a time interval search.

```bash
python s5p-request.py <product-type> --date <timestamp> <timestamp>
```
`<timestamp>` can be expressed in one of the following formats:
  - `yyyyMMdd`
  - `yyyy-MM-ddThh:mm:ssZ`
  - `yyyy-MM-ddThh:mm:ss.SSSZ`(ISO8601 format)
  - `NOW`
  - `NOW-<n>MINUTE(S)`
  - `NOW-<n>HOUR(S)`
  - `NOW-<n>DAY(S)`
  - `NOW-<n>MONTH(S)`


