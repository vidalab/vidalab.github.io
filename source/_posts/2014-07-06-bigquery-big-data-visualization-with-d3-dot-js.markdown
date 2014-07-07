---
layout: post
title: "BigQuery Big Data Visualization with D3.js"
date: 2014-07-06 21:58:05 -0700
comments: true
author: Phuoc Do
categories: 
---

How to handle large dataset with D3.js?

It's a frequently asked question. You can read several discussions on the topic [here](http://stackoverflow.com/questions/19144369/how-to-handle-large-dataset-in-d3js), [here](http://stackoverflow.com/questions/18244995/d3-how-to-show-large-dataset), and [here](https://groups.google.com/forum/#!topic/d3-js/aRKFtUaE5h4). So far, the best solution is to process data to a smaller dataset. Then use D3.js to visualize.

With carefully crafted data processing, we can get decent story from data. But this solution doesn't provide a lot of flexibility to experiment with data on the fly. We need a more streamlined workflow. Less friction can spark interesting data innovation.

I recently delved deep into Google BigQuery. It's a great tool to handle big dataset.

<!-- more -->

We will use New York Taxi dataset hosted on Google BigQuery. It is 4+ GB and has more than 350 million rows in 2 tables. In this article, I want to show you how to query it on the fly. Then use D3.js to create a line chart of total trip amount over time. You can explore the dataset here:

https://bigquery.cloud.google.com/table/833682135931:nyctaxi.trip_fare?pli=1

BigQuery has full SQL support. So we can run aggregate query directly on dataset. We'll group by month/year and sum total_amount column. It takes less than 5 seconds.

```sql
SELECT
  CONCAT(CONCAT(STRING(MONTH(TIMESTAMP(pickup_datetime))), "/"), STRING(YEAR(TIMESTAMP(pickup_datetime)))) AS time,
  SUM(INTEGER(total_amount)) AS total_amount
FROM
  [833682135931:nyctaxi.trip_fare]
GROUP BY
  time;
```

I export my result data to CSV and show here:

```
time,total_amount
8/2013,57131656
9/2013,127640676
2/2013,60858916
5/2013,69475856
1/2013,64333338
10/2013,67093673
11/2013,63805595
3/2013,69752928
12/2013,63510475
7/2013,62018079
6/2013,65204371
4/2013,67594555
```

Since I don't own this dataset, I can't query it on the fly directly. So I'm going to save this view to my account. But if you are the owner, you can run the above query directly. I'll be using the following query for the saved view:

```sql
SELECT * FROM [nyc_taxi.total_amount_month] LIMIT 1000;
```

Now we can construct our D3.js Javascript code:

```javascript

function onClientLoadHandler() {
  // setup D3.js
  
  // run BigQuery
  function runQuery() {
    var request = gapi.client.bigquery.jobs.query({
      'projectId': "master-smithy-633",
      'timeoutMs': '30000',
      // use your own query here
      'query': 'SELECT * FROM [nyc_taxi.total_amount_month] LIMIT 1000;'
    });
    request.execute(function(response) {
        var bqData = []

        response.result.rows.forEach(function(d) {
          bqData.push({"date": d3.time.format("%m/%Y").parse(d.f[0].v),
            "amount": +d.f[1].v});
        });
      
        drawLineChart(bqData);
    });
  }

  // authenticate to BigQuery, it asks for your Google credential to perform oauth
  var config = {
    'client_id': '262329615658-hhd3mjl4rkcq85njprr33s6hbau97bma.apps.googleusercontent.com',
    'scope': 'https://www.googleapis.com/auth/bigquery'
  };
  gapi.auth.authorize(config, function() {
    runQuery();
  });
  
  function drawLineChart(bqData) {
    // D3.js line chart drawing code
  }
}

// run client library load

$.getScript("https://apis.google.com/js/client.js", function(d) {
  onClientLoadHandler();
});

```

That's it. You can check out full code example here. You'll need to clone it and use your client_id key. Make sure your key allows vida.io origin.

https://vida.io/documents/icwvp4qcCbEkYW2ve

![BigQuery Line Chart](http://i.imgur.com/4uem4Qm.png?1)