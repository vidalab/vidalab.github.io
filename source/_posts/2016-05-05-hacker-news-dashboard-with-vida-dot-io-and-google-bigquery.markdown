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

First, we'll create a data source for Google BigQuery.

1. After login, click on Source tab and New Source button.
2. Name your source: Hacker News (BigQuery).
3. Select database type BigQuery.
4. Upload your credentials file. Click [here](https://cloud.google.com/storage/docs/authentication#generating-a-private-key) for instruction to generate the file.

Next, we'll create four datasets.

1. Click on Datasets tab and New Dataset button.
2. Click on Add SQL Query button.
3. Select the database source we just created: Hacker News (BigQuery).
4. Paste in the queries below for each dataset.

Type Count over Time

```
SELECT a.month month, stories, comments, comment_authors, story_authors
FROM (
  SELECT STRFTIME_UTC_USEC(time_ts, '%Y-%m') month, COUNT(*) stories, EXACT_COUNT_DISTINCT(author) story_authors
  FROM [fh-bigquery:hackernews.stories] 
  GROUP BY 1
) a
JOIN (
  SELECT STRFTIME_UTC_USEC(time_ts, '%Y-%m') month, COUNT(*) comments, EXACT_COUNT_DISTINCT(author) comment_authors
  FROM [fh-bigquery:hackernews.comments] 
  GROUP BY 1
) b
ON a.month=b.month
ORDER BY 1
```

Type Count Summary

```
SELECT type, COUNT(*) count
FROM [fh-bigquery:hackernews.full_201510]
GROUP BY 1
ORDER BY 2
LIMIT 100
```

Number of Comments during Day

```
SELECT HOUR(SEC_TO_TIMESTAMP(time-3600*7)) hour, COUNT(*) comments, AVG(ranking) avg_ranking, SUM(ranking=0)/COUNT(*) prob
FROM [fh-bigquery:hackernews.comments] 
WHERE YEAR(time_ts)=2015
GROUP BY 1
ORDER BY 1
```

Probability of Having Top Comments

```
SELECT HOUR(SEC_TO_TIMESTAMP(time-3600*7)) hour, COUNT(*) comments, AVG(ranking) avg_ranking, SUM(ranking=0)/COUNT(*) prob
FROM [fh-bigquery:hackernews.comments] 
WHERE YEAR(time_ts)=2015
AND parent IN (SELECT id FROM [fh-bigquery:hackernews.stories] WHERE score>10)
GROUP BY 1
ORDER BY 1
```

Here are the links to the 4 datasets that we use:

* [Hacker News - Type Count over Time](https://vida.io/datasets/DvPDG5HfxpDNkEMQ3)
* [Hacker News - Type Count Summary](https://vida.io/datasets/TGc5ytt99pQnLP9Gg)
* [Hacker News - Number of Comments during Day](https://vida.io/datasets/hNN5Hmf762NYuyYQQ)
* [Hacker News - Probability of Having Top Comments](https://vida.io/datasets/Qzicd7DFjy5mKTbL2)

After creating 4 datasets, we go to Dashboards tab and create new dashboard. We'll add 1 line chart and 3 bar charts.

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

<iframe width="630" height="472" src="//www.youtube.com/embed/BGfTa_wKjK4" frameborder="0" allowfullscreen></iframe>
