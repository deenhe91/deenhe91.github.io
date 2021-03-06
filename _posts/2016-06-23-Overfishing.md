---
layout: post
title: overfishing
excerpt: "Keystone project: Building an overfishing app and raising awareness."
categories: [Metis Projects]
comments: true
image: 
  feature: http://www.greenpeace.org/international/Global/international/photos/oceans/2014/GP04BW5.jpg 
  credit: 
  creditlink: 
---
### The final stretch

here's a link to a pdf of the final presentation I gave on career day, 23rd June: [link.](https://github.com/deenhe91/fish_app/blob/master/fish_.pdf)

Overfishing is one of the biggest and most neglected issues of our time. The oceans play a crucial role in maintainig a stable atmosphere and also provide food for billions of people on earth. Maintaining a healthy ecosystem is important everywhere, but in the oceans, an unbalanced and collapsing ecosystem results in substantial effects on the levels of CO2 in our atmosphere and thus has catastrophic effects, not just for economies that rely on fishing to sustain them, but also for fish populations and ultimately our environment.

For my final project at Metis, I clustered fish species into levels of threat, and used these in an [app](github.com/deenhe91/fish_app) so that users can input the name of a fish and find out how threatened or overfished that species currently is.

I got my data from [NOAA](http://noaa.gov), which provided information on over 500 species of fish over an average of 60 years.

I also collected data from the [WCPFC](https://www.wcpfc.int) and did some analysis on that which I'll talk about later.


### Exploratory Analysis

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/IMG_20160610_113730.jpg?raw=true)

Amidst the many groupbys and pyplots a very clear pattern emerged. Most of these fish populations are severely declining. It was quite shocking to view such an obvious trend. 

Here is a plot of the aggregated 'exploitation rate' of all tuna types in the data set, over time. It is a simple measure of the proportion of a population that is caught. So you can see that the percentage of the population caught has increased dramatically over the past 60 years.

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/ERTuna.png?raw=true)

This could be because total catch has increased, or because the population size has decreased. When we look at plots of catch rates, which is essentially how much fish is caught per unit effort, you can see that this is decreasing...

BIG EYE

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/BET_meancatchrate.png?raw=true)

ALBACORE

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/ALBmeancatchrate.png?raw=true)

YELLOWFIN

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/YFTmeancatchrate.png?raw=true)


This indicates that the number of available tuna have dropped, and not just that we're getting better at catching them.

#### By month, By region, By fish? Fuzzy-Matching

I used the fuzzy matching python package `fuzzywuzzy`, to pull out fish by region. First I used fuzzywuzzy to detect all fish in Pacific and Atlantic regions and then `numpy.where()` to pull out indices of all the fish in those regions.

I made separate dataframes for Pacific and Atlantic fish to analyse the differences in overfishing between the two major oceans. 

- more to come here -

#### Missing Data

This is just one snapshot of the data I had, namely the mean mortality rate (over the 60 year time period) of fish species in the Pacific...

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/missingdata.png?raw=true "Pacific")

...and Atlantic oceans.

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/missingdata2.png?raw=true "Atlantic")

You can't glean an awful lot from these plots, but it shows you just how much data is missing, especially in the Pacific. Some fish had information on total catch, others had information on available biomass or mortality rate. Some had no information at all. 

I tried using `PyBrain` to fill in these gaps with a recursive neural network.


#### Apping

This part required some serious readjustment of my understanding of the internet It was a really enjoyable and fascinating task. I'll do a post on understanding app buidling in the next couple of weeks with a link to the live web app. In the meantime you can have a gander at the app format on my [github page](https://github.com/deenhe91/fish_app).

I built a fish-specific search tool with a little help from [Joe Oliver]() that would allow people to find out how overfished a fish population is. The idea is also to provide alternatives and more of a dashboard breakdown which I am working on right now.

I clustered the fish into different categories of 'threat level' or overfishedness using KMeans Clustering in `SciKitLearn`. I used fishing rate, population size and an indicator of the health of the population (the rate of growth in the last 5 years) as variables.

![](https://github.com/deenhe91/deenhe91.github.io/blob/master/images/cluster.png?raw=true)

I wanted to use 'length at age' as a variable because that is a good measure of a healthy fish population, but it looks like getting that information for all the fish species I was working with would be a much longer process than I had the time for in this project.

The  clusters:

RED - overfished and dwindling/unhealthy population, do not eat.

ORANGE - low population size but not necessarily over-fished, treat with caution.

GREEN - healthy population and not overfished, bon apetit!



### Further info and efforts

With a bit of digging on the interweb I found countless organisations, listed at the bottom of this post, who are feverishly campaigning and recruiting to tackle these problems. 

The Seawatch app, this is very similar to what I have done, but with more time, money and manpower. However, they don't show the changes in the fish and this is a pretty useful chunk of information for the public to digest. It is far more impactful if someone says, "don't eat this fish, look here's why", than just, "don't eat this fish." In the same way you want to educate your children on _why_ they can't go around hitting things, or eat an entire bowl of haribo. That reaction to evidence stays an important influencer of our behaviour and in this way, data visualisations can be completely necessary.

##### Videos

[The Black Fish](http://theblackfish.org/) is a super cool organisation based in the UK and the Netherlands that aim to keep fishing practices legal and pressure the government to set higher standards. They work in the Baltic and Mediterrenean seas, where illegal fishing is rife. They film [Losing Nemo](https://vimeo.com/66514539?raw=true) is there informational video on the state of over and illegal fishing.

Another fantastic short film which aims to educate people on overfishing was made by ---

[video]()

__The End of The Line__ is a very moving and comprehensive documentary on the state of the oceans and the corruption within fisheries. 

##### Google

[The Global Fishing Watch](http://globalfishingwatch.org/) is google's attempt to pick out illegal fishing practices with a little help from enthusiastic volunteers.

