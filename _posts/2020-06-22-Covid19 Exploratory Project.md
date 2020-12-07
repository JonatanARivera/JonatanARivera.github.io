---
layout: post
title:  Data Exploration Project
subtitle: 
cover-img: /assets/img/path.jpg
tags: [books, test]
---

![alt text](https://github.com/JonatanARivera/JonatanARivera.github.io/blob/master/assets/img/COVID-map.png)


# Is There an Association between Population and Covid-19 Deaths Per U.S county?


In this project, I attempt to answer a basic question: is the population associated with Covid-19 deaths per U.S counties? 
From the 3D Scatter plot I made below, we can see there is logarithmic growth of Covid-19 deaths for the counties' corresponding population. This simply means, that as the population increases, generally speaking, the number of deaths per county increases as well

<div>
    <a href="https://plotly.com/~jonatan5696/21/?share_key=vB5rxfmNkBSVpbco3FnlZW" target="_blank" title="Final_PopCovidDeathsJune14" style="display: block; text-align: center;"><img src="https://plotly.com/~jonatan5696/21.png?share_key=vB5rxfmNkBSVpbco3FnlZW" alt="Final_PopCovidDeathsJune14" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plotly.com/404.png';" /></a>
    <script data-plotly="jonatan5696:21" sharekey-plotly="vB5rxfmNkBSVpbco3FnlZW" src="https://plotly.com/embed.js" async></script>
</div>

Yellow points represent deaths over 100 ; also the size of points represents the amount death toll relative to other counties

## A BIGGER POPULATION DOES NOT ALWAYS EQUAL MORE DEATHS

<div>
    <a href="https://plotly.com/~jonatan5696/26/?share_key=gsYWWjaCPhjTM1hhx0tqGK" target="_blank" title="NewYorkVSCalifornia" style="display: block; text-align: center;"><img src="https://plotly.com/~jonatan5696/26.png?share_key=gsYWWjaCPhjTM1hhx0tqGK" alt="NewYorkVSCalifornia" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plotly.com/404.png';" /></a>
    <script data-plotly="jonatan5696:26" sharekey-plotly="gsYWWjaCPhjTM1hhx0tqGK" src="https://plotly.com/embed.js" async></script>
</div>


From the scatter plots above we can see that New York State has several counties, represented as points, which on average have a bigger death toll compared to counties in California, despite California having a bigger population! This means that we can infer that the population alone, despite the correlation mentioned above, does not necessarily determine the death toll in counties. Other factors are very likely to play a role too.

## HOW LATE SOCIAL DISTANCING POLICIES ARE IMPLEMENTED, MAY HAVE A ROLE IN CONTRIBUTING TO THE NUMBER OF DEATHS

One possible explanation for the higher death toll in some counties more than others, despite differences in population, could be due to how late a county implements social distancing policies. For example, Los Angeles County and New York City implemented stay at home policies as late as 4 weeks after their first reported cases of Covid-19, in their respective regions (1); which compared to the Bay Area in Northern California is late, having implemented policies 2 weeks earlier (1). Also, the staggering differences between these two states could also have to do with how late the statewide home orders were executed, which in New York, came about five days later after California's order(2).


<div>
    <a href="https://plotly.com/~jonatan5696/35/?share_key=NTwlC5hrhEC8CochwlCZTJ" target="_blank" title="Florida" style="display: block; text-align: center;"><img src="https://plotly.com/~jonatan5696/35.png?share_key=NTwlC5hrhEC8CochwlCZTJ" alt="Florida" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plotly.com/404.png';" /></a>
    <script data-plotly="jonatan5696:35" sharekey-plotly="NTwlC5hrhEC8CochwlCZTJ" src="https://plotly.com/embed.js" async></script>
</div>

Another example, of how implementing a social distancing policy late might impact a county's Covid-19 timeline, is Hillsborough County in Florida. The trend was similar to that noted above, the earlier the social distancing procedures were implemented, the less the death toll was for the respective county. For example, Hillsborough County implemented its 6-feet distancing practices on March 17, 2020, approximately 2 weeks after the first two reported cases in Florida (3). However, a county with similar population size Palm Beach County in Florida didn't implement its social distancing policy until March 22, 2020, or about 5 days after Hillsborough County (4). These 5 days late into the implementation of the social distancing policy, possibly, might have contributed to the more deaths in Palm Beach compare to Hillsborough.

So, conclusively, there is an association between population and deaths per county, but there are likely more factors affecting how fast Covid-19 spreads, and as crucially, how many deaths occur per county.

Limitations: One limitation is the amount of available data reported on Covid-19 deaths by U.S. Counties in my data set; I work with 3,007 counties that had FIPS codes, out of the 3,141 county-equivalents available in the U.S States(5); I had about 26 missing data values, where the county names appear as 'Unknown'. There were also some counties or equivalents such as the 5 boroughs in New York City that were treated as one county by the New York Times. Furthermore, in some instances, these groups or county-equivalents had no FIPS codes associated with them. Lastly, I work data on the deaths and cases of Covid-19 reported up until June 14, 2020, and work with population estimates of counties for 2019 (6,7).

GIT HUB Notebook:
JonRivera/JonRivera.github.io


Sources:
1. https://www.livescience.com/why-covid19-coronavirus-deaths-high-new-york.html
2.https://www.mercurynews.com/2020/04/08/how-california-has-contained-coronavirus-and-new-york-has-not/
3. https://www.hillsboroughcounty.org/en/residents/public-safety/emergency-management/covid-administrative-orders-and-emergency-policy-group
4. http://discover.pbcgov.org/coronavirus/Pages/Orders.aspx
5. https://www.usgs.gov/faqs/how-many-counties-are-united-states?qt-news_science_products=0#qt-news_science_products
6. Covid19 Data Extracted from New York Times Repository: https://github.com/nytimes/covid-19-data/blob/master/us-counties.csv
7. 2019 Population Estimates: 'https://www2.census.gov/programs-surveys/popest/datasets/2010-2019/counties/totals/co-est2019-alldata.csv'
