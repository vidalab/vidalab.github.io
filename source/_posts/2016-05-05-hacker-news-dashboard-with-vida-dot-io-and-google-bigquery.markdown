---
layout: post
title: "Hacker News Dashboard with vida.io and Google BigQuery"
date: 2016-05-05 17:22:36 -0700
comments: true
author: Phuoc Do
categories:
---

Google BigQuery provides data storage for large datasets. You can store Gigabytes of data and query them in seconds. In this article, we discuss how to connect to Google BigQuery and create a dashboard. We'll use the Hacker News dataset provided in BigQuery public data repository.

The final dashboard has four charts. Here's a screenshot of what it will look like:

<img src="http://i.imgur.com/SgRReJU.png" width="100%" title="Final Dashboard" />

First, we'll create four datasets. We will send query to Google BigQuery through a REST API proxy:

```javascript
  var query = "SELECT a.month month, stories, comments, comment_authors, story_authors \
  FROM ( \
    SELECT STRFTIME_UTC_USEC(time_ts, '%Y-%m') month, COUNT(*) stories, EXACT_COUNT_DISTINCT(author) story_authors \
    FROM [fh-bigquery:hackernews.stories]  \
    GROUP BY 1 \
  ) a \
  JOIN ( \
    SELECT STRFTIME_UTC_USEC(time_ts, '%Y-%m') month, COUNT(*) comments, EXACT_COUNT_DISTINCT(author) comment_authors \
    FROM [fh-bigquery:hackernews.comments]  \
    GROUP BY 1 \
  ) b \
  ON a.month=b.month \
  ORDER BY 1";

  $.post("https://pyapi-vida.herokuapp.com/bigquery", query, function(result) {
    var bqData = [];
    for (var i = 0; i < result.rows.length; i++) {
      var bqd = {};
      for (var key in result.rows[i]) {
        bqd[result.fields[key].name] = result.rows[i][key];
      }
      bqData.push(bqd);
    }

    callback(bqData);
  });
```

Here are the links to the 4 datasets that we use:

* [Hacker News - Type Count over Time](https://vida.io/datasets/MqCFLnsmpyxxg9Dsx)
* [Hacker News - Type Count Summary](https://vida.io/datasets/Rp43GosAhzS5Zhfbo)
* [Hacker News - Number of Comments during Day](https://vida.io/datasets/YPpNt8NqRw9ZbD6Lv)
* [Hacker News - Probability of Having Top Comments](https://vida.io/datasets/RqegcX8kAHJLiB4DA)

After creating 4 datasets, we go to Dashboards tab and create new dashboard. We'll add 1 line chart and 4 bar charts.

* Line Chart - Type Count over Time
  1. Select dataset "Hacker News - Type Count over Time".
  2. Set X Axis to Month.
  3. Set X Axis Label to Month.
  4. Set Y Axis Label to Count.
  5. Set Y Axis to: stories[new line]comments[new line]comment authors[new line]story_authors.
  6. Set Title to: Type Count over Time.

* Bar Chart - Type Count Summary
  1. Select dataset "Hacker News - Type Count Summary".
  2. Set X Axis to Type.
  3. Set X Axis Label to Type.
  4. Set Y Axis Label to Count.
  5. Set Y Axis to count.
  6. Set Title to: Type Count Summary.

* Bar Chart - Number of Comments during Day
  1. Select dataset "Hacker News - Number of Comments during Day".
  2. Set X Axis to Hour.
  3. Set X Axis Label to Hour.
  4. Set Y Axis Label to Count.
  5. Set Y Axis to count.
  6. Set Title to: Number of Comments during Day.

* Bar Chart - Probability of Having Top Comments
  1. Select dataset "Hacker News - Probability of Having Top Comments"
  2. Set X Axis to Hour.
  3. Set X Axis Label to Hour.
  4. Set Y Axis Label to Probability.
  5. Set Y Axis to prob.
  6. Set Title to: Probability of Having Top Comments.

Here's a video demo of the entire process:

<iframe width="630" height="472" src="//www.youtube.com/embed/u4xoofChZrk" frameborder="0" allowfullscreen></iframe>
