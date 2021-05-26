cloudify-web-monitoring-plugin
===================


# Description

A Cloudify Plugin that monitor a URL response time and based on metrics will trigger scale up or down


## Building the plugin

In order to build the plugin you need to have wagon installed on a virtual environment

```
wagon create -r dev-requirements.txt --build-tag "centos-Core" -v -f .
```

or you can use Cloudify wagon builder Docker images

```
docker run -v {path_to_plugin}/:/packaging cloudifyplatform/cloudify-centos-7-py3-wagon-builder
```

## Example

check blueprints sub-directory for the example
