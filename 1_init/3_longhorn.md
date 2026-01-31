# Longhorn 設定

## 参照

[公式](https://docs.k3s.io/storage)

## なぜlonghornか

Local Storage Providerでも良いが、バックアップを有効活用したいので。
今後のクラスタ増強にも備えたい。

## 手順

open-iscsiが必要なので入れておく。

```sh
sudo apt install open-iscsi
```

Tailscale の Ingress を使うので、`ingressClassName: tailscale` とホスト名を Tailnet の FQDN にしておく。


`YOUR_TAILNET` を `tailnet-xxxx.ts.net` の形に置き換える。

```sh
helm upgrade --install longhorn longhorn/longhorn \
	--namespace longhorn-system \
	--create-namespace \
	--version 1.11.0 \
	--set persistence.defaultClassReplicaCount=1 \
	--set ingress.enabled=true \
	--set ingress.ingressClassName=tailscale \
	--set ingress.host=longhorn-raspberry01.YOUR_TAILNET \
	--set ingress.tls=true \
	--set ingress.tlsSecret=longhorn-tls
```

`ingress.tlsSecret` は Tailscale 側で自動発行されるため、存在しなくても作成される。

## 既存フォルダからデータをコピーする場合

1. pvcをまず作成する
1. longhornのUIから、volumeタブに移行。当該のPVCを選択。
1. 右上メニューからattachを選択。ノードを指定しattach.
1. attachしたノードでマウント処理。

```bash
sudo systemctl daemon-reload
sudo mount  /dev/longhorn/pvc-xxxxxxxxxxxxxxxx /tmp/pvc
```

1. /tmp/pvcの配下にコピーできる。

## TODO

s3へのバックアップ環境用意。
