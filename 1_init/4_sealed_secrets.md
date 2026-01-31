# Dashbord

## 参照

[公式](https://github.com/bitnami-labs/sealed-secrets)

## 手順

インストール

```bash
helm repo add sealed-secrets https://bitnami-labs.github.io/sealed-secrets
helm repo update
helm install sealed-secrets sealed-secrets/sealed-secrets \
  --namespace kube-system \
  --wait
```

