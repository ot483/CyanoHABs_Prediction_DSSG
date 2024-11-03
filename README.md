# Cynobacteria in the Kinneret - DSSG 🦠
This repository contains the code for the Data Science for Social Good (DSSG) project on predicting cyanobacteria blooms in the Kinneret.

**Team members:** Maor Moshe, Iyar Hadad, Tal Raviv, Vitaly Lubimzev, Amit Yehuda  
**CIDR**, September 2024  
Collaboration with **Israel Oceanographic & Limnological Research (IOLR)**

## Data Preprocessing 🧹
The file `main_preprocessing.py` is responsible for the data preprocessing. Run this file to generate the final dataset that will be used for the model training.
It assembles all data sources into one file that includes a `Year` and `Week` (week number in that year) columns, joined with relevant data for that week.

At the beginning of the script, the user should specify the path to the data files and the path to the output files, or use the default paths.
We recommend creating a `data` folder outside the repository (in one directory with this project) and storing all the data files there. Several files will be created along the way in this directory.

The preprocessing handles the following data sources:

#### FluoroProbe data 🧪
The script uses the original FP file (as it was uploaded by IOLR team to Google Drive).
It will first remove unnecessary columns and perform some data cleaning.
Then it fills the missing values in the data using Prophet.

#### Rain data 🌧
The data containing the daily amount of rain was downloaded from the website of the Israel Meteorological Service (השירות המטאורולוגי) from a specific station (tzemach in our case).
The format of this data is a `.csv` file with two columns only - one called `date` and one for the amount of rain. The script completes the missing dates (no rain).

#### Inflow data (Huri Bridge - Jordan River) 💦 
The data contains the daily amount of water flow. This input is a csv file with two columns - one named `date` and one names `Discharge [m^3/s]`.
There were some missing values in the data, which are predicted using seasonal decomposition of time series (SARIMA model).

#### Water flows data (spatial) 🌊
The script uses the original flows data, which was uploaded to Google Drive as `kinneret_uvt_2019_2023.tar.gz`. Please unzip before running the script.

ADD water trend model - the flows trend script saves its intermediate files `./data/processed` folder.

In addition to the flows trend model, we added 4 features showing the total weekly flow in each direction (north, south, east, west) averaged on the entire lake.

#### Satellites data 🛰
All the satellites data files (sentinel2, sentinel3 and Landsat) should be stored in `./data/satellites_data/` folder in a `.csv` format. The data files should be with the following column names:
`"date","long","lat","chlp"`.  
At the top of `main_preprocessing.py` script, the user should specify the dimensions of the grid that the satellite data will be split into. The script will read each file and split the data into the grid, then it will calculate the mean value of the chlp for each grid cell.

## Models 📈
Documentation on the models appears in each notebook in the `./models` directory.

