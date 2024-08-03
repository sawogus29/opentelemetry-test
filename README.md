### intall ingress-nginx
```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

### install chart
```bash
helm uninstall -n otel-test myrelease; helm install -n otel-test myrelease mychart/; watch 'kubectl get all -n otel-test';
```