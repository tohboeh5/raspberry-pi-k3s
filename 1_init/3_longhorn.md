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

以下インストール。

```sh
kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/v1.6.0/deploy/longhorn.yaml
```

replica数変えとく

```bash
kubectl edit configmap longhorn-storageclass -n longhorn-system
```

```yaml
apiVersion: v1
data:
  storageclass.yaml: 
   parameters:
      numberOfReplicas: "1"
```

ingress立てておく。

```sh
kubectl apply -f longhorn_ingress.yam
```

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
