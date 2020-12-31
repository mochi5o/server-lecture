## ハンズオン２ー自分のPCの仮想環境にサーバーを立てよう

### 仮想環境の準備

- [Vagrant](https://www.vagrantup.com/downloads)をインストール
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)をインストール

### CentOS7の環境を作る

VMの設定と作成はGUIからでもできますが、環境を揃えたいので今回はコマンドで作成していきます。

```
# 作業ディレクトリ作成
$ cd ~
$ mkdir VM-test
$ cd VM-test
$ vagrant init bento/centos-7

```

Vagrantfileの修正をする。
~/VM-test/Vagrantfile をVSCodeで開く。

もしくは、vimで開く。
```
$ vim Vagrantfile
```

ファイルを修正していく
```
# 20行目のコメントアウトを外す
config.ssh.insert_key = false

# 35行目のコメントアウトを外す、さらに ip: "192.168.33.10" の末尾の数字を下記に換えておく
config.vm.network "private_network", ip: "192.168.33.33"
```

スクショは[こちら](https://github.com/mochi5o/server-lecture/issues/8)にあります。

Vagrantfileの修正が終わったらVagrantを立ち上げる。

```
$ cd ~/VM-test
$ vagrant up
```

時間がかかるのでしばし待つ。。。

```
$ vagrant ssh
```

これでログインできたらOK！！


（解説）

```
mochiko@PMAC747S ~/VM> 　 # →これはローカルの環境
mochiko@PMAC747S ~/VM> vagrant ssh 

This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$ pwd
/home/vagrant
[vagrant@localhost ~]$　　# →これは仮想環境にSSHログインしたところ
```
