### intall ingress-nginx
```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace \
  -f controller-config.yaml
```
or
if ingress-nginx-controller already installed,
```bash
kubectl edit -n ingress-nginx configmap ingress-nginx-controller
```
```yaml
data:
  # log-level: "debug"
  enable-opentelemetry: "true"
  opentelemetry-operation-name: "HTTP $request_method $service_name $uri"
  opentelemetry-trust-incoming-span: "true"
  otlp-collector-host: "jaeger.otel-test.svc"
  otlp-collector-port: "4317"
  # otel-max-queuesize: "2048"
  # otel-schedule-delay-millis: "5000"
  # otel-max-export-batch-size: "512"
  # otel-service-name: "nginx-proxy" # Opentelemetry resource name
  # otel-sampler: "AlwaysOn" # Also: AlwaysOff, TraceIdRatioBased
  # otel-sampler-ratio: "1.0"
  # otel-sampler-parent-based: "true"
...
```

### install chart
```bash
helm uninstall -n otel-test myrelease; helm install -n otel-test myrelease mychart/; watch 'kubectl get all -n otel-test';
```

### Reference
- [ingress-nginx official document: opentelemetry](https://kubernetes.github.io/ingress-nginx/user-guide/third-party-addons/opentelemetry/)
- [todo source (docker-compose)](https://github.com/habmic/opentelemetry-101)