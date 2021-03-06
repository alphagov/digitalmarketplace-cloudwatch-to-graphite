Digital Marketplace Cloudwatch to Graphite
=========================

> As of January 2019 this repo is no longer used by the Digital Marketplace, as we have switched to using Prometheus and alphagov/paas-prometheus-exporter.

## Purpose

Ships Cloudwatch metrics to Hosted Graphite.
Based on the work of https://github.com/crccheck/cloudwatch-to-graphite and the `leadbutt` script. Particularly config parsing to define metrics.

An example config file is included (`config.yaml.example`) to help you define the correct structure for your metrics.

## Initial setup

#### Setup a virtualenv, activate it and install python dependencies with pip

```
virtualenv venv
source venv/bin/activate
pip install -r requirements-dev.txt
```

#### Generate config.yaml

The `config.yaml` file defines what metrics are to be shipped to graphite. It is generated from the `config.yaml.j2` Jinja template using:

```
scripts/generate-config-yaml.py
```

## To run locally

Set the required environment variables

```
export HOSTED_GRAPHITE_API_KEY=your-key-here
export AWS_ACCESS_KEY_ID=your-access-key-id-here
export AWS_SECRET_ACCESS_KEY=your-secret-access-key-here
```

...and run

```
python app.py
```

## To deploy on PaaS

If you haven't done so already, go through the "Initial Setup" section above.

You will also need to create a manifest file using the example manifest (`manifest.yml.example`), filling in the necessary environment variables.
You can then deploy this to the PaaS by running:

```
cf push -f manifest.yml
```
