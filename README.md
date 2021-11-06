# DMPOT

Distributed model parameter optimization tool for the SWAT model, dmpot_swat, is a tool for conducting multivariable and multisite calibration of the SWAT model with the distributed optimization procedure.



### Requirements:

[python](https://www.python.org/),[NumPy](http://www.numpy.org/), [SciPy](http://www.scipy.org/), [matplotlib](http://matplotlib.org/), [pandas](http://https//pandas.pydata.org/), [Ray](https://www.ray.io/),[fortranformat · PyPI](https://pypi.org/project/fortranformat/), [GDAL · PyPI](https://pypi.org/project/GDAL/#:~:text= Project description  1 Dependencies.  2,included but provide notices to state... More ),



### Features

1. Sensitivity analysis: available method include Sobol, Morris, and FAST,  based on the [SALib](https://salib.readthedocs.io/en/latest/#)
2. Two modes of optimization for multivariable and multisite calibration: Lumped optimization that implements one optimization across the watershed; Distributed optimization that implements individual optimization based for all subarea groups automatically identified for each user-specified outlet.

### Environment setup notes

#### Install GDAL (Windows)

References: https://github.com/Toblerity/Fiona

Before install:

1. Install python (here, 3.7.6 was used): https://www.python.org/downloads/release/python-376/
2. Install GDAL: https://www.gisinternals.com/index.html
    1. [release-1911-x64-gdal-2-4-4-mapserver-7-4-3-libs.zip](http://download.gisinternals.com/sdk/downloads/release-1911-x64-gdal-2-4-4-mapserver-7-4-3-libs.zip):  compiled libraries and headers
    2. [gdal-204-1911-x64-core.msi](http://download.gisinternals.com/sdk/downloads/release-1911-x64-gdal-2-4-4-mapserver-7-4-3/gdal-204-1911-x64-core.msi): GDAL installation file
    3. Setup the environment properly to include gdal, gdal-data. 
    4. [GDAL-2.4.4.win-amd64-py3.7.msi](http://download.gisinternals.com/sdk/downloads/release-1911-x64-gdal-2-4-4-mapserver-7-4-3/GDAL-2.4.4.win-amd64-py3.7.msi): python-gdal binding
3. Run the following command



### Quick description of the procedure

1. download the code from the src folder

2. Copy all the input files (usually all contents within the txtinout folder created by ArcSWAT) under the "04workingDir" (create one if it does not exist). 

3. Copy the shapefile for the reach of your watershed into the "03gisLayers" folder. Be sure to include all the files for a shapefile (usually including .dbf, .prj, .shp, .shx, .cpg, .sbn)

4. If conducting calibration, prepare the observed data for corresponding outlet setup in the next step. The format need to be exactly same as those provided in the example. The names should be obs_XXXXYYYY.prn. XXXX represents the time frequency of the data, including daily, monthly, or annual. YYYY represents the outlet number.

5. Setup the project configuration files based on your watershed and simulation by editing the "dmpot_Control.set" file under the "01projSetupContPara" folder.

6. Specify the parameters to be used during the calibration by editing the "dmpot_Para_Combined.set" file under the "01projSetupContPara" folder. One parameter is selected by changing the value of the "selectFlag" column into 1. If one parameter is not going to be included, set that value as 0.

7. There are several functions provide:

   1. To just calculate the statistics, run the dmpotswat_1TimeStatCal.py script
   2. To conduct Sensitivity Analysis, run the dmpotswat_SAAnalysis.py script. The output of sensitivity analysis will be stored in the "08SAOutput" folder.
   3. To conduct Calibration, run the dmpotswat_Calibration.py script. The output of calibration will be stored in the "06output" folder.
   4. After calibration, pick up the best run from the objective function output by comparing the value of objective functions of all outlets. Pick one number and edit the "dmpot_Control.set" file under the "01projSetupContPara" folder by changing the value under the line of "Run number for best parameter sets".
   5. Then, to apply the best parameter to the model and get the calibrated and validated model, run the  dmpotswat_ApplyBestParmSet.py script. The output will be stored in a new created folder named with heading of 07.
   6. To generate Flow duration curve after calibration and validation, run the dmpotswat_GenFDC.py script.

   

### Quick description of the procedure

1. (working on)