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

## TODO

s3へのバックアップ環境用意。
