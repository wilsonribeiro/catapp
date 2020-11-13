# OpenShift YAML Files

These files are used to deploy the Nodejs app to an OpenShift environment.

The Deployment uses the local Image with tag `catapp:latest`. If the Nodejs app
was not built locally with the tag `catapp:latest`, then the Deployment will
fail.

## Build and run the Nodejs app using OpenShift

Follow the instructions in the [openshift/tekton/](openshift/tekton/README.md) directory to build
and run the Nodejs app using a cloud native Tekton Pipeline.

If you do not want to use a Tekton Pipeline to build and run the app, then
execute the following in your cluster:

```bash
NAMESPACE=catapp
buildah bud -t image-registry.openshift-image-registry.svc:5000/${NAMESPACE}/catapp:latest .
oc apply -f openshift/config/
```

Get the URL for your route with `oc get route catapp`, and open the route URL in your web browser.

*If your Kubernetes environment does not support LoadBalancer services, then
change the Service type in the [service.yaml](https://github.com/ncskier/catapp/blob/master/config/service.yaml#L9) file.*
