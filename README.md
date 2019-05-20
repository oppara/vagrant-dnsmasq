# ローカル開発環境用のDNSサーバー

Vagrant で立ち上げた Web サーバに iPhone や Android からアクセスさせるための DNS サーバー


## 手順

1. スマホからアクセスさせたい Virtual Machine (VM) のネットワーク設定を public にする

```Vagrantfile
config.vm.network "public_network", bridge: "en0: Wi-Fi (Wireless)"
```

2. スマホからアクセスさせたい VM を `vagrant up`

network interfaces を聞かれたらよしなに選択する（以下の場合は、`1` を入力）

```
==> default: which network to bridge to.
==> default: Available bridged network interfaces:
1) en0: Wi-Fi (AirPort)
2) en1: Thunderbolt 1
3) en2: Thunderbolt 2
4) p2p0
5) awdl0
6) bridge0
==> default: When choosing an interface, it is usually the one that is
==> default: being used to connect to the internet.
    default: Which interface should the network bridge to?
```

3. スマホからアクセスさせたい VM の IPアドレスを確認

```
$ vagrant ssh -c "ip addr show"

または

$ vagrant ssh -c "ifconfig"
```

4. 3 で確認した IPアドレスを `etc/hosts` に設定

5. この VM を `vagrant up`

6. この vm の IPアドレスを確認

7. スマホの DNS 設定に 6 で確認した IPアドレスを追加する

<img src="https://raw.githubusercontent.com/oppara/vagrant-dnsmasq/assets/iphone_01.png" width="25%">
<img src="https://raw.githubusercontent.com/oppara/vagrant-dnsmasq/assets/iphone_02.png" width="25%">
<img src="https://raw.githubusercontent.com/oppara/vagrant-dnsmasq/assets/iphone_03.png" width="25%">


## 環境

```
% sw_vers                                                                                                                                                                                            master
ProductName:    Mac OS X
ProductVersion: 10.14.4
BuildVersion:   18E226

% VBoxManage -v                                                                                                                                                                                      master
6.0.8r130520

% vagrant -v                                                                                                                                                                                         master
Vagrant 2.2.4
```


## 参考

* [iPhoneアプリを開発するための環境をローカルに構築してみた！！](https://qiita.com/kouji555/items/c1d383f48ee7ed418bcc)

