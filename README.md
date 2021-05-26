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


## Installing the plugin

In order to upload the plugin you can do that through Cloudify console or through cli

```
cfy plugin upload -y plugin.yaml cloudify_web_monitoring_plugin-1.0-centos-Core-py27.py36-none-linux_x86_64.wgn
```

## Example

check blueprints sub-directory for the example
