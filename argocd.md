# Installing ArgoCD
1. We will start with launching minikube cluster.
```bash
minikube start --driver=docker
```
2. Create a namespace for argocd
```bash
kubectl create namespace argocd
```
3. Apply ArgoCD manifest installation file from ArgoCD [github repository](https://github.com/argoproj/argo-cd/releases)
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.12.6/manifests/install.yaml
```
4. Verify the installation by getting all the objects in the ArgoCD namespace.
```bash
kubectl get all -n argocd
```
5. wait till all pods in that namespace running

# Access ArgoCD UI
1. we need to do a port forwarding from the argocd-server service
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
2. now lets go to browser with http://localhost:8080
3. retrieve password from secret in argocd namespace
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
4. the default login username is ```admin``` with the password we took above
