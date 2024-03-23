# Raspberry pi 5 上でk3sクラスタをデプロイ

## 参考

- [公式](https://k3s.io/)
- [ブログ](https://zenn.dev/kuma3303/articles/21d5725a94fcc1#k3s%25E3%2581%25AE%25E3%2582%25A4%25E3%2583%25B3%25E3%2582%25B9%25E3%2583%2588%25E3%2583%25BC%25E3%2583%25AB)

## 事前準備

raspberry pi 5一台用意。sshできるようにしておく。
OSはrasberry pi os 64 bit.

## k3sを選んだ理由

単純に軽いから。

## セットアップ

### ip 固定(ipv4)

設定ファイル(/etc/NetworkManager/system-connections/preconfigured.nmconnection)に以下を追記。
192.168.x.xxxはラズパイのアドレス、192.168.y.yyyはgatewayのアドレス。

```text
[ipv4]
method=manual
address1=192.168.x.xxx/24,192.168.y.yyy
```

適用

```bash
sudo nmcli connection reload
```

### cgroup有効化

設定ファイルに以下を追記。

```text
cgroup_memory=1 cgroup_enable=memory
```

### swap無効化

```bash
swapoff --all
systemctl stop dphys-swapfile.service
systemctl disable dphys-swapfile.service
```

### k3s インストール

```bash
curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
```

### kubectl 他のPCから可能に

同じLAN上の別のPCから接続できるようにしておく。
以下のコマンドでkubeconfigをコピーする。

```bash
scp raspberrypi.local:/etc/rancher/k3s/k3s.yaml ~/.kube/config
```

ipの部分だけraspberry piの固定化したipに変えておく。
httpsはhttpに直さず、そのままで。

```console
$ kubectl get po
No resources found in default namespace.
```
