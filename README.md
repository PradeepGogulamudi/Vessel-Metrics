# Vessel Metrics Python Package
This is Vessel Metrics Python package to collect Application/Micro-Service level Metrics and act as a scrape target for Prometheus to scrape for every pre-defined time interval.

This repository contains a very fast and light Metrics Collection client for Vessel Services.

Programming languages supported so far are:

-->Python

## Vessel Metrics Python Package
You can download the Vessel Metrics library as Python Package from Pfizer Artifactory, i.e.

```bash
pip install vslmetrics==0.0.2 -i https://artifactory-oh.pfizer.com/artifactory/api/pypi/vessel-py-dev-local/simple
```
or

You can clone vessel-metrics from the following repository, i.e.
```bash
pip install git+http://bitbucket-insightsnow.pfizer.com:7990/scm/ga/vessel-metrics.git
```

After installing package, import classes and methods to your microservice required to collect application metrics, e.g.

```python
from vslmetrics.metrics import setup_metrics
from vslmetrics.counter import CounterMetric
from vslmetrics.register import app_register
from vslmetrics.guage import GuageMetric
```
Add the following lines of code to your mainfile.py

```python
app = Flask(__name__)
setup_metrics(app)
app_register(app)

app.config['CORS_HEADERS']='content-Type'
cors = CORS(app)

cm = CounterMetric(metric_description= "hello", metric_name="test", metric_key_value= {"key1":"ad"}, svc_version="0.11", op_code="asd", app_id="add")
CM = cm.create_metric()
```
Add the following code to each individual @app.route method
```python
try:
	      CM.labels(svc_version="0.11", op_code="asd", app_id="add", key1 = "dad").inc()
```

