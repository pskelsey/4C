<p align="left">
  <img width="212" height="166"  src="https://github.com/pskelsey/4C/blob/gh-pages/4CLogo.png">
</p>


# DOCUMENTATION

# Table of Contents
* [Background](#background)
  * [Climate data](#climate-data)
  * [Crop data](#crop-data)
* [Basic operation](#basic-operation)
* [Model Tab](#model-tab)
  * [Create your own model](#create-your-own-model)
  * [Fit a model to your own data](#fit-a-model-to-your-own-data)
  * [Final model selection](#final-model-selection)
* [Projections tab](#projections-tab)
  * [Emissions panel](#emissions-panel)
  * [Landscapes panel](#landscapes-panel)
  * [Dispersal panel](#dispersal-panel)
  * [Plots panel](#plots-panel)
  

## Background
The app uses gridded crop distribution / land use data and gridded climate change data, and allows you to build a weather-dependent model to apply in selected grid cells under various climate change scenarios. A unique feature of the app is the ability to define spatial relationships (e.g., risk of pest or pathogen dispersal) among grid cells via various dispersal options. These spatial relationships can be used to modify projected values. 

### Climate data
The app uses raw monthly 25 km gridded (52 x 39 cells) climate data from the UK Met Office Climate Projections database ([UKCP09](http://ukclimateprojections.metoffice.gov.uk/)) 11-member ensemble of spatially coherent climate projections (SCPs). The SCPs provide the best estimates for modelling and summarising the potential effects of future climates on spatial processes in GB as they are fully coherent across different locations, allowing the user to consider climate change at more than one location in a way that captures the relationship between the different locations,and to average projections across user defined land areas. They include both internal modelling variability (using perturbed physics ensembles) and external modelling variability (from the use of different General Circulation Models, or GCMs), as well as information on climate variability. The SCPs provide 11 equally plausible snapshots of climate change; i.e. a range of 11 future values are provided for each climate variable in each grid cell. UKCP09 1961-1991 baseline data are also included for comparison, i.e. for computing a change relative to the current climate.

### Crop data
Polygon data defining the spatial coverage of crops and land-use types were derived from [IACS](https://ec.europa.eu/agriculture/direct-support/iacs_en), [JACS](http://www.gov.scot/Topics/Statistics/Browse/Agriculture-Fisheries/PubFinalResultsJuneCensus), and [CROME](https://data.gov.uk/data/search?q=CROME). These data cover Scotland and England only. The vector data were rasterised to 25 km grids matching the resolution of the climate change data. Information on the location and area of each crop / land-use type per grid cell is available for use in the app.

## Basic operation
*Tabs*: The app has two 'tabs' - 'Model' and 'Projections.' To switch from one tab to the other just click on their name.  
*Switches*: Drag the circluar switch to the left or right, or just click in the empty space.  
*Drop down lists*: Click on the downward pointing arrow to reveal the list.  
*Numeric fields*: Click in the white box to change the numerical value. Then hit enter or click outside the box.  
*Text fields*: Click in the white box to change the text. Then click outside the box. If you can't, you're not allowed.  
*Buttons*: Click them.  
*Knobs*: Drag the control to around your selection, or click on your selection.  
*List boxes*: Use the scroll bar to the right to reveal more choices. Click on a value to select it - it will be highlighted.  
*Radio buttons*: These are little circles to the left of lists. Click one to select, and it will be highlighted with a black dot.  
*Toggle switches*: These flip up and down. 

## Model Tab
The risk models you create here must be a function of one weather variable only, y = f(x); e.g. crop damage as a function of temperature, infection risk as a function of precipitation, etc. The ability to build models containing more than one weather variable will be included in a future release.  

<p align="left">
  <img src="https://github.com/pskelsey/4C-model/blob/master/docs/modelsTabLarge.png">
</p>

### Create your own model
Select 'Create a model' using the switch.

#### Use a pre-defined function
Select 'Use the list' using the switch. Select a function from the 'Model list' dropdown list. The equation will be displayed in the 'Model description' pane. Adjust the value of the parameters (a, b, c, d) using the numeric fields. The 'lower' and 'upper' fields will be greyed out as these are used for fitting models to data. 

#### Define your own function
Select 'Define my own' using the switch. The 'Use my function f(x) = ' text field will no longer be greyed out and you can now type in the function you want to use. The following rules must be followed when defining your model: (i) do not include the dependent variable, i.e. omit the 'y = ' or 'f(x) = ' part of your equation as this is implicitly assumed; (ii) your equation should be a function of one independent variable only and you must use the letter 'x' for that variable; (iii) [MATLAB notation](https://uk.mathworks.com/help/matlab/matlab_prog/matlab-operators-and-special-characters.html) is required for your arithmetical operators and symbols. If these rules are not followed, an 'Incorrect sytax' warning will occur. 

#### Plotting your model
To visualise your function, adjust the range of your x-variable (minimum and maximum values) and the increment (affects the smoothness of the curve) using the 'x-range' numeric field. The format required is min:step:max, e.g., to plot from 0 to 10 in steps of 0.1 you would enter 0:0.1:10. Click the 'Run' button.

### Fit a model to your own data
Select 'Fit model to data' using the switch. This will open up a file selection dialog box. Your datafile must be an ASCII delimited text file or CSV file with the data stored in columns. The first column should contain the independent- or x-variable (i.e. the weather variable) and the second column the dependent variable. Replicate values of the dependent variable should be stored in subsequent columns. If your file does not meet these requirements then a warning will occur and the app will default back to 'Create a model.' A data file has been provided in the download zipfile ('data.txt') to help you get up and running with the model fitting features. Your data will be plotted once it has loaded successfully. 

To fit a model, select one from the dropdown 'Model list.' The selected model will be displayed in the 'Model description' pane. The grid of 'Parameter' text fields in the top-right corner will adjust according to the model, with unnecessary fields greyed out. Default initial values for the parameters to be fitted are selected uniformly at random from the interval (0,1), or you can set these yourself using the 'initial' text field. Lower and upper bounds on the parameters to be fitted can be set using the 'lower' and 'upper' text fields. Click the 'Run' button to fit the model. The numerical fit results will be displayed in the 'Model description' pane and goodness of fit statistics in the 'GoF' pane. If the model fails to fit a warning will occur, with some suggestions to help improve the fit. The method of least squares (linear or nonlinear) is used when fitting data, or there is an option to fit a smoothing spline in the 'Model list'. Spline is a good option if your data is noisy or you are having trouble fitting other models, although this is considered a non-parametric fit and the display of numerical fit results will be limited. The value of the smoothing parameter for splines is fixed at 0.1. 

### Final model selection
To use a model for projections you must select 'Use this model' with the switch in the bottom right of the tab, changing the lamp from red to green. You can now proceed to the Projections Tab.

## Projections Tab
<p align="left">
  <img src="https://github.com/pskelsey/4C-model/blob/master/docs/projectionsTabLarge.png">
</p>

## Emissions panel
Select your climate variable, future time-period, and CO2 emissions scenario using the knobs. Select the month of the year or the season using the list box. For seasonal averages of the selected climate variable, Spr = spring (MAM), Sum = summmer (JJA), Aut = autumn (SON), and Win = winter (DJF). The climate change data are probabilistic, therefore a range of climate values will be provided for each grid cell (see [Climate data](#climate-data)).

## Landscapes panel
Here you define the distribution of locations (grid cells) that you want to use in your risk assessment. First, the 'Areas' radio buttons (No / Yes) are used to determine whether or not you want the area of the selected crop / land use type within each 25 km grid cell to be incoporated into risk model projections. 'No' = projections are made for every grid cell containing the crop / land use of interest. 'Yes' = projected values are a cumulative total for the area of crop / land use within each grid cell; i.e. risk model value x area x initial density (number per square metre). The latter is suitable for population modelling. When 'Yes' is selected then the numeric field below the radio buttons will become available to enter the initial density of the dependent variable (number per square metre). Some examples of how these radio buttons and the initial density numeric field can be combined for different outcomes:
1. Your risk model describes the impact of a climate variable on disease severity in an experimental unit (e.g. grain kernel, plant, field). To obtain a representative value for future disease severity in each grid cell, select 'No.'
2. Your risk model describes the impact of a climate variable on the density (number per square metre) of a pest or pathogen. To obtain the projected total number in each grid cell, select 'Yes' and set the density field equal to 1.
2. Your risk model describes the impact of a climate variable on the density (number per square metre) of a pest or pathogen in the crop canopy. To obtain the projected total number in each grid cell, select 'Yes' and set the density field equal to the ratio of canopy area to ground area (leaf area index).
3. Your risk model describes the impact of a climate variable on the density of a pest or pathogen using some other 



number of spores per square metre of lesion and you want the projected total number of spores in each grid cell: select 'Yes' and set the density field equal to the proportion 


If 'No' is selected then areas are ignored and the risk model will provide projections for each grid cell containing the crop / land use of interest. If 'Yes' is selected then the risk model will project a cumulative total for the area of crop / land use within each grid cell. The latter is used for population modelling. When 'Yes' is selected then the numeric field below the radio buttons will become available to enter the initial density of the dependent variable (number per square metre). Some examples of 


If your risk model decsribes the the effect of climate on the density of your dependent variable (e.g. pests per square metre of crop cover) and you wish to multiply projected values by the area of crop / land use to obtain the cumulative total per grid cell, then set the initial density to 1. If, however, your risk function describes , and projected values will be multiplied by the area and initial density. This is useful 
average value per grid cell
population modelling, where your risk model describes the effect of climate on the density (e.g. pests) with a climate variable

Yes: risk model = rgr / risk model = no. m^2



'No' will produce a range of projected model values for each grid cell. 'Yes' will provide a cumulative total for the area of crop / land use within each selected cell, for example, if your risk model . If 'Yes' is selected then the numeric field beneath will become available to enter the density

latter is used if you want  are a cumulative total  in each grid cell *i* are weighted by the overall area of the land use type of interest *j* in the distribution of locations, value<sub>i</sub> = value<sub>i</sub> x (regional area of type<sub>j</sub> / regional area of all types).

projected values in each grid cell *i* are weighted
weighted by the relative area of the selected land type in the the distribution of locations


of type i in the region, written as a fraction of all potential  

weighted by the  area of the selected land type, expressed as the fraction of all available land use types 

weighted by the propoetion of each cell occupied by the selected land use type. 

where the total area per cell is the total 

## Dispersal panel


## Plots panel

### Output data
For each future scenario you define, a 'super-ensemble' of projected values is produced (11 SCPs x *n* selected grid cells). These can be saved to an ASCII file, where a new column of data is added for each scenario defined. Each column will contain 22308 values (52 x 39 cells x 11 SCPs). Only a small proporition of these values will be numerical, pertaining to the grid cells you selected for your projections. The rest will be NaN (not a number). These results can be saved to any location you like.



