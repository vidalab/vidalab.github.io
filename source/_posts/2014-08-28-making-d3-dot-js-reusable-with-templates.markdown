---
layout: post
title: "Making D3.js Reusable with Templates"
date: 2014-08-28 13:48:49 -0700
comments: true
categories: 
---

D3.js is an awesome library for visualization. However, it requires a developer to perform the magic. So far, it has not been so popular with traditional data analysts.

At [vida.io](https://vida.io), we set out to bring D3.js to less technically savvy users. We want to enable them to create amazing data visualizations with D3.js. Our approach is template.

<!-- more -->

<b>What is a D3.js Template?</b>

It's a D3.js visualization that you can reuse by just plugging in new data. For example, one of our customers want to be able to compare metrics of two different entities. We made a template with multiple side-by-side bar charts. Below are comparisons of India vs. China and Apple vs. Orange.

<div style="width: 100%; float: left">
<div style="float: left; width: 45%"><a href="https://vida.io/documents/ZCzewTza4ZSzMWSBG">India vs. China<br><img src="http://i.imgur.com/gBZEQHe.png?1" width="100%" title="India vs. China" /></a></div>

<div style="float: right; width: 45%"><a href="https://vida.io/documents/7Ynhpabosba6uABXD">Apple vs. Orange<br><img src="http://i.imgur.com/K8k4I6A.png" width="100%" title="Apple vs. Orange" /></a></div>
</div>

<br>

Both visualizations share the same JavaScript and Stylesheet. User can clone India vs. China template, add new data, update colors to get Apple vs. Orange.


Data for India vs. China:

```json
[
  {
    "chart_title": "Population",
    "unit": "billion",
    "India": 1.22,
    "China": 1.36
  },
  // ...
]
```

Data for Apple vs. Orange:

```json
[
  {
    "chart_title": "Calories",
    "unit": "int",
    "Apple": 52,
    "Orange": 47
  },
  // ...
]
```

You can see data format for two visualizations are identical.

<b>Reuse a D3.js Template</b>

You can create new D3.js visualizations in 3 quick steps with [vida.io](https://vida.io) tool.

1. Clone a visualization template
2. Apply new data
3. Update styling and colors

<b>More Templates</b>

Here's a complex template used by the [Washington Business Alliance](https://www.wabusinessalliance.org/) to display metrics of US states.

<div style="width: 100%; float: left">
<div style="float: left; width: 33%"><a href="https://vida.io/documents/4vZ9mRGyepoyQxFcK">Obesity<br><img src="http://i.imgur.com/UgFqLF0.png" width="100%" title="Obesity" /></a></div>

<div style="float: left; width: 33%"><a href="https://vida.io/documents/69un8KK53pakRQtLZ">Wine Consumption<br><img src="http://i.imgur.com/u2GqAJO.png" width="100%" title="Wine Consumption" /></a></div>

<div style="float: right; width: 33%"><a href="https://vida.io/documents/5pQED7H5Lym36xsuC">Hockey Players per 100k residents<br><img src="http://i.imgur.com/0HOfp4a.png" width="100%" title="Hockey Players" /></a></div>
</div>

Check out the list of templates on [vida.io/explore](https://vida.io/explore). If you need more, contact us at contact@vida.io.

With template, D3.js is easy to use, reuseable, and affordable. Add it to your toolbox for business intelligence and data analysis!