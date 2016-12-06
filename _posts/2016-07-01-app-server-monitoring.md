---
layout: single
title: App/Server monitoring
category: node
excerpt: graphite, graphana, statsd
tags: node
---

- [PDF Format](http://dr.jmjeong.com/ubmm+)

---

> It's not in production unless it’s monitored”. 
-- Theo Schlossnagle

---


> If you can not measure it, you can not improve it.” 
-- Lord Kelvin

---


> What is measured improves
-- Peter Drucker

---

## Question to answer

- How fast is my system?
- Is it faster than last month?
- Did our last deploy affect database performance?
- How much time do we spend calling external web services?

---

## More questions

- How many errors do we have a day?
- How many failed logins?
- How many successful logins?

---

## To answer all of this, you need a way
## [fit] to **track** difference **numbers**

---


![100%](https://googledrive.com/host/0B5YqfYBpS__8b1pIVnNVbFNGc0U/Graphite)

---


## Graphite 

- A Highly Scalable Real-time Graphing System
- [http://graphite.wikidot.com/](http://graphite.wikidot.com/)


- Components 
   - carbon - a daemon that listens for time-series data.
   - whisper - a simple database library for storing time-series data.
   - webapp - a (Django) webapp that renders graphs on demand.

--- 


![inline,100%](http://graphite.wikidot.com/local--files/screen-shots/graphite_cli_800.png)

---

## Data Retention

- Default settings
  - 6 hours of 10 second data
  - 1 week of 1 minute data
  - 5 years of 10 minute data  
- That's amounts to ~3.2MB per metric
- Configurable
  
```yaml
[server_load]
priority=100
pattern- ^servers\.
retentions = 60:43200,900:350400
```

--- 

## Ports

- 80 : nginx
- 2003 : carbon
- 2004 : carbon aggregator
- 2023 : carbon pickle
- 2024 : carbon aggregator pickle

---

## The Graphite Message Format

```
metric_patch value timestamp(UNIX epoch time)\n
```

```
ex) foo.bar.baz 42 74857843
```

---

## Populate Data

```bash
PORT=2003
SERVER=graphite.your.org
echo "local.random.diceroll 4 `date +%s`" | nc -c ${SERVER} ${PORT}
```

---

## node.js

```js
var graphite=require('graphite')

var client = graphite.createClient('plaintext://server:2003/');
var metrics = { foo.bar.baz : 72, 
                foo.bar.test : 100 
                foo.bar.size : 1024 };
client.write(metrics, Date.now(), function(err) {
	if (err) console.error(err);
})                
```

another notation:

```js
var metrics = { foo.bar : {baz : 72, test : 100, size : 1024 }};
```
--- 


## Grafana

- Beautiful metric & analytic dashboards
- Use graphite as backend storage
- [http://grafana.org/](http://grafana.org/)
- [Live Demo](http://play.grafana.org/)

---

![inline](http://grafana.org/assets/img/features/dashboard_ex.png)

---

## Statsd

- A simple NodeJS daemon that listens for messages on a **UDP** port
- It parses the messages, extracts metrics data, and periodically flushes the data to graphite



![inline, 100%](https://cl.ly/4339102u2d1p/statsd.png)
Your app send data to StatsD

---

## Usage

```
<metricname>:<value>|<type>
```

```sh
echo "foo:1|c" | nc -u -w0 127.0.0.1 8125
```

---

### StatsD Metric Types

- Counting - number of orders per sec
  - `gorets:c|c`
  - At each flush the current count is sent and reset to 0

- Sampling
  - `gorets:1|c|@0.1`
  - Sent sampled every 1/10th of the time
	
---

### StatsD Metric Types (cont'd)

- Gauges - total orders today
  - `gaugor:333|g`
  - If the gauge is not updated at the next flush, it will send the previous value

- Sets - unique user count
  - `uniques:765|s`
  - Counting unique occurrences of events between flushed, using a Set to store all occurring events

---

### StatsD Metric Types (cont'd)

- Timing - time to make an order
  - `glork|320|ms|@0.1`

---

### node statsd-client

```js
var SDC = require('statsd-client');
var sdc = new SDC({host:host,port:port,prefix:prefix});

sdc.increment('sample.counter');
sdc.increment('sample.mycounter',10);
sdc.gauge('sample,gauge', randomInteger(100));

var timer=new Date();
sdc.timing('sample.timer',timer);

sdc && sdc.close();
```

---

## For log & crash search


---

## Slack Integration


![inline ](http://cl.ly/0u2L422E2T0P/slack-tclcs.png)


---


```js
var alarmUrl = conf.alarm.info.url;
var payload = {
		"channel": "monitoring",
		"username": title.name,
		"text": ['[', moment().format('YYYY-MM-DD HH:mm:ss'), '] ', icon, ' ', data].join(''),
		"icon_emoji": title.icon
};
request({
		url: alarmUrl,
		method: 'POST',
		json: payload
}, function(err, resp, body) {
		if(err) {
				logger.error('[sendNoti] error;', err);
		} else {
				logger.debug('[sendNoti] result; '+body.toString());
		}
});
```

---


## graphite naming convention

- {env}.{metric}.{region}.{hostname}

- lnc.summary.* - for All Projects
  - count, size, totalsize
  - denySize, denyCount, ...
- lnc.{group}.{appkey}.* - for each Projects
- lnc.internal.*
  - lnc.internal.sct.stats.*
  - lnc.internal.kafka.lag.*

---

![inline,100%](http://cl.ly/0U1m1d1o3s12/grafana-lnc.png)

---

![inline,100%](http://cl.ly/003X0w0K0j2Q/grafana-setting.png)

---

## node.js

```js
function sendToGraphite(prefix, data) {
    var url = 'plaintext://'+conf.graphite.server+':'+conf.graphite.port+'/';
    var client = graphite.createClient(url);

    var metric = {};
    metric[prefix]=data;
    client.write(metric, function(err) {
        if (err) {
           logger.error('[sendToGraphite] send error', err);
        }
        else {
            logger.debug('[sendToGraphite] send to ', url);
		}
        client.end();
    });
}

sendToGraphite('lnc.internal.sct.stats', {
	totalOnEs: result.total_doc_count,
	sctQueue: result.doc_count,
	esProcessed: result.processed_count,
	esUpdateChecking: result.update_waiting
});
```