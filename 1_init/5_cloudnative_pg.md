# CloudNativePG

## 参照

[公式](https://artifacthub.io/packages/helm/cloudnative-pg/cloudnative-pg)

## 手順

インストール

```bash
helm repo add cnpg https://cloudnative-pg.github.io/charts
helm repo update
helm upgrade --install cloudnative-pg cnpg/cloudnative-pg \
  --namespace cnpg-system \
  --create-namespace \
  --wait
```

## 確認

```bash
kubectl get pod -n cnpg-system
```
