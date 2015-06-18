---
layout: post
title: "Experiment with d3.js in the Cloud"
date: 2014-05-28 00:12:31 -0700
comments: true
author: Phuoc Do
categories: 
---

bl.ocks.org is a popular tool within D3 community for sharing data visualization. While it is great to be able to share visualization, bl.ocks.org is not easy to experiment with your visualization.

We are building a new offering at vida.io to enable cloud experimentation. You can quickly import and play with the visualization. There are two ways to import d3.js block into vida.io. The first way is directly from gist. The second way is to create a reusable template document.

<b>Import gist or block</b>

Video demo:

<iframe width="630" height="472" src="https://www.youtube.com/embed/ZOSiMGcBtug" frameborder="0" allowfullscreen></iframe>

1. Copy Gist (Block) URL
2. Login to vida.io and select Gists (Blocks) menu
3. Click on Import button and paste in the URL
4. Click Create button

<b>Create a resuable template document from gist or block</b>

Video demo:

<iframe width="630" height="472" src="//www.youtube.com/embed/e1BOJnW9N3Q" frameborder="0" allowfullscreen></iframe>

In this post, we'll use this bl.ocks.org example for d3noob:

[Basic Directional Force Layout Diagram](http://bl.ocks.org/d3noob/5141278)

<!-- more -->

Here are the steps to import bl.ocks.org to [vida.io](https://vida.io):

1. Create a new document in vida.io
2. Copy stylesheet code to Stylesheet tab
```css
path.link {
  fill: none;
  stroke: #666;
  stroke-width: 1.5px;
}

circle {
  fill: #ccc;
  stroke: #fff;
  stroke-width: 1.5px;
}

text {
  fill: #000;
  font: 10px sans-serif;
  pointer-events: none;
}
```
3. Copy javascript code to Javascript tab. No need to copy d3.csv call, data field is already declared by vida.io
```javascript
var nodes = {};

// Compute the distinct nodes from the links.
links.forEach(function(link) {
    link.source = nodes[link.source] || 
        (nodes[link.source] = {name: link.source});
    link.target = nodes[link.target] || 
        (nodes[link.target] = {name: link.target});
    link.value = +link.value;
});

// ...

    node
        .attr("transform", function(d) { 
  	    return "translate(" + d.x + "," + d.y + ")"; });
}

```
4. Rename links variable name to data
```javascript

// links.forEach(function(link) {

data.forEach(function(link) {

// .links(links) 

.links(data)

```
5. Copy force.csv data to Data tab
6. Save to refresh the visualization. You can start tweaking parameters of the visualization.

Here is the final result document:

[Directional Force Layout](https://vida.io/documents/XWsLjooRt6KXadzT9)