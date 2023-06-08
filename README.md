
# Notes
Note: Forked the offical repo to download Sentinel-5P data from https://github.com/bilelomrani1/s5p-tools  

Downloaded data from satellite [Sentinel-5P](https://www.esa.int/Applications/Observing_the_Earth/Copernicus/Sentinel-5P) from the [Copernicus Open Access Hub](https://scihub.copernicus.eu). The collect is based on the `sentinelsat` [package](https://github.com/sentinelsat/sentinelsat) and the [API Hub Access](https://scihub.copernicus.eu/twiki/do/view/SciHubWebPortal/APIHubDescription). L3 resampling is made with [HARP tools](https://cdn.rawgit.com/stcorp/harp/master/doc/html/harpconvert.html).


## Installation
```bash
conda env create --name environment_name --file environment.yml
conda activate <envname>
pip install sentinelsat
```
> **Note1:** sentinelsat is not available through conda so we install it using pip

> **Note2:** `conda` can take a while to resolve dependencies.

## Downloading and processing data
```bash
python s5p-request.py L2__NO2___ --aoi aux-files/sohio.geojson --date 20230201 20230207
```
This Downloads the L2__NO2___ product data for the coordinates outlined in our .geojson file, for the given data range. 

TROPOMI Level 2 geophysical products are given in the table below:

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


# Power App
Power app was built with person O364 E5 License using BingSearch API, Open AI Whisper API, OpenAI GPT-3.5 Turbo API, and downloaded data related to Ohio First Responders and representatives. Saved the Power App files to Github using the "experimental" Upcoming Feature, Git Version Control: https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/git-version-control

# Ohio Data
Contains static excel files of Ohio Representatives and first responders