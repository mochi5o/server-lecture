## ハンズオン２ー自分のPCの仮想環境にサーバーを立てよう

### 仮想環境の準備

- [Vagrant](https://www.vagrantup.com/downloads)をインストール
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)をインストール

### CentOS7の環境を作る

以下、VMとはVirtualMacine、つまり仮想マシンのことです。

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
# 35行目のコメントアウトを外す、さらに ip: "192.168.33.10" の末尾の数字を下記に換えておく
config.vm.network "private_network", ip: "192.168.33.33"
```

設定のスクショは[こちら](https://github.com/mochi5o/server-lecture/issues/8)にあります。

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
[vagrant@localhost ~]$    # →これは仮想環境にSSHログインしたところ
[vagrant@localhost ~]$ pwd
/home/vagrant
[vagrant@localhost ~]$
```


### Webサーバーに必要なソフトウェアをインストールする

- Apacheインストール、起動

```
### Apacheのインストール
  1  sudo yum -y install httpd
  2  httpd -v			# バージョンが出たらOK
  3  sudo systemctl start httpd  # Apacheの起動
```
バージョン情報はこんな感じ。多少ことなっていてもOK
```
[root@localhost ~]# httpd -v
Server version: Apache/2.4.6 (CentOS)
Server built:   Nov 16 2020 16:18:20
[root@localhost ~]#
```

この時点でブラウザから、"192.168.33.33" にアクセスすると、Apacheのテスト画面が出ている
スクショは[こちら](https://github.com/mochi5o/server-lecture/issues/9)

- ブラウザから仮想マシン上のファイルを確認する
```
### ディレクトリを移動
  4  cd /var/www/html
  5  pwd      # /var/www/htmlに移動していることを確認する
  6  ls				# おそらくなにもないはずなのでファイルを追加する
  7  sudo touch index.html
### test.htmlの編集。中身はなんでもOK
  8  sudo vi
### Apacheのリスタート
  9  sudo systemctl restart httpd
```
192.168.33.33 にアクセスしてファイルの中身が見れたらOK

- ついでなので、phpがまだ動いていないことを確認する
```
### phpのファイルを用意する
 10 sudo touch test.php
 11 sudo vi
### test.phpの中身は下記のように編集する
<?php
phpinfo();
```     
192.168.33.33/test.php にアクセスしてファイルの中身が見れたらOK



- PHPのインストール

```
### PHPをインストールする
 12 sudo apt install ./vagrant_2.2.7_x86_64.deb
 13 sudo yum -y install epel-release
 14 sudo rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
 15 sudo yum install -y --enablerepo=remi,remi-php71 php php-deval php-mbstring php-pdo php-mysqlnd php-gd
 16 php -v			# バージョンが出たらOK
 17 cd /var/www/html
 18 ls				# test.phpとindex.htmlがあるはず
### 再び192.168.33.33/test.php にアクセスしてみる   
### もしファイルが開けなかったらリスタートしてみる
 19 sudo systemctl restart httpd
```
再び192.168.33.33/test.php にアクセスしてPHPが動作していることを確認する


スクショは[こちら](https://github.com/mochi5o/server-lecture/issues/9)にあります。

### VM関連の使ったコマンドまとめ

- vagrant up
  - Vagrantfileを元にしてVMを立ち上げるコマンド。
- vagrant ssh
  - VMにSSHするためのコマンド。このコマンドでログインした後の操作はVM上でのコマンド実行となる。
  - VMからログアウトするには`Ctrl＋d` でOK
- vagrant halt
  - VMをシャットダウンするコマンド

### ハンズオンが終わったら、、、、

不要な人は環境を削除しておきましょう（もちろん、このままいろいろ遊んでみてもOK）

- VirtualBoxを開いて、今日作ったVMを削除しておく
  - スクショは[こちら](https://github.com/mochi5o/server-lecture/issues/8#issuecomment-753431124)
- VM-testディレクトリごと消す

以上！お疲れ様でした。
