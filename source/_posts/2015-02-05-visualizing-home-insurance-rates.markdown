---
layout: post
title: "Visualizing Home Insurance Rates"
date: 2015-02-05 17:34:11 -0800
comments: true
author: Phuoc Do
categories: 
---

This tutorial is a guest post from [GRIDLEX](http://www.gridlex.com/) and [vHomeInsurance.com](http://vHomeInsurance.com). Visit their websites for more information.

[GRIDLEX](http://www.gridlex.com/) is a data analytics firm based in New York.

[vHomeInsurance.com](http://vHomeInsurance.com), a home insurance analytics service, visualized US wide home property prices using Vida.io. The below guide walks through a case study on representing geographical data on a map & how they did it.

<!-- more -->

From the [vHomeInsurance.com](http://vHomeInsurance.com) Team:

[Vida.io](https://vida.io) is a great place on the web to get the visualizations done. Using their templates, some complex map visualizations using D3.js can be done very easily, without much programing knowledge. The beauty of the tool is that only data needs to be plugged in and some styling elements edited, while it handles all the complexities itself. 

Here is an example of we used vida.io to generate an awesome Chloropeth heat map representing home prices across the US at a county level.

<b>Interactive Heatmap (Hover to See Value)</b>

<iframe src="http://embed.vida.io/documents/CvFWfA899K4gtNBtN" width="650" height="420" seamless frameBorder="0" scrolling="no"></iframe>

The above chart from Vida.io is a visualization of home values in all the counties in US quantized to 21 levels, with lighter values representing the counties where homes are cheaper and the darkest are the counties where the homes are the costliest.

<b>Search for Your Visualization</b>

To generate visualizations like the above heat map:

1. Register and log in
2. Navigate to Explore section of the page
3. Click "More" button of "maps" category
4. Select “US Map Counties - Choropleth”
5. Clone the document template (clone button is available on the left side just below the map)

<img src="http://i.imgur.com/1IE8Ewh.png" width="100%"/>

<b>Get Familiar with the Editing Screen</b>

Once the template is cloned, the document is shown in the home screen, click on the document to start editing it. The right half of the editor window has code , data,stylesheets and other configurable variables while the left half has the map itself so that the effect of the changes made can be seen immediately to start editing the document.

<img src="http://imgur.com/vffdaVt.png" width="100%"/>

<b>Import your data</b>

We can import data in any one csv, tsv or json format by clicking the import button in the data tab or it can directly be pasted in the editor. If you want to keep things simple keep the headers as is. For example, in the data we imported, we had the county ID  & the home value rates. We can retain those same headers or change it to whatever we want. For example, if we want to change rates to Home Values we need to edit a few extra lines of code.

For the county & geographical information, it has to be noted that the id column in the default data is the combination of state FIPS code and county FIPS code, its important that the data to be visualized contains this number as the its used as the identity of the county when map is generated

More information about the number can be obtained from 
[https://www.census.gov/geo/reference/codes/cou.html](https://www.census.gov/geo/reference/codes/cou.html)

<b>Edit Javascript</b>

This is where all the magic happens. All the code needed to generate the visualization is already present, we only need to edit one or two lines depending upon what we want to achieve

Notice the following code:

```javascript
var quantize = d3.scale.quantize()
                  .domain([0, .15])
                  .range(d3.range(9).map(function(i) { return "q" + i + "-9"; }));
```

Its of the form:

```javascript
var quantize = d3.scale.quantize()
                  .domain([<LOWEST>, <HIGHEST>])
                  .range(d3.range(<Q>).map(function(i) { return "q" + i + "-9"; }));
```

where:

<LOWEST> is the lowest value your data can have
<HIGHEST> is the highest value your data can have
<Q> is the number of quantization levels you want for your data, here it is number of colors you want to use in the cloropeth

Change those values according to your data and needs.

If you have changed the headers for data in the data tab see the following code:

```javascript

data.forEach(function(d) {
  rateById.set(d.id, +d.rate); 
});
```

Its equivalent to:

```javascript
data.forEach(function(d) {
  rateById.set(d.id, +d.<Column Name>); 
});
```

If you are comfortable with representing your data in less than 9 colors, just save the document using the save button on the top right and you can see your visualization on the left side of the screen immediately.

<b>Change the Colors</b>

You can change the colors in the map or other styling in stylesheet tab:

If you have used the default 9 quantization levels its enough to edit the numbers in:

```css
.q0-9 { fill:rgb(247,251,255); }
```

To change the color of a quantization level 0. you can choose the colors using any online css color picker tool.

If you were not satisfied with 9 quantization levels and increased the number, you need to add the colors you want to use for that quantization level.

For example if you used 11 quantization levels, you need to add the lines:

```css
.q9-9 { fill:rgb(255,0,255); }
.q10-9 { fill:rgb(255,0,0); }
```

To use the colors magenta and red to represent the newly added quantization level 9 and 10 respectively.

Save the document to see the visualization.

<b>Share your work</b>

You can find the code to embed the map in web pages and the link to share your work by clicking the Embed button under Settings tab.

View and clone home insurance visualization here:

[https://vida.io/documents/CvFWfA899K4gtNBtN](https://vida.io/documents/CvFWfA899K4gtNBtN)