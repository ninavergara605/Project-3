# Predicting Water Well Conditions in Tanzania 
 
**Author**: *Nina Vergara*
  
## Overview
- [Modeling Goals](Modeling-Goals)
- [Data](Data)
   - [Data Dictionary](Data-Dictionary)
- [Methods](Methods)
- [EDA Results: Notable Features](EDA-Results-Notable-Features)
  - [Construction Year](Construction-Year)
  - [Extraction Mechanism](Extraction-Mechanism)
  - [Management Group](Management-Group)
  - [Water Quality](Water-Quality)
- [Modeling Results](Modeling-Results)
- [Conclusions](Conclusions)
- [For More Information](For-More-Information)
- [Repository Structure](Repositroy-Structure)
  

## Modeling Goals
A Non-Profit Organization would like to allocate resources to Tanzania. They require a precise way to identify communitites that wells that are non-functioning, or in need of repair.
 
## Data
A total of 74,250 records were extracted from Taarifa, an open source platform that aggregates data collected by volunteers and the Ministry of Water. This particular subset of Taarifa data was accessed through the Driven Data- Pump it Up: Data Challenge. This dataset includes 38 features, which give information on location, well mechanisms and management systems, as well as surrounding population numbers.

 #### Data Dictionary
    Data Dictionary *kc_house_data.csv*
    
    
## Methods
#### Data Cleaning
For continuous features, values that were above 3.5 standard deviations from the training set mean were replaced with the training median. These columns were also scaled. The training set median was also used to impute the 'gps_height' column. For categorical features, missing value placeholders were identified and replaced with 'missing'. 

A tree-like structure was made from the categorical training set data by linking words if one was a substring of another. The bottom level(n-1) words were grouped with the second lowest level(n-2). The value that appeared at a higher frequency was used to rename the lower frequency word. This was applied to categorical columns that contained more than a thousand unique entries. These columns in the test dataset were also categorized using the training set decision tree.

#### KNN Feature Engineering
To utilize the location data, namely the 'latitude', 'longitude', and 'gps_height' features, a KNN algorithm was devised to create new features based on the 5 nearest neighbors of any one point. For the initial creation of the new features, the well condition labels (y_train) of the closest neighbors for a given point were extracted. For each condition, probabilities were created by dividing the represented frequency by the total number of neighbors.

In order to pair these training features for the test dataset, each test point was paired with the closest training set value, and the new features were transfered.
    
## EDA Results Notable Features
 
### Construction Year
![images](https://github.com/ninavergara605/Project-3/blob/e93380f36bd3007db2ea35ba42ce1c2f8e7be318/images/construction%20year%20new.png)
 
As the construction year approaches present day, the well has a higher probability of being functioning. The inverse is also true in that well age is negatively correlated with the probability of the well having a non-functioning status.

### Extraction Mechanism
![image](https://github.com/ninavergara605/Project-3/blob/e93380f36bd3007db2ea35ba42ce1c2f8e7be318/images/Extraction%20Mechanism%20new.png)

Extracton Mechanisms seem to have an effect on the condition of a well. Needs-repair wells are present in a much higher proportion for Gravity Extraction wells when compared to the other condition types. Motor Pump and Other extraction wells tend to be non-functional.

 
### Management Group

![image](https://github.com/ninavergara605/Project-3/blob/e93380f36bd3007db2ea35ba42ce1c2f8e7be318/images/management%20new.png)

Management groups seem to be an excellent indicator of well conditions. The functional wells have the a majority presence in the Private Operator and Trust management groups. Wells that are tended by Companies and Schools tend to be Non-Functional. If a well is tended by a Company, School, or Private Operator, theyre least likely to Need-Repair.
 
### Water Quality

![image](https://github.com/ninavergara605/Project-3/blob/e93380f36bd3007db2ea35ba42ce1c2f8e7be318/images/Quality%20New.png)

Water Quality also influences the condition label of a well. Colored wells are more likely to be labeled as Needs-Repair while Dry and Milky have very little Needs-Repair classifications. Surprisingly, the 'Good' category doesn't have the Functional classification as it's majority class. This indicates that other characteristics, like extraction mechanism, are at play.
    
 
## Modeling Results


## Conclusions

    

## Repositroy Structure
 ```
├── data.zip                            <- Zipped data file (please unzip before running scripts)
├── images                              <- Images that were used in the presentation                                            
├── water_well_classification           <- Script folder
   └── EDA.ipynb.                       <- EDA Notebook and results
   └── data_cleaning.ipynb              <- Data cleaning notebook
   └── feature_engineering.ipynb        <- Categorization tree and KNN feature engineering notebook
   └── models.ipynb                     <- Modeling notebook
├── Water Well Presentation.pdf         <- PDF of an EDA Project Presentation                       
└── README.md                           <- The README.md

```
