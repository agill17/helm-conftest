# Conftest Helm plugin

A [Helm](https://helm.sh/) plugin for testing Helm charts with Open Policy Agent, using [conftest](https://github.com/instrumenta/conftest).


## Installation

Install the plugin using the built-in plugin manager.

```
helm plugin install https://github.com/instrumenta/helm-conftest
```


## Usage

Assuming you have policy defined in the `policy` folder, you can point the plugin at your chart.

```
$ helm conftest .
FAIL - release-name-mysql must include Kubernetes recommended labels: https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/#labels
Error: plugin "conftest" exited with error
```

Conftest has a number of flags which can alter it's behaviour, from changing the output formatting to
specifying where to find the policy files. Conftest options are automatically passed to Conftest,
with any other options being passed to Helm in the same way as `helm template`. This means you
could set values before validating the chart. eg.

```
helm conftest charts/stable/nginx-ingress --set controller.image.tag=latest
```


## Docker

The Helm Conftest plugin is also available as a standalone Docker image. Simply mount your Chart source
code at `/chart` and include the `policy` dirctory along with your chart and run:

```
docker run --rm -it -v $(pwd)/snyky:/chart instrumenta/helm-conftest
```
