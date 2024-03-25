# Outline

## develop

```bash
kubectl create secret generic keycloak-secret -n keycloak --dry-run=client --from-env-file=.env --output=yaml > main/secret.yaml
```

```bash
kubectl apply -f init
kubectl apply -f main
```