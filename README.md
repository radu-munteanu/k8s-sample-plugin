# k8s-sample-plugin
Sample Foo Custom Resource Plugin

## Description
This is a very basic example of a Kubernetes Plugin.

The plugin displays the Foo custom resources (as seen in the k8s.io/sample-contoller) with deployment, replicas and available replicas, similar to the `get deployments` command's output.

### Current Version

In Kubernetes 1.12 release, a few changes took place in kubectl that require some logic to be added in the plugin to make the namespaces and name filters work properly. The current version of the plugin shows all the Foo resources across all namespaces and ignores any name filters.

## Installation
```bash
# install
wget -O k8s-sample-plugin.zip https://gitlab.com/radu-munteanu/k8s-sample-plugin/-/archive/master/k8s-sample-plugin-master.zip && unzip -o k8s-sample-plugin.zip && sudo cp -f k8s-sample-plugin-master/kubectl-sample /usr/local/bin && sudo chmod +x /usr/local/bin/kubectl-sample && printf 'Success!\n'
# source cleanup
rm -rf k8s-sample-plugin-master
rm -f k8s-sample-plugin.zip
# plugin cleanup
sudo rm -f /usr/local/bin/kubectl-sample
```

## Use Case Examples
```bash
$ kubectl sample
RESOURCE        DEPLOYMENT_NAME     REPLICAS            AVAILABLE_REPLICAS
example-foo     example-foo         1                   1
example-foo-01  example-foo-01      2                   2
example-foo-02  dep-example-foo-02  1                   0
example-foo-03  example-foo-03      2                   0

# doesn't work yet
$ kubectl sample example-foo
RESOURCE     DEPLOYMENT_NAME  REPLICAS            AVAILABLE_REPLICAS
example-foo  example-foo      1                   1

# doesn't work yet
$ kubectl sample example-foo-
RESOURCE        DEPLOYMENT_NAME     REPLICAS            AVAILABLE_REPLICAS
example-foo-01  example-foo-01      2                   2
example-foo-02  dep-example-foo-02  1                   0
```
