---
layout: post
title: "Extract web data with import.io and create d3 visualization"
date: 2014-06-08 22:45:06 -0700
comments: true
author: Phuoc Do
categories: 
---

With vida.io, you can quickly create new data visualizations. But how would you collect the data? There are now powerful and easy to use tools for this task. In this article, I will show you how to use import.io to extract web data and create d3 map visualization.

<!-- more -->

1. Download [import.io](https://import.io/) app.
2. Register your account and and login.
3. Create a new dataset. This will open a new tab.
4. Click Add Data menu and select "Create new Source" from drop down.
5. Enter wikipedia data source into import.io URL browser: http://en.wikipedia.org/wiki/Obesity_in_the_United_States
6. Extract data and upload to import.io. Final data will look like this:<img src="https://s3-us-west-2.amazonaws.com/vida-public/blog/import-io-dataset.png" width="600">

Once we are done with you can download data from import.io to CSV format. It is now ready for visualization on [vida.io](https://vida.io). Register an account if you don't have one.

1. Open [d3-map](https://vida.io/d3-map) page.
2. Select "US Map States - Choropleth" template and clone to your account.
3. Rename visualization (e.g. Obesity in the United States) and add description.
4. Go to data tab and import downloaded CSV file above. Click Save to save data.
5. Go to properties tab, select state_and_district_of_columbia for Map State field and overweight_incl_obese_adults_number for Map Value field.
6. Click Save to refresh visualization. Here's the [final visualization](https://vida.io/documents/bJDg3iQwyXcfngjgf):

<iframe src="http://embed.vida.io/documents/bJDg3iQwyXcfngjgf" width="800" height="450" seamless frameBorder="0" scrolling="no"></iframe>

That's it! Check out more templates on [Explore](https://vida.io/explore) section.

Here's a video tutorial that walks you through all the steps above:

<iframe width="600" height="450" src="//www.youtube.com/embed/b4vxnmdZN98" frameborder="0" allowfullscreen></iframe>