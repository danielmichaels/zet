# kubernetes tips

Random helpers

**Create Namespace if not Exists**
- `kubectl create namespace test --dry-run -o yaml | kubectl apply -f -`

**Wait for deployment to rollout**

This will wait until the deployment has completed and very useful in 
bash scripting.

- `kubectl rollout status deployment argocd-repo-server -n argocd`

Tags:

    #kubernetes #bash #kubectl
