# Outline

## develop

```bash
kubectl create secret generic langflow-secret -n langflow --dry-run=client --from-env-file=.env --output=yaml > main/secret.yaml
```

```bash
kubectl apply -f init
kubectl apply -f main
```
