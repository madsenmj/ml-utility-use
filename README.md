# Machine Learning Demonstration

A machine learning demonstration predicting the Los Angeles utility usage. This project uses data from the Los Angeles [Open Data repository](data.lacity.org/A-Livable-and-Sustainable-City/Water-and-Electric-Usage-from-2005-2013/asvq-scwp). 

# Project Documentation

There is a [PowerPoint presentation](/docs/LA_Utility_Demo.pptx) that describes the entire project. The project is also described in a [YouTube video presentation](https://youtu.be/ryEMlsaQazg). A [PowerBI dashboard](/docs/LA_utility_project.pbix) visualized the zip-code data.

# Project Data

There are four primary data sources described in the data enrichment notebook: [LA_Utility_Data_Enrichment](/src/LA_Utility_Data_Enrichment.ipynb). They include:

### LA Utility Data
I am using data from the city of Los Angeles originally found from [this website](
https://data.lacity.org/A-Livable-and-Sustainable-City/Water-and-Electric-Usage-from-2005-2013/asvq-scwp).

The dataset has four columns of interest:
1. The month in which the data was recorded
2. The zip code (geographical location) for the data
3. The water use for that zip code (measured in HCF)
4. The power use for that zip code (measure in kWh)
The raw data has another column (Value Date) that we will not be using. I first examine the raw data.

### Population Data
The population data was retrieved from the US Census Bureau.
> https://www.census.gov/geo/maps-data/data/zcta_rel_download.html

The dataset includes information about the population, the land area, and the total area for each zip code. There are a number of other columns of data that I will not use. I convert the zip code column (ZCTA5) to an integer in order to match the datatype of my power/water usage dataframe zip code.

### Economic Data

I add the economic data which is based on IRS tax records:
> https://www.irs.gov/uac/soi-tax-stats-individual-income-tax-statistics-zip-code-data-soi

This dataset has the following variables I am interested in:
* Nreturns: number of filed tax returns
* AGI: adjusted gross income (in thousands of \$)
* SW: Salary and Wages (in thousands of \$)
* EIC: total earned income tax credit (in thousands of \$)

However, the dataset is originally an Excel spreadsheet with multiple sheet names. I created a short function to retrieve the tax data I want.

### Weather Data

I add historical weather data to my input features. This dataset comes from:

> https://www.ncdc.noaa.gov/cdo-web/search?datasetid=GSOM

The dataset has the following variables:

* AWND: average wind speed (m/s)
* CLDD: cooling degree days
* HTDD: heating degree days
* PRCP: preciptiation (cm)
* TSUN: daily total sunshine
* TAVG: Average daily temperature (celsius) [Not Used]

The weather data is essentially the same for all of the zip codes in this dataset- they are all in the city of Los Angeles. Any small variation in the rain or temperature will be negligible because I only have the average over the full month of data.

# Project Source

The machine learning is divided into two parts:
1. [Data cleaning and exploration](/src/LA_Utility_Data_Enrichment.ipynb)
2. [Machine learning and testing](/src/LA_Utility_Predicting_Power_Needs.ipynb)

