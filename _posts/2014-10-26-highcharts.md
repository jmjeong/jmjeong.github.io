---
layout: post
title: highcharts
modified: 
category: 
tags:
image:
  teaser: t-highcharts.jpg
---

open-flash-chart.swf 대신 사용한 js library. 간단하게 미려한 결과를 보여준다.

#### 결과

![](http://cl.ly/image/1Y2z2B11352N/Screenshot%20of%20Safari%20(2014.%208.%2014.%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011%3A31%3A01).jpg)

#### a.json

```json

{ "series": [
  { "name": "old",
    "data": [1,3,2,5] },
  {	"name": "new",
    "data": [5.1,3.7,3.4,4.4]}],
 "title": { "text": "Sales" },	
 "xAxis": {"categories": ["Apple", "Banaas", "Oranges", "Simul"]}
}
```

#### html

```html
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
<script src="http://code.highcharts.com/highcharts.js"></Script>
<div id="container" style="height: 500px"></div>

<script>
$(document).ready(function() {
    var options = {
        chart: {
            renderTo: 'container',
            type: 'spline'
        },
        series: [{}],
        yAxis: {
            title: {
                text: 'num',
            }
        },
    };
    
    var url =  "http://localhost:4000/a.json";
    $.getJSON(url,  function(data) {
        options.series = data.series;
        options.xAxis = data.xAxis;
        options.title = data.title;
        var chart = new Highcharts.Chart(options);
    });
});
</script>
```
