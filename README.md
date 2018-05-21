# k8s-sample-plugin
Sample Foo Custom Resource Plugin

## Description
This is a very basic example of a Kubernetes Plugin.

The plugin displays the Foo custom resources (as seen in the k8s.io/sample-contoller) with deployment, replicas and available replicas, similar to the `get deployments` command's output.

## Implementation
This might not be the best way to implement the required functionality, parsing the plain text output of other commands, but it does show how to use options (namespace) and command arguments (resource name prefix).

Probably a nicer implementation would be to use the JSON output.

## Installation
```bash
# install
wget -O k8s-sample-plugin.zip https://github.com/radu-munteanu/k8s-sample-plugin/archive/master.zip && unzip -o k8s-sample-plugin.zip && cp -rf k8s-sample-plugin-master/plugins/sample/* ~/.kube/plugins/sample && chmod +x ~/.kube/plugins/sample/sample && printf 'Success!\n'
# source cleanup
rm -rf k8s-sample-plugin-master
rm -f k8s-sample-plugin.zip
# plugin cleanup
rm -rf ~/.kube/plugins/sample
```

## Use Case Examples
```bash
$ kubectl plugin sample
RESOURCE        DEPLOYMENT_NAME     REPLICAS            AVAILABLE_REPLICAS
example-foo     example-foo         1                   1
example-foo-01  example-foo-01      2                   2
example-foo-02  dep-example-foo-02  1                   0

$ kubectl plugin sample example-foo
RESOURCE     DEPLOYMENT_NAME  REPLICAS            AVAILABLE_REPLICAS
example-foo  example-foo      1                   1

kubectl plugin sample example-foo-
RESOURCE        DEPLOYMENT_NAME     REPLICAS            AVAILABLE_REPLICAS
example-foo-01  example-foo-01      2                   0
example-foo-02  dep-example-foo-02  1                   0
```
