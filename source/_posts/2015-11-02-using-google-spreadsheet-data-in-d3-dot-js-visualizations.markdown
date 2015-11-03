---
layout: post
title: "Using Google Spreadsheet data in d3.js visualizations"
date: 2015-11-02 16:46:08 -0800
comments: true
author: Phuoc Do
categories: 
---

Google Spreadsheet offers a convenient way to work with data on the web. It is now possible to retrieve live Google Spreadsheet data for d3.js visualizations. In this article, we'll show you how.

We make use of tabletop.js to abstract data retrieval task.
https://github.com/jsoma/tabletop

1. Move d3.js visualization code into a function, e.g. drawChart.
2. Use tabletop.js to get data and render the visualization:

```javascript
    var public_spreadsheet_url = 'https://docs.google.com/spreadsheets/d/1n-PIdnAJnxmHqVp_iE2g1k8UpPf-lEXLm_pu7zxuov4/pubhtml';

    function renderSpreadsheetData() {
        Tabletop.init( { key: public_spreadsheet_url,
                         callback: draw,
                         simpleSheet: true } )
    }

    function draw(data, tabletop) {
      // draw chart
      drawChart(data);
    }

    renderSpreadsheetData();
```

And a live example:

https://vida.io/documents/9eEyB4R74WWyrPXAi
