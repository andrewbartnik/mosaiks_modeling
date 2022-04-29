# CropMOSAIKS Modeling Repository

## Purpose

The Modeling repository contains code for utilizing the features created in the Featurization repository, or downloaded from the [MOSAIKS API](https://nadar.gspp.berkeley.edu/home/index/?next=/portal/index/). Random Convolutional Featurization produces features that are agnostic to the task a user is interested in modeling. The CropMOSAIKS team has focused on modeling crop data, but these same features could be used to make prediction on forest cover, population, income, and many other variables. The key element to building a model is the data which the user needs to supply. This data should be in a standard tabular dataframe, with a spatial component included as column(s) (latitude and longitude) because the supplemnetal data is joined to the features spatially. 

## Datasets

No feature data or crop data is hosted directly in this repository. To request access to Zambia feature data files, please contact the CropMOSAIKS team (individual GitHub accounts with contact information is included at the end of the main organization README). Below we describe the feature data and crop data and in what context it is used. 

### 1. Features

Random Convolutional Features are a way to encode a geospatial location with information based on the satellite image of that location. These features reflect information such as landscape colors, delimination between colors (like the edge of a field, forest, or building that appears as a line from space), and combinations of colors such as red next to green. In a feature data frame, each row represnts an image, and each feature represents a column. Each cell contains a numerical value for that feature at that location, which is later statistically coorelated with the numerical value of crop yield data for that location during the modeling step (or other data provided by the user). Random Convolutional Features can either be created from the featurization repository or downloaded from the MOSAIKS API. 

### 2. Crop data (labels)

Zambia maize production are forecast yields in units of metric tonnes/hectare. These units are derived from the expected production reported by the farmers each year in units of metric tonnes, divided by the amount of hectares of farmland in that district. This data was collected by the [Central Statistics Office of Zambia (CSO)](https://www.zamstats.gov.zm/). These data are forecasted from pre-harvest survey data collected in May preceding the harvest season (July-August). The forecast model is conducted in Stata, a general purpose statistical software, and adjusted with post-harvest season survey data. There is an unknown degree of uncertainty in this forecast data as the model process and parameters are unknown.

### 3. Administrative level boundaries

Zambia district level boundaries that match the sub-national crop yield data. These are used for finding which spatial points fall within the district boundaries to then summarise the features to the district boundary level. 

### 4. Crop area (weights)

For weighted averages or simple spatial masking. We spatially mask for crop area in the Modeling repository in order to optimize our model for crop yields. This data is specific to our task, and other spatial data should be applied if a user is interested in spatially masking for another task. A portion of the cropped area that remains after the mask is applied overlaps with certain cells in our subsetted unform grid. During the modeling process later, the crop land percentage in each cell determines the weight of the area in the model. More cropland in a cell translates to more weight in the model because that land contains more critical feature information. 

## Requirements

Most modern personal computers will be able to run the modeling notebook. Despite this there is a minimum ammount of comfort with python needed in order to use or adapt this code responsibly, including installing python and managing environments. 

A properly configured python environment can be created through the provided `environment.yml` file. To build this environment open a terminal and run 
```bash
conda env create -f environment.yml
```
Then activate the environment with 
```bash
conda activate mosaiks
```
Finally open this repository in Jupyter Lab by running 
```bash
jupyter lab
```

## Getting Started

There are two primary options to getting started, connecting to the MEDS server `taylor.bren.ucsb.edu`, or using personal compute. 

### 1. Taylor
The notebooks are currently configured to be used on Taylor with file paths that lead to persistent data storage with features, administrative boundaries, crop area weights, and the crop yield data. 

### 2. Personal Compute
To use personal compute, first clone this repository and configure your environemnt as described above. Following this, adjust the file paths in the top of the document to reflect your data directory location. This repository maintains the structure of the data sub folders and it is recomended to use this structure for your own data. If you are unable to produce your own features, pre-compiled features can be downloaded from the [MOSAIKS API](https://nadar.gspp.berkeley.edu/home/index/?next=/portal/index/).

## Notebooks

It is possible and even likely that the user supplied data will be of lower resolution than the feature data. 
Modeling, rasters

## Constraints

While most personal computers are able to run this analysis, users may still be constrained by the scope of their analysis (i.e., the number of features, the number of points, and the length of time) that is being modeled. It is possible to expand these variables sufficiently to push a persoanl computer past its resources. system monitoring may be needed, and it may be neccessary to implement aggresive memory managment strategies. 

## Future Work

Suggestions on how to expand... We plan to expand this section towards the end of the project when we have a better idea of the current scope and the best ways to expand.

## Contributing

code of conduct, access, API, etc
