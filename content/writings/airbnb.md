---
title: Airbnb in New York
date: 2015-09-20
---


![airbnb_trans.png](/img/writings/airbnb_trans.png)
 
I find Airbnb itself to be an interesting concept. Renting out any left over space you might have in your home seems like a great way of earning some extra cash while at the same time meeting new people.
 
![cover.PNG](/img/writings/cover.jpg)
 
## Initial datasets
 
Airbnb provides datasets containing all the airbnb listings a number of large cities through [insideairbnb](http://insideairbnb.com/). I thought it would be cool to have a look at some of this data. It triggered my data exploration urge and multiple questions popped into my mind straight away. Let's have a look how Airbnb is like in New York.
 
The dataset contains information like Price, Number of Reviews and Number of days available in a year. It also allows for geospatial analysis as we have Borough, Neighborhood and even Latitude and Longitude information. 
 
I decided to go hunting for some additional data to find possible correlations. I soon bumped into the website [nycopendata](https://nycopendata.socrata.com) which has a bunch of free datasets related to New York. One that caught my eye was [Subway Entrances](https://nycopendata.socrata.com/Transportation/Subway-Entrances/drex-xx56) data. Might there be a correlation between price/ratings and the proximity to a subway entrance?
 
![newyork_subway_entrances.PNG](/img/writings/newyork_subway_entrances.jpg)
 
I also added the location of the main tourist attractions in New York. It would be interesting to see how the proximity to these affect the price.
 
![tourist_attraction_locations2.PNG](/img/writings/tourist_attraction_locations2.jpg)

I also found datasets containing all the free WifI hotspots and even all public parking lots/garages. I didn't use these dataset in my analysis but you can find them in the Git repo if you're interested. 
 
## Data preparation
 
First I needed to calculate the closest subway entrance. Using R, I came up with the following code. I fully expect this to be unoptimized. It did take a while to go through the 27000+ listings. If you have any suggestion, [please let me know!](http://svenhofstede.github.io/contact/)
 
<script src="https://gist.github.com/svenhofstede/06b18c62b34d1d85eab8.js"></script>

A similar calculations was needed for the closest tourist attractions. Here I also added the name of the attractions itself to the resulting dataset.

## Prices

*Disclaimer: I have never been to New York so I started with zero prior knowledge of the geo-spatial layout of New York.*

![price_count_per_borough.PNG](/img/writings/price_count_per_borough.PNG)

As expected Manhattan has the highest average price and also the most amount of listings. The majority of the famous attractions in New York (atleast as an unknowing tourist like myself) are located on Manhattan which should bump up the demand and therefore the price. 

Staten Island is the second most expensive borough to stay in. It does however have the least amount of listings. 

<script type='text/javascript' src='https://public.tableau.com/javascripts/api/viz_v1.js'></script><div class='tableauPlaceholder' style='width: 750px; height: 742px;'><noscript><a href='#'><img alt='general_impression ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;ai&#47;airbnb_analysis&#47;general_impression&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz' width='750' height='742' style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='site_root' value='' /><param name='name' value='airbnb_analysis&#47;general_impression' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;ai&#47;airbnb_analysis&#47;general_impression&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='showVizHome' value='no' /><param name='showTabs' value='y' /><param name='bootstrapWhenNotified' value='true' /></object></div>

The most expensive neighborhood is Tribeca in Manhattan with a hefty average price tag of just over $400 for one night. Not surprising as this is supposed to be one of the most desired neighborhoods in NYC. The list of celebrities who has proporty here is extensive.

## Subway Proximity

<script type='text/javascript' src='https://public.tableau.com/javascripts/api/viz_v1.js'></script><div class='tableauPlaceholder' style='width: 750px; height: 742px;'><noscript><a href='#'><img alt='distance_subway_price ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;pr&#47;proximity_subway&#47;distance_subway_price&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz' width='750' height='742' style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='site_root' value='' /><param name='name' value='proximity_subway&#47;distance_subway_price' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;pr&#47;proximity_subway&#47;distance_subway_price&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='showVizHome' value='no' /><param name='showTabs' value='y' /><param name='bootstrapWhenNotified' value='true' /></object></div>

The majority of the listings are very close to a subway entrance ( < 400m ) indicated by the blue line. The price of the listings are lower the further away from a subway entrance they are. This can be explained quite easily though. The attractive (more pricey) areas are generally packed with subway entrances. In Manhattan for example you will never be far from the subway whereas outside of Manhattan distances of 400m+ are more common.

<script type='text/javascript' src='https://public.tableau.com/javascripts/api/viz_v1.js'></script><div class='tableauPlaceholder' style='width: 750px; height: 742px;'><noscript><a href='#'><img alt='subway_entrances ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;56&#47;56XW8H7CB&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz' width='750' height='742' style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='path' value='shared&#47;56XW8H7CB' /> <param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;56&#47;56XW8H7CB&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='showVizHome' value='no' /><param name='showTabs' value='y' /><param name='bootstrapWhenNotified' value='true' /></object></div>

## Free WiFi

<script type='text/javascript' src='https://public.tableau.com/javascripts/api/viz_v1.js'></script><div class='tableauPlaceholder' style='width: 750px; height: 742px;'><noscript><a href='#'><img alt='WIFI Location ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;wi&#47;wifi_location&#47;WIFILocation&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz' width='750' height='742' style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='path' value='views&#47;wifi_location&#47;WIFILocation' /> <param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;wi&#47;wifi_location&#47;WIFILocation&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='showVizHome' value='no' /><param name='showTabs' value='y' /><param name='bootstrapWhenNotified' value='true' /></object></div>

Not related to Airbnb but still interesting. NYC seems to provide free WiFi in most parks.
