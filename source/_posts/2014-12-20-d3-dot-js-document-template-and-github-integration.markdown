---
layout: post
title: "D3.js Document Template and GitHub Integration"
date: 2014-12-20 18:25:29 -0800
comments: true
categories: 
---

In this blog post, we want to show you integration between vida.io cloud editor and GitHub. git is a great source control tool to keep track of complex visualization project.

You can use import your git repository for instant view and sharing in the cloud.

<!-- more -->

vida.io use a new repository format. We made a few enhancement on top of GitHub gist:

1. Full git repo (issue tracking, pull request)
2. Separation of data and code
3. Support for visualization properties

This is done through manifest.json file. Here's a manifest.json for Line chart template:

```json
{
  "data": ["document.json"],
  "javascript": ["document.js"],
  "stylesheet": ["document.css"],
  "html": ["document.html"],
  "properties": [
    {"label":"Data Column 0 (X Axis)","name":"data0","type":"data_column","value":null},
    {"label":"Data Column 1 (Y Axis)","name":"data1","type":"data_column","value":null},
    {"label":"Label 0","name":"label0","type":"string","value":"label 0"},
    {"label":"Label 1","name":"label1","type":"string","value":"label 1"},
    {"label":"Color 0","name":"color0","type":"color","value":"#0f608b"},
    {"label":"Color 1","name":"color1","type":"color","value":"#99ccff"},
    {"label":"Width","name":"width","type":"number","value":800},
    {"label":"Height","name":"height","type":"number","value":400}
  ]
}
```

We host the document template repository on GitHub. You can clone it to get started.

https://github.com/vidalab/document_template

We have created a [Directional Force Layout example (from d3noob)](http://bl.ocks.org/d3noob/5141278) repository:

https://github.com/dnprock/document_template

You can import your GitHub repository into vida.io:

1. Login to vida.io
2. Select D3 Documents
3. Click New Document
4. Select Import GitHub type
5. Paste your GitHub repository URL (e.g. https://github.com/dnprock/document_template)
6. Click Import

Viola! Now you have a force layout live in the cloud. You can share with your team and customers.