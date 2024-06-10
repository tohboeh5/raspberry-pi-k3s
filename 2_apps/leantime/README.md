# Outline

## develop

```bash
kubectl create secret generic leantime-secret -n leantime --dry-run=client --from-env-file=.env --output=yaml > main/secret.yaml
```

```bash
kubectl apply -f init
kubectl apply -f main
```
