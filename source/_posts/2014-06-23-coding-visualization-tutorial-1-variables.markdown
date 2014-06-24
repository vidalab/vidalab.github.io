---
layout: post
title: "Coding Visualization Tutorial 1: Variables"
date: 2014-06-23 14:44:42 -0700
comments: true
author: Phuoc Do
categories: 
---

In this tutorial, we want to explore Javascript variables. They are important code components. We will review the major variable types that you'll see in a D3 visualization. Then we will dive into visualization examples and play with variables.

You can declare Javascript variables as below:

(// is comment)

```javascript

// declare WIDTH variable, the type is integer
var WIDTH = 800;

// declare HEIGHT variable, the type is integer
var HEIGHT = 500;

// declare margin as hash with keys are 4 corners of visualization,
// hash is a key value pair, use key to access value,
// for example, margin.top returns an integer of value 20
var margin = {top: 20, right: 20, bottom: 30, left: 50}

// string variable
var Y_AXIS_LABEL = "Price ($)";

// array variable
var data = [];
// add 2 data points to data array
data.push({x_axis: "1-May-12"}, {y_axis: 582.13});
data.push({x_axis: "30-May-12"}, {y_axis: 583.98});

// boolean variable, 2 values: true or false
var check = true;

// variable can be an object which means it can be anything
var xAxis = d3.svg.axis()
    .scale(x)
    .orient("bottom");
// think of xAxis as a d3 axis type, it can do some axis magic
```

<!-- more -->

Things you can do with variables:

```javascript
// for number, arithmetic
// calculate real width, height of visualization
// by subtracting margins, number can be subtracted
var width = WIDTH - margin.left - margin.right;
var height = HEIGHT - margin.top - margin.bottom;

// you can concatenate string with +
Y_AXIS_LABEL = Y_AXIS_LABEL +  " " + "Dollars";
// now Y_AXIS_LABEL is "Price ($) Dollars"

// access data array

// data[0] returns 1st data point
// check if value of 2nd data point is greater than 1st data point
var check = data[0].y_axis > data[1].y_axis;
```

Here's an example D3 document you can use:

https://vida.io/documents/eSGFToFs3gXk4LEwP

See tutorial video here:

<iframe width="420" height="315" src="//www.youtube.com/embed/5Jg7RLZC6s8" frameborder="0" allowfullscreen></iframe>