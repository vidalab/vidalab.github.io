---
layout: post
title: "Embed d3.js visualization to blog"
date: 2014-05-31 23:54:14 -0700
comments: true
author: Phuoc Do
categories: 
---

I recently got a question from our user on how to embed d3.js visualization into their blog. A quick search returns several solutions like bl.ocks.org or Wordpress D3 plugin. The first solution requires programmer intervention each time content owner needs to update the site. Wordpress D3 plugin requires installation of plugin.

There comes [vida.io](https://vida.io) embed. Our site provides simple solution. Blog content owner can update post without programmer's intervention. In case of visualization update, he/she can use [vida.io](https://vida.io) editor to quickly make change.

<!-- more -->

Here's an example:

```html
<iframe src="http://embed.vida.io/documents/SodotqYWppo6NWK9m" width="100%" height="340" seamless frameBorder="0" scrolling="no"></iframe>
```

<iframe src="http://embed.vida.io/documents/SodotqYWppo6NWK9m" width="100%" height="340" seamless frameBorder="0" scrolling="no"></iframe>

The above visualization is responsive to window width. It fits to mobile devices. This is supported by viewbox resize technique:

```javascript
function resizeViewbox() {
    var targetWidth = $('#canvas').width();

    if (targetWidth > frameWidth) {
      targetWidth = frameWidth;
    }

    chart.attr("width", targetWidth);
    chart.attr("height", targetWidth / aspect);
}
```

It's a simple technique that works with [vida.io](https://vida.io) embed. [Contact us](mailto:contact@vida.io) if you have any question.