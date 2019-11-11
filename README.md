# Vessel Metrics Python Package
This is Vessel Metrics Python package to collect Application/Micro-Service level Metrics and act as a scrape target for Prometheus to scrape for every pre-defined time interval.

This repository contains a very fast and light Metrics Collection client for Vessel Services.

Programming languages supported so far are:

-->Python

## Pre-Requisites
Python >= 3.x.

Pip (latest)

Prometheus-Client

```bash
pip install prometheus_client
```
## Vessel-Metrics Docker Image
You can install vessel-metrics after cloning this repository, i.e.
http://bitbucket-insightsnow.pfizer.com/scm/ga/vessel-metrics.git
or using vessel-metrics docker image

After Cloning/Installing or adding image to your micro-service, import classes and methods required to collect application metrics, e.g.
```python
from vslmetrics.metrics import setup_metrics
from vslmetrics.counter import CounterMetric
from vslmetrics.register import app_register
from vslmetrics.guage import GuageMetric
```
Add the following lines of code to your app.py
```python
app = Flask(__name__)
setup_metrics(app)
app_register(app)

app.config['CORS_HEADERS']='content-Type'
cors = CORS(app)

cm = CounterMetric(metric_description= "hello", metric_name="test", metric_key_value= {"key1":"ad"}, svc_version="0.11", op_code="asd", app_id="add")
CM = cm.create_metric()
```
Add the following code to each individual @app.route
```python
try:
	      CM.labels(svc_version="0.11", op_code="asd", app_id="add", key1 = "dad").inc()
	except Exception as e:
	    print("Failed to get Counter metric for test1 path. Error: %s" %e)
```

