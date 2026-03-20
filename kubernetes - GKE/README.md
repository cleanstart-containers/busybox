# BusyBox Kubernetes Deployment

Simple Kubernetes deployment for BusyBox HTTP server on GKE.

## Files
- `namespace.yaml` - Creates namespace
- `deployment.yaml` - Deploys BusyBox pod with HTTP server
- `service.yaml` - Exposes service via LoadBalancer

## Deploy

```bash
# Apply in order to avoid namespace timing issues
kubectl apply -f namespace.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

## Test

```bash
# Check deployment status
kubectl get pods -n busybox-sample
kubectl get service -n busybox-sample

# Get external IP and test directly
kubectl get service -n busybox-sample
curl http://<EXTERNAL-IP>
# please use GKE cluster to make this IPaddress available. If you are running locally, this will assign nodeport only, but not loadbalancer..

# Expected response: <h1>Hello from BusyBox on Kubernetes!</h1>
```

## Access

Once deployed, you'll get an external IP like `35.184.5.205`. Access your app at:
- **URL**: http://<EXTERNAL-IP>
- **Response**: `<h1>Hello from BusyBox on Kubernetes!</h1>`

## Cleanup

```bash
kubectl delete -f .
```
