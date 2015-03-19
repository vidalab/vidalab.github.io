---
layout: post
title: "Coding Visualization Tutorial 2: Functions"
date: 2014-06-23 17:40:04 -0700
comments: true
author: Phuoc Do
categories: 
---

Function is a block of code to perform a particular task. You can use function to reduce repetitive code and improve readability. Function can be a separate object or part of another object.

```javascript

// general syntax
function name(variables) {
  // execute task
}

// for example, multiple two numbers
function multiply(n1, n2) {
  return n1 * n2;
}

// this call return 12 and assign to n
var n = multiply(3, 4);

// This function selects div tag with id="canvas-svg"
var canvas_svg = d3.select("#canvas-svg");

// Append svg element to canvas_svg div
var svg = canvas_svg.append("svg");

```

<!-- more -->

You can call functions in a chain. It's commonly used in D3 code.

```javascript

// This statement calls select and append on select result
// It's equivalent to two statements above.
var svg = d3.select("#canvas-svg")
            .append("svg");

```

Even more chaining:

```javascript
var svg = d3.select("#canvas-svg")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

// Above code do the following:

// Append svg element to #canvas-svg div, this statement returns svg element
d3.select("#canvas-svg").append("svg");

// Set width and height of svg element
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)

// Append g element to svg element
  .append("g")

// Set transform attribute of above g element
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
```

After that, you'll get canvas-svg div like below:

```html

<div id="canvas-svg">
  <svg width="800" height="450">
    <g transform="translate(50,20)">
      <!-- visualization elements -->
    </g>
  </svg>
</div>

```

See example document here:

https://vida.io/documents/9Pst6wmB83BgRZXgx

See tutorial video here:

<iframe width="630" height="472" src="//www.youtube.com/embed/PlH1MIrYY_M" frameborder="0" allowfullscreen></iframe>