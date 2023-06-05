This README.txt file was generated on 2023-27-04 by Erica Dale, Victoria Cutler, Mallory Giesie, Lewis White.

**GENERAL INFORMATION**

1\. Title of the Project: Climate Futures for Ecohydrological Modeling of Emerging Fire Regimes in Central Coast California

2\. Author Information 

A. Principal Investigators Contact Information
Name: Erica Dale  
Institution: UCSB  
Email: ericadale@bren.ucsb.edu

Name: Victoria Cutler  
Institution: UCSB  
Email: victoriacutler@bren.ucsb.edu

Name: Mallory Giesie  
Institution: UCSB  
Email:mallorygiesie@bren.ucsb.edu

Name: Lewis White  
Institution: UCSB  
Email: lewiswhite@bren.ucsb.edu


B. Faculty Advisor Contact Information 
Name: Naomi Tague  
Institution: UCSB Tague Lab  
Email: ctague@bren.ucsb.edu 

3\. Date of data collection or obtaining:

This project was developed from 2023-01-01 to 2023-06-09. The original data used for cleaning and organizing the workflow was obtained in January 2023 from CalAdapt.

4\. Geographic location of data collection:

The original data utilized from CalAdapt covers California and surrounding states, including Nevada, Arizona, and Oregon. The application is limited to using this data with an API however, user-input data frames into the configurable workflow are not constrained to this geographic range.

5\. Information about funding sources that supported the collection of
the data:

This project was part of a larger project within the Tague Lab, supported by the Moore Foundation.


**SHARING/ACCESS INFORMATION**

1\. Licenses/restrictions placed on the data: Not Applicable

2\. Links to publications that cite or use the data: Not Applicable

3\. Links to other publicly accessible locations of the data: 

The original CalAdapt data that the workflow was based off can be found at https://cal-adapt.org/data/download/.


4\. Links/relationships to ancillary data sets: Not Applicable

5\. Was data derived from another source? If yes, list source(s): Not Applicable

6\. Recommended citation for the project: Not Applicable

**DATA & FILE OVERVIEW**

1\. File List: 

The current file organization, shown below, is organized into several repositories containing appropriate folders and files. These repositories include data cleaning, workflow of building climate scenarios, the educational visualizations, and the final shiny application.

2\. Relationship between files, if important:

The final repository will have a README folder with important information regarding the project, and user-instructions. For users following the workflow with their own data, the Manual-Workflow folder has the Workflow.Rmd document to walkthrough which sources all of the files in the Functions folder. To use this process, the Workflow file and functions folder must be accessible together. The Automated-App folder contains the build for the interactive online application.

<img src="https://github.com/fire-futures/.github/assets/63022802/5df1cea9-4c44-4f9a-b995-38ac01e4f6ee" alt="repoorganization" width="400">


3\. Additional related data collected that was not included in the
current data package: Not Applicable

4\. Are there multiple versions of the dataset?

Multiple grid cells can be selected for this workflow, and must each be entered as their own data frame. One grid cell will need to be selected as the primary cell for selecting a matching criteria list. The resultant series of selected date ranges will then be applied to the rest of the grid cells.


**METHODOLOGICAL INFORMATION**

1\. Description of methods used for collection/generation of data:

To create the workflow, CalAdapt Global Climate Models were used. We utilized the 4 priority models within the LOCA Downscaled CMIP5 Climate Projections. Each priority model was downloaded with two emission assumptions, RCP 4.5 and RCP 8.5, thus 8 total models.


2\. Methods for processing the data: 

Data acquisition: Within the Shiny Application, the Cal-Adapt API collects the data utilizing user-inputs on model, RCP, and grid cells desired. Otherwise, in the workflow the user will input a dataframe of their own matching the necessary parameters.
Data cleaning: This process prepares the data frame with steps to match units, such as converting temperature from Kelvin into Celcius.
Criteria selection: Within the markdown, a user will follow steps to upload their variable criteria for each season or year they would like to build. Alternatively, within the application, a user can explore interactive graphs to see each climate variable distribution, which might prove useful in creating the criteria table.
Filtering: The list of criteria tables are used to search for matching time periods per table. Each criteria table may have numerous matching time periods, these are all saved as a list of lists.
Randomly select: For each list of matching time periods, a function randomly selects one and saves in a new list. The result is a series of seasons or years, one per criteria table.
Cutting and stitching: The final series of time periods is then used. Going in order of the list, each time period is cut from the original data frame and added to a new data frame. 
Time series: The data frame is converted into time series files beginning with the desired start date followed by the variable measurements. Each variable has its own time series file, with appropriate file extensions.
Grid cell loop: Each grid cell loops through the cutting, stitching, and time series steps.

The output data will be in a file structure, with folders and files named as the model selected and grid cell:
- main output folder
	- metadata.csv
	- grid_1 time series folder
		- grid_1_timeseries.csv
- grid_1_timeseries.rain
		- grid_1_timeseries.tmax
		- grid_1_timeseries.tmin
- grid_1_timeseries.wind
- grid_1_timeseries.relative_humidity_max 
- grid_1_timeseries.relative_humidity_min
- grid_2 time series folder
		- grid_2_timeseries.csv
- grid_2_timeseries.rain
		- grid_2_timeseries.tmax
		- grid_2_timeseries.tmin
- grid_2_timeseries.wind
- grid_2_timeseries.relative_humidity_max 
- grid_2_timeseries.relative_humidity_min

3\. Instrument- or software-specific information needed to interpret the data:

IDE: R studio 4.2.2
Programming language: R
Workflow Packages: {strex} {tidyverse} {lubridate}
The packages are sourced in packages.R, but may need to be installed prior to use.
Shiny App Packages: {shiny} {shinydashboard} {tidyverse} {leaflet} {shinycssloaders} {markdown} {fresh} {gridExtra} {zip}
These packages do not need to be installed for using the interactive online application, but are here as reference to what was used for the process.

4\. Standards and calibration information, if appropriate: Not Applicable

5\. Environmental/experimental conditions: Not Applicable

6\. Describe any quality-assurance procedures performed on the data: 

Checks still planned to be built in.

7\. People involved with sample collection, processing, analysis and/or
Submission: Not Applicable

**DATA-SPECIFIC INFORMATION FOR:** 

\[FILENAMES\] CanESM2_rcp45, CanESM2_rcp85, MIROC_rcp45, MIROC_rcp85, CNRM_CM5_rcp45, CNRM_CM5_rcp85, HADGEM2ES_rcp45, HADGEM2ES_rcp85

Each of these files contain the same structure as below, while varying with the values for each based on the climate model and assumed rcp.

1\. Number of variables: 7

2\. Number of cases/rows: 54784

3\. Variable List:
- time: YYY-MM-DD
- max_temp: in degrees Celsius
- min_temp: in degrees Celsius 
- min_humidity: percent 0-1
- max_humidity: percent 0-1
- wind: meters per second
- precip: kilogram per meter squared per second

4\. Missing data codes: No missing data in the CalAdapt dataset

5\. Specialized formats or other abbreviations used: Not applicable
