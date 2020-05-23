# PyWrfHydroCalib

## Disclaimer:
This software is preliminary and is subject to revision. The software is provided in Beta status and under the condition that NCAR/UCAR will not be held liable for any damages resulting from the authorized or unauthorized use of the software. Until the official public release, this software is unsupported and “use at your own risk”.

## Introduction
This package provides tools for calibration of WRF-Hydro. All the scripts here are either in Python or R. The user manual has the full description of the underlying concepts and technical details on what is included in the database and how to set a calibration run from start to finish. 

## Content of package
The main workflow management scripts are in python which are placed in the main directory. The backend R and Python scripts which do the parameter adjustment, statistics calculations, updating the parameters for the next version (thought DDS calibration technique), etc are in the [core](/core). [util](/util) has few utilities that the important ones are described in the manual. 

# dependencies
R required packages 
* data.table
* ncdf4
* ggplot2
* gridExtra
* plyr
* hydroGOF

Python required packages 
* netCDF4 for Python
* pandas
* numpy
* psycopg2
* psutil

## Quick instruction how to set up an experiment
Defile the followings first: 
* PATH_TO_PyWrfHydroCalib : Path to the PyWrfHydroCalib
* PATH_TO_Database
* PATH_TO_domainMeta.csv 
* PATH_TO_setup.parm

Each steps needs to be finished before you run the command in next step. 
Step 1: Create database
```bash
python $PATH_TO_PyWrfHydroCalib/initDB.py --optDbPath $PATH_TO_Database`
```
Step 2: Input domain meta
```bash
python $PATH_TO_PyWrfHydroCalib/inputDomainMeta.py $PATH_TO_domainMeta --optDbPath $PATH_TO_Database`
```
Step 3: Initialize batch job
```bash
python $PATH_TO_PyWrfHydroCalib/jobInit.py $PATH_TO_setupParm --optExpID 1 --optDbPath $PATH_TO_Database`
```
Step 4: Run spinup
```bash
python $PATH_TO_PyWrfHydroCalib/spinOrchestrator.py 1 --optDbPath $PATH_TO_Database`
```
Step 5: Run calibration
```bash 
python $PATH_TO_PyWrfHydroCalib/calibOrchestrator.py 1 --optDbPath $PATH_TO_Database
```
Step 6: Run validation
```bash 
python $PATH_TO_PyWrfHydroCalib/validOrchestrator.py 1 --optDbPath $PATH_TO_Database
```
