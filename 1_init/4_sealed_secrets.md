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

### kubeseal 利用時の指定

この手順だと controller 名は `sealed-secrets`、namespace は `kube-system`。
`kubeseal` 実行時に以下を指定する。

```bash
kubeseal \
  --controller-name=sealed-secrets \
  --controller-namespace=kube-system
```

