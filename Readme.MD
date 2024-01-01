
##K3D

###Set up cluster and network

Creating the local cluster:

```bash
k3d cluster create chatbox --servers 1 --agents 1 --port 9080:80@loadbalancer --registry-config ~/Code/School/S6/ChatBox-backend/k8s/k3d-registry-config.yml
```

```bash
k3d cluster list
```

```bash
k3d cluster delete <name>/--all
```

check if running
```bash
kubectl get nodes
```

###Put in the yamls

To deploy the image to our kubernetes cluster we need the following command.
```bash
kubectl apply -f *-deployment.yaml
```

TODO: write how the port number in the deployment file is for the container, not the app hosted inside of it.

Delete deployment
```bash
kubectl delete deployment [name]
```
To check if a deployment was succesfull we can run.
```bash
kubectl get deployment
```

If we want the deployment and its pods to be accessed on the network, we need to enable a service for it.
```bash
kubectl apply -f *-service.yaml
```


> apply ingress


## Configuration

Example from gateway, to make config based on existing config files that Kubernetes pods use:

- pass multiple files if you want, use ``--from-file=<path>``
- ``-o`` prints the output to console, can choose the output type (like json or yaml)
- ``--dry-run=client`` is used to not contact kubernetes cluster and save it. We just want the file to manually apply

```bash
kubectl create configmap gateway-config --from-file=../../Gateway/appsettings.json --from-file=../../Gateway/ocelot.json -o yaml --dry-run=client > gateway-configmap.yml
```

TODO: how do we apply this output to a pod?

## Port forward pod
To check whenever we can reach the api we can use the `kubectl port-forward` command.

```bash
kubectl port-forward [POD_NAME] <external-port>:<application:port>

