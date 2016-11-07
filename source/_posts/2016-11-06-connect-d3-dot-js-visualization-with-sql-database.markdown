---
layout: post
title: "Connect D3.js Visualization with SQL database"
date: 2016-11-06 23:14:25 -0800
comments: true
categories: 
---

Supported SQL databases: PostgreSQL, MySQL, MS SQL Server.

D3.js visualizations often use CSV data files that are loaded into browser. In this article,
we walk you through how to connect to SQL database on vida.io and use D3.js to visualize the data.

The database contains data for view activities of website. We use calendar heatmap to visualize
the frequency during months. The raw data table has 3 columns: views, created_at, and updated_at.

<img src="http://i.imgur.com/LYyl3lk.png" title="Raw Data" />

<!-- more -->

The first step we need to do is to connect to the PostgreSQL database. After login, we go to
Sources section and create a new data source. We call it ACME PostgreSQL. For our example,
we use the following connection settings:

1. Hostname: localhost
2. Port: 5432
3. Username: postgres
4. Password:
5. Database name: acme_webapp

Next, we create a dataset that reads from ACME PostgreSQL data source.

1. Go to Datasets section and create a new dataset.
2. We call it ACME Activities.
3. Scroll to the bottom of the page and click "Add SQL Query."

Raw data points only record the event. We need to group and count the data happening during days.
We use the following SQL query:

```
SELECT TO_CHAR(created_at, 'MM/DD/YYYY') AS created, count(*) FROM activities GROUP BY created ORDER BY created;
```

The result dataset contains the following data:

<img src="http://i.imgur.com/3YUkuC2.png" title="Grouped Data" />

Now, we create calendar heatmap visualization.

1. Go to Documents section and click on "New Document" button.
2. Select "Import Vida" under custom section. We use Calendar Heatmap template from vida.io.
3. Paste in the following document ID "Fmhxf9jxed5GY993X" and click Import.
The app will take us to the imported document.
4. Click on Data tab and select "Link External" from Datasets menu. Note: this feature is
available to subscribed user only. Please contact us if you have any question.
5. Select "ACME Activities" dataset that we created earlier.
6. Click on Save to refresh the document.

The final visualization looks like below.

<img src="http://i.imgur.com/azVf8th.png" title="Grouped Data" />

Here's a video demo of the entire process:

<iframe width="630" height="472" src="//www.youtube.com/embed/cyWDmGqfzHQ" frameborder="0" allowfullscreen></iframe>
