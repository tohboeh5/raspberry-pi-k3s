# tailscale operator

## 参考

[公式](https://tailscale.com/kb/1236/kubernetes-operator)

## 準備

### ACL設定

tailscaleのダッシュボードから、Access controlタブに入り、editfile内で以下記述を追加。

```json
"tagOwners": {
   "tag:k8s-operator": [],
   "tag:k8s": ["tag:k8s-operator"],
}
```

### デバイス追加

tailscaleのダッシュボードから、settingsタブに入り、左メニューのTrust credentialsを選び、「New credential」を押す。
`Devices Core, Auth Keys, Services write scopes, and the tag tag:k8s-operator`を設定し、「generate client」を押す。
出てきたIDとSECRETを環境変数TAILSCALE_CLIENT_IDとTAILSCALE_CLIENT_SECRETに格納。

### デプロイ

```bash
helm repo add tailscale https://pkgs.tailscale.com/helmcharts
helm repo update
helm upgrade \
  --install \
  tailscale-operator \
  tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId=$TAILSCALE_CLIENT_ID \
  --set-string oauth.clientSecret=$TAILSCALE_CLIENT_SECRET \
  --wait
```
