Proposal
================
Anand Rajan (ar4173), Matt Neky (mjn2142), Joe Kim (jhk2201), Alyssa
Watson (aw3253), Yoo Rim Oh (yo2336)

## Project Title

The Effect of Concentrations of Various Air Pollutants on Cancer
Prevalence at the State Level over Time

## Motivation for Project

Given the rapid progression of climate change, we have seen widespread
effects on the environment, many of which have deleterious consequences
on population health, including increased burden of cancer. Prior
research has shown that air pollution is associated with the increase in
both incidence and mortality for certain cancers. Thus, we want to take
a closer look at trends of levels of major air pollutants, such as NO2,
SO2, and 03, and compare these trends to incidence and mortality cancer
data by state, with respect to time. The cancers we will specifically be
looking at are lung cancer, pancreatic cancer, and liver cancer. We
chose these cancers based on widely held beliefs by researchers and
clinicians that suggest stronger associations between air pollutant
concentrations and incidence/mortality of these specific cancer types as
opposed to other forms of cancer. Our motivation for this project is to
to more robustly investigate the aforementioned theories by further
analyzing and evaluating the associations between pollutants and lung,
pancreatic, and liver cancers at the population level with respect to
time.

## Intended Final Products

We plan to publish our final project by constructing a website. The
website will contain a background summarizing published research
regarding the associations between lung, liver and pancreatic cancers to
air pollutants. We evaluate the depth of analysis of current literature,
and address where there could be possible gaps. Furthermore, we intend
to have a methods tab that describes the source of our data sets and
display the code that was involved in cleaning, combining, and
stratifying our final data set. For this project, we anticipate merging
multiple data sets in order to conduct necessary analysis. Moreover, our
results section will be split into two portions. One will moreso be
focused on numerical analyses and tables, whereas another section will
be dedicated towards data visualization. For the data visualization, we
expect to create a flex dashboard. Finally, we will have a section
dedicated to conclusions, limitations, and recommendations for future
research.

## Anticipated Datasources

Thus far, we have gathered data from two main sources. Regarding cancer
statistics, we retrieved data from
<https://cancerstatisticscenter.cancer.org/#!/> The three data sets give
us information on mortality data, trends of mortality related to various
cancers over time and incidence rate of various cancers at the state
level. According to the file and website, the data source is the North
American Association of Central Cancer registries. I have attached the
data sets in the following code chunk.

``` r
incidence_df = 
  read_excel("data/incrate.xlsx", skip = 6, sheet = 2)

deathrate_df = 
  read_excel("data/deathrate.xlsx", skip = 6, sheet = 2)

deathtrend_df = 
  read_excel("data/deathtrend.xlsx", skip = 6)
```

The second data set is air pollution data in the United States from 2000
to 2016. The data was gathered by the EPA and measures air pollutant
concentrations(in ppb) for major pollutants at the city/county level.
This is an extremely large data set with over 174,000 observations and
will require extensive cleaning, so it was not uploaded at this time due
to size limitations..

Though not uploaded the following is a brief description of the data
set(<https://data.world/arajan98/data-science-project-proposal/workspace/project-summary?agentid=data-society&datasetid=us-air-pollution-data>):

Includes four major pollutants (Nitrogen Dioxide, Sulphur Dioxide,
Carbon Monoxide and Ozone) and each has 5 specific columns. For example,
for NO2:

-   NO2 Units : The units measured for NO2
-   NO2 Mean : The arithmetic mean of concentration of NO2 within a
    given day
-   NO2 AQI : The calculated air quality index of NO2 within a given day
-   NO2 1st Max Value : The maximum value obtained for NO2 concentration
    in a given day
-   NO2 1st Max Hour : The hour when the maximum NO2 concentration was
    recorded in a given day

## Planned Analyses and Data Visualization

We intend to include both comprehensive numerical analyses and various
data visuals. First we will evaluate the air pollutant data and come up
with figures that display average pollutant concentration by state over
time. Given the raw data set with city/county level measurements, we
will have to run numerical analyses to find average pollutant
concentration by state. In this table we will also include other
statistics such as variance and range. With this figure, we can create
multiple visualizations including, but not limited to a plot tracing the
trend of specific air pollutant concentration over time by state and/or
comparing the data stratified by type of pollutant. Similar workflow
will be applied to the mortality data for cancer over time by state.
Furthermore, we can run linear regressions comparing pollutant
concentration to incidence rate of specific cancer types under the
numerical analyses section. Additionally, with the available data
stratified by sex and race/ethnicity, visual representation of cancer
incidence/death rate trend can be provided as reference.

## Challenges

The major challenge of this coding project will be mainly around
cleaning and merging the data sets. As you can see the data sets are
disorganized and we need to clean the observations while reasonably
merging the data sets. This will require a lot of time and manipulation
of the raw data. Once we are able to effectively tidy the data, running
basic analyses and visuals should not be too difficult. However creating
regression models may be a tad difficult given the data sources we are
merging and the possible incongruities of years of data collected. Until
we get to coding/cleaning the data will we know the extent of
regressions we can run with the given data.

## Timeline

| Date   | Plan                                                     |
|:-------|:---------------------------------------------------------|
| 11/13  | Turn in Proposal                                         |
| 11/23  | Set up website infrastructure and complete data cleaning |
| 11/28  | Complete Numerical Analysis                              |
| 12/3   | Complete Data Visualization                              |
| 12/4-9 | Complete website, work on report and explanatory video   |
| 12/10  | Final edits to website and report                        |
| 12/11  | Turn in report, repo/website, and video                  |
