Proposal
================
Anand Rajan(ar4173), Matt Neky(mjn2142), Joe Kim(jhk2201), Alyssa
Watson(aw3253), Yoo Rim Oh (yo2336)

## Project Title

The Effect of Concentrations of Various Air Pollutants on Cancer
Prevalence at the State Level over Time

## Motivation for Project

Given the rapid progression of climate change, we have seen deleterious
consequences on population health in the United States, specifically
increased burden of cancer. Prior research has shown that air pollution
is associated with the increase in incidence and mortality related to
certain cancers. Thus, we want to take a closer look at trends of levels
of major air pollutants, such as NO2, SO2 and 03, and compare these
trends to incidence and mortality cancer data at the state level over
time. The cancers we will specifically be looking at are lung cancer,
pancreatic cancer, and liver cancer. We chose these cancers based on
previous clinical research that suggest associations between air
pollutant concentrations and incidence/mortality of these specific
cancer types. Thus our motivation is to further analyze and evaluate
these associations at a population level over time.

## Intended Final Products

We plan to publish our final project by constructing a website. The
website will contain a background summarizing previous clinical research
regarding the associations between lung, liver and pancreatic cancer to
air pollutants. We evaluate the depth of analysis of current literature,
and address where there could be possible gaps. Furthermore, we intend
to have a methods tab that describes the source of our data sets and
display the code that was involved in cleaning, combining and
stratifying our final data set. For this project, we anticipate merging
multiple data sets in order to conduct necessary analysis. Moreover, our
results section will be split into two portions. One will moreso be
focused on numerical analyses and tables, whereas another section will
be dedicated towards data visualization. For the data visualization we
expect to create a flex dashboard. Finally, we will have a section
dedicated to conclusions, limitations, and recommendations for future
research.

## Anticipated Datasources

Thus far, we have gathered data from two main sources. Regarding cancer
statistics, we retrieved data from
<https://cancerstatisticscenter.cancer.org/#!/> The three data sets give
us information on mortality data, trends of mortality related to various
cancers over timeand incidence rate of various cancers at the state
level. According to the file and website, the data source is the North
American Association of Central Cancer registries. I have attached the
data sets in the following code chunk.

``` r
incidence_df = 
  read_excel("data/incrate.xlsx", skip=6, sheet=2)

deathrate_df = 
  read_excel("data/deathrate.xlsx", skip=6, sheet=2)

deathtrend_df = 
  read_excel("data/deathtrend.xlsx", skip=6)
```

The second data set is air pollution data in the United States from 2000
to 2016. The data was gathered by the EPA and measures air pollutant
concentrations(in ppb) for major pollutants, such as Sulfur Dioxide and
Ozone, at the city/county level. Now this is an extremely large data set
with over 174,000 observations and as you can see will require much
cleaning.

## Planned Analyses and Data Visualization

We intend to include both comprehensive numerical analyses and various
data visuals. First we will evaluate the air pollutant data and come up
with figures that display average pollutant concentration by state over
time. Given the raw data set has values measured at the city/county
level, we will have to run numerical analyses to find average pollutant
concentration by state. In this table we will also include other
statistics such as variance and range. With this figure we can create
multiple visualizations, such as a plot the trend of specific air
pollutant concentration over time by state, or stratify it by type of
pollutant. We can do the same with mortality data for cancer over time
by state. Furthermore, we can run linear regressions comparing pollutant
concentration to incidence rate of specific cancer types. The linear
regression models would fall in the numerical analyses section.
Moreover, other analyses include gender specific stratification and
whether there are differential effects on

## Challenges

The major challenge of this coding project will be mainly around
cleaning and merging the data sets. As you can see the data sets are
fairly messy and we need to clean the observations while reasonably
merging the data sets. This will require a lot of time and manipulation
of the raw data. Once we are able to effectively tidy the data, running
basic analyses and visuals should not be too difficult. However creating
regression models maybe a tad difficult given the data sources we are
merging and the possible incongruities of years of data collected. Until
we get to coding/cleaning the data will we know the extent of
regressions we can run with the given data.

## Timeline

11/13 - Turn in Proposal 11/23 - Set up website infrastructure and
complete data cleaning 11/28- Complete Numerical Analysis 12/3 -
Complete Data Visualization 12/4-9 - Complete website, work on report
and explanatory video 12/10- Final edits to website and report 12/11-
Turn in report, repo/website, and video
