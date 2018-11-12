# k8s-sample-plugin
Sample Foo Custom Resource Plugin

## Description
This is a very basic example of a Kubernetes Plugin.

The plugin displays the Foo custom resources (as seen in the k8s.io/sample-contoller) with deployment, replicas and available replicas, similar to the `get deployments` command's output.

### Current Version

The current version of the plugin shows all the Foo resources across all namespaces.

## Installation
```bash
# install plugin
wget -O k8s-sample-plugin.zip https://gitlab.com/radu-munteanu/k8s-sample-plugin/-/archive/master/k8s-sample-plugin-master.zip && unzip -o k8s-sample-plugin.zip && sudo cp -f k8s-sample-plugin-master/kubectl-sample /usr/local/bin && sudo chmod +x /usr/local/bin/kubectl-sample && printf 'Success!\n'
# source cleanup
rm -rf k8s-sample-plugin-master
rm -f k8s-sample-plugin.zip
# plugin cleanup
sudo rm -f /usr/local/bin/kubectl-sample
```

## Use Case Examples
```bash
# the resources in the example below can be found in this repo, inside resources directory

$ kubectl create -f "resources/crd.yaml"
customresourcedefinition.apiextensions.k8s.io/foos.samplecontroller.k8s.io created

# optional: start sample controller in order to update these resources

$ kubectl create namespace sample-namespace
namespace/sample-namespace created

$ kubectl create -f "resources/example-foo-01.yaml"
foo.samplecontroller.k8s.io/example-foo-01 created

$ kubectl create -f "resources/example-foo-02.yaml"
foo.samplecontroller.k8s.io/example-foo-02 created

$ kubectl create -f "resources/example-foo-03.yaml" --namespace sample-namespace
foo.samplecontroller.k8s.io/example-foo-03 created

$ kubectl sample
NAMESPACE         RESOURCE        DEPLOYMENT_NAME     REPLICAS            AVAILABLE_REPLICAS
default           example-foo-01  example-foo-01      2                   2                 
default           example-foo-02  dep-example-foo-02  1                   1                 
sample-namespace  example-foo-03  example-foo-03      2                   0                 
```

