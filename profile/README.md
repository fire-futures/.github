# Automating Climate Scenario Creation for Wildfire Modeling
<p align = "center">
<img src="https://github.com/fire-futures/.github/assets/63022802/1910f415-93f7-4ba6-9e3e-0eba6379c373" alt="Bren Logo" width="100">
</p>
This github contains the Master's Capstone Project associated with the Masters of Environmental Data Science at the University of California, Santa Barbara - Bren School of Environmental Science & Management. A configurable workflow as an R Markdown document, code to run this workflow as an interactive shiny application, and educational visualizations are included in this github. In this workflow, we demonstrate a process for creating a range of unique climate scenarios by stitching together pieces of existing climate model projections

## Fire Futures Team 
<img width="116" alt="FireFutures_Logo_white" src="https://github.com/fire-futures/.github/assets/63022802/af9f299f-c4a6-430c-9758-4bd2fe03acef">

Name: Victoria Cutler  
Institution: UCSB  
Email: victoriacutler@bren.ucsb.edu

Name: Erica Dale  
Institution: UCSB  
Email: ericadale@bren.ucsb.edu

Name: Mallory Giesie  
Institution: UCSB  
Email:mallorygiesie@bren.ucsb.edu

Name: Lewis White  
Institution: UCSB  
Email: lewiswhite@bren.ucsb.edu


Faculty Advisor: Dr. Naomi Tague  
Institution: UCSB Tague Team Lab  
Email: ctague@bren.ucsb.edu 

This project was part of a larger project within the Tague Team Lab, supported by the Moore Foundation.

## Data & File Overview
This project was developed from 2023-01-01 to 2023-06-09. The original data used for cleaning and organizing the workflow was obtained in January 2023 from CalAdapt. This data covers regionally California and surrounding states, including Nevada, Arizona, and Oregon. The application is connected via API to the 4 priority models within the LOCA Downscaled CMIP5 Climate Projections. Each priority model has options for two emission assumptions, RCP 4.5 and RCP 8.5, thus 8 total models. The application is limited to using this data with an API however, user-input data frames into the configurable workflow are not constrained to this geographic range. 

The original CalAdapt data that the workflow was based off can be found at https://cal-adapt.org/data/download/.

**FILE OVERVIEW**

The current file organization, shown below, is organized into several repositories containing appropriate folders and files. These repositories include data cleaning, workflow of building climate scenarios, educational visualizations, and the final shiny application.

<img src="https://github.com/fire-futures/.github/assets/63022802/5df1cea9-4c44-4f9a-b995-38ac01e4f6ee" alt="repoorganization" width="400">

## Methodology and Use

**METHODOLOGICAL INFORMATION**

Data acquisition: Within the Shiny Application, the Cal-Adapt API collects the data utilizing user-inputs on model, RCP, and grid cells desired. Otherwise, in the workflow the user will input a dataframe of their own matching the necessary parameters.

Data cleaning: This process prepares the data frame with steps to match units, such as converting temperature from Kelvin into Celcius.

Criteria selection: Within the markdown, a user will follow steps to upload their variable criteria for each season or year they would like to build. Alternatively, within the application, a user can explore interactive graphs to see each climate variable distribution, which might prove useful in creating the criteria table.

Filtering: The climate model will be filtered by 'segments', the segments can be defined as either years or seasons (based on wet or dry periods of the wet year). The criteria tables are used to search for and identify matching years/seasons that match specified climate characteristics of interest. Each criteria table may have numerous matching time periods, these are all saved as a list of lists.

<img width="275" alt="image" src="https://github.com/fire-futures/.github/assets/63022802/80942970-af19-4915-8991-b128183a61ce">

Randomly select: If multiple years/seasons meet the criteria, a random sample of the available segments is selected, allowing for a variety of scenarios that fit the same baseline criteria. The result is a series of seasons or years, one per criteria table.  

Cutting and stitching: The resulting segments are then joined together to form a continuous time series with daily values for the climate variables of interest. Going in order of the list, each time period is cut from the original data frame and added to a new data frame. 

<img width="365" alt="image" src="https://github.com/fire-futures/.github/assets/63022802/600ecb2e-65b8-44ad-9b19-502f25461a4f">

Output Files: The resulting time series for each climate variable (min/max temperature, precipitation, wind speed, and min/max humidity) are then output into a csv file and time series files for each variable. The data frame is converted into time series files beginning with the desired start date followed by the variable measurements. Each variable has its own time series file, with appropriate file extensions.  

Grid cell loop: Each grid cell loops through the cutting, stitching, and time series steps using the same series of seasons/years determined by the original sample cell in the randomly select function.

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


**CUSTOMIZABLE WORKFLOW USE DETAILS**

For users following the workflow with their own data, the Manual-Workflow folder has the creating-scenarios-workflow.Rmd document to walkthrough which sources all of the files in the Functions folder. To use this process, the workflow file and functions folder must be accessible together. Multiple grid cells/data frames can be selected for this workflow, and must each be entered as their own data frame. One grid cell will need to be selected as the primary cell for selecting a matching criteria list, the resultant series of selected date ranges will then be applied to the rest of the grid cells.

Data must be organized as daily values with the column names and units as:
- time: YYY-MM-DD
- max_temp: in degrees Celsius
- min_temp: in degrees Celsius 
- min_humidity: percent 0-1
- max_humidity: percent 0-1
- wind: meters per second
- precip: kilogram per meter squared per second

**SHINY APPLICATION USE DETAILS**

The Automated-App folder contains the build for the interactive online application. This can be run through R-studio by opening the ui file and selecting "run shiny".  It will also be deployed via the Tague Team Lab.
There are two tabs on this application: The welcome tab has further information on use and a map that can be explored to find CalAdapt grid cell numbers. The build tab provides steps to select and explore the climate model predictions and to build a climate scenario.



**SOFTWARE REQUIREMENTS**

IDE: R studio 4.2.2

Programming language: R

Workflow Packages: {strex} {tidyverse} {lubridate}

The packages are sourced in packages.R, but may need to be installed prior to use.

Shiny App Packages: {shiny} {shinydashboard} {tidyverse} {leaflet} {shinycssloaders} {markdown} {fresh} {gridExtra} {zip}

These packages do not need to be installed for using the interactive online application, but are here as reference to what was used for the process.





This README.txt file was generated on 2023-06-05 by Erica Dale, Victoria Cutler, Mallory Giesie, Lewis White.

MIT License
Copyright (c) [2023] [Automating Climate Scenario Creation for Wildfire Modeling]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
