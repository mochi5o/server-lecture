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


### Webサーバーに必要なソフトウェアをインストールする

- httpdのインストール

```
[vagrant@localhost ~]$ sudo -i
[root@localhost ~]# yum -y install httpd

# こんな感じのメッセージが出て終わる
Installed:
  httpd.x86_64 0:2.4.6-97.el7.centos

Dependency Installed:
  apr.x86_64 0:1.4.8-7.el7             apr-util.x86_64 0:1.5.2-6.el7             httpd-tools.x86_64 0:2.4.6-97.el7.centos             mailcap.noarch 0:2.1.41-2.el7

Complete!
[root@localhost ~]#

# 下記のコマンドでバージョン情報が出ればOK
[root@localhost ~]# httpd -v
Server version: Apache/2.4.6 (CentOS)
Server built:   Nov 16 2020 16:18:20
[root@localhost ~]#
```

- Apache起動

```
[root@localhost ~]# systemctl start httpd
[root@localhost ~]#
```

この時点でブラウザから、"192.168.33.33" にアクセスすると、Apacheのテスト画面が出ている
スクショは[こちら](https://github.com/mochi5o/server-lecture/issues/9)

- Mysqlインストール
先にMariaDBを削除

```
[root@localhost ~]# yum -y remove mariadb-libs.x86_64

# こんなメッセージが出て完了する
Removed:
  mariadb-libs.x86_64 1:5.5.68-1.el7

Dependency Removed:
  postfix.x86_64 2:2.10.1-9.el7

Complete!
[root@localhost ~]#
```

リポジトリ追加、Mysqlのインストール
```
[root@localhost ~]# yum -y install http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm

Complete!
[root@localhost ~]# yum -y install mysql-community-server

Complete!
[root@localhost ~]#

# バージョン確認できてたらOK！
[root@localhost ~]# mysqld --version
mysqld  Ver 5.7.32 for Linux on x86_64 (MySQL Community Server (GPL))
[root@localhost ~]#
```

mysqlの起動

```
[root@localhost ~]# systemctl start mysqld
[root@localhost ~]#
```


- PHPのインストール

```
[root@localhost ~]# yum -y install epel-release


Complete!
[root@localhost ~]#
```

```
[root@localhost ~]# rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm


Preparing...                          ################################# [100%]
Updating / installing...
   1:remi-release-7.8-1.el7.remi      ################################# [100%]
[root@localhost ~]#
```


```
[root@localhost ~]# yum -y install --enablerepo=remi,epel,remi-php70 php php-devel php-intl php-mbstring php-pdo php-gd php-mysqlnd

Complete!
[root@localhost ~]#
```

- PHPのバージョンが出たらOK
```
[root@localhost ~]# php -v
PHP 7.0.33 (cli) (built: Sep 29 2020 10:34:33) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
[root@localhost ~]#
```
