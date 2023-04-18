---
title: "What I think of Tableau"
date: 2016-02-20
---

I've been working with Tableau professionally for the past two years. I create ready-to-use dashboard for end-users who typically consume them via the Tableau Server portal. I feel however that this is not the best use for Tableau and I'll go into details why further on. Let's start with some of the highlights.

## + As easy as Excel

Tableau is great. I would advise anyone to go check it out if you are looking for an easy-to-learn, professional package for data exploration/analysis. The core features of Tableau work extremely well and the user experience is great. You can safely hand the program to any experienced computer/excel user and expect them to get started with it.

## + Effective visualization out of the box

Choosing the right visualization is very important. Explaining the results of your data analysis is about conveying a message, telling a story. It's not supposed to be flashy. Tableau has awesome default graph settings which not only look sleek and clean but also emphasize the message without being distracting. A simple bar chart or line graph usually all you need and Tableau knows this. Very little time is lost formatting and customizing the appearance of the output.

## + Speed of workflow 

Have a new idea? Adding an new view is super convenient. Simply create a new worksheet and drag on the fields. Or even better, duplicate an existing worksheet and modify from there. You find yourself often creating new worksheet to try out different combinations. 

Making is mistake is no problem, the undo button works everytime. This lets you explore freely without worrying of losing your work. 

## + Tableau Server

This is not a crucial product if you a lone data analyst or a small group. The investment is big and only makes sense for certain Tableau environments. It allows for easy sharing and viewing of published Tableau workbooks. The permission system works great. 

## - Lack of developer-focussed features

The problem with Tableau is typical for any GUI based, end-user focussed product. To be easy to use you need to abstract away a lot of the fine-grained, nitty-gritty controls. This is great if you are a data analyst simply looking to find answers to your questions. You don't want to worry about that, acceptable default settings are fine. However it would be nice to have more control in case you need it.

## - Layout is a nightmare

This probably the biggest pitfall when using Tableau intensively for 'canned' dashboards. If you want your dashboard to look exactly like you would like it to you can expect some major annoyances. Moving elements around on dashboard can be super fidgety. It uses a snap-to-grid style which forces you to structure your dashboard in an unnatural way.

Responsive design has not yet been implemented properly. The automatic sizing option is actually discouraged when used together with Tableau Server as the server will create a cached version of the output for every requested screen dimension. 

Effectively copying over formatting from one view to another or applying workbook-wide layout/format settings is not possible. You will need to change the font/colors/thickness/number format, .. for each view seperately.

I know they are working on this and a large overhaul of the system is coming up in a future release so hopefully they make this slightly more bearable. 

## - Tableau doesn't do lists

Tableau simply doesn't support creating lists, only crosstabs. You can mimic a list using the crosstab but this still has it's limitations. Tableau always expects there to be values in the row section AND the column section. 

Tableau does have an data export feature which in essence is a list of your data but this feature is not customizable. Exporting your data means exporting everything including all the custom calculations you added. This might not sound as bad but I would expect there to be way to customize which columns of the data set you would like to export. 

## - Strange data source behaviour

Caching, joining data sets, switching data sources, working with data extracts, .. create a lot of headaches when dealing with data sources, especially in conjunction with Tableau server. This is probably more of an issue once you start connecting to actual databases and try to do complex joins.

## - Missing feature or strange limitations

Finally there are many features that you would expect a product such as Tableau to have by default. A short list below, much more can be found on <a href="https://community.tableau.com/community/ideas">the ideas website</a>

* Changing/resetting custom color configurations when switching datasource
* No dynamic parameters where value automatically update based on the dataset
* No multi-select prompt using a parameter 
* Automatically renaming columns when importing a data source
* Setting font/color/format settings on a workbook level
