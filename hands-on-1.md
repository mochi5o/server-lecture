## サーバーへ接続してやること

### ブラウザからのアクセス
- （WIP）192.168.1.1へアクセスしよう
- PHP INFOがでたらOK
  - この画面がどうやって表示されているかはやりながら説明します

### DEMO

- ノートPCがサーバーとして動作していることを確認しよう
  - ノートPCの/var/www/html/にtestディレクトリを作る
  - /var/www/html/test/の下にファイルをおく
  - ブラウザ経由でtestディレクトリがみんなからも見えるようになる
  - testフォルダにブラウザからアクセスしてみよう

### FTPクライアントの準備

- cyberduckをインストール
  - [ここからインストールできます](https://cyberduck.io/download/)
    - [Windowsの手順](https://tab-log.com/ftp-cyberduck)
    - [Macの手順](https://tab-log.com/mac-cyberduck)
- 接続設定の情報をいれて接続
  - https://github.com/mochi5o/server-lecture/issues/7
- testフォルダとindex.phpが見えたらOK
- index.phpをダウンロード、ファイルの中身を開いて確認してみよう

#### ノートPCへの接続情報

```
ユーザー名：sftp-user
パスワード：別途共有
```
### ファイルのアップロードとダウンロードを試してみよう

html/sftp-userのディレクトリにはファイルがアップできるようになっています。

- アップロード

<img width="665" alt="スクリーンショット 2020-12-31 14 39 03" src="https://user-images.githubusercontent.com/41158022/103396342-fc3c5000-4b75-11eb-86fb-1f04dbe926f4.png">


- ダウンロード

<img width="520" alt="スクリーンショット 2020-12-31 14 37 24" src="https://user-images.githubusercontent.com/41158022/103396303-bd0dff00-4b75-11eb-914e-14c84b2a250c.png">

<img width="712" alt="スクリーンショット 2020-12-31 14 15 22" src="https://user-images.githubusercontent.com/41158022/103396309-c5663a00-4b75-11eb-80a9-098f2504dcc9.png">



#### ハンズオン

- html/sftp-user の中に自分の名前のディレクトリを作って、任意のindex.htmlをアップロードする
- 上記ファイルをブラウザに表示しよう
- htmlディレクトリ直下のindex.phpをダウンロードして中身を見てみよう

#### DEMO

- 特定のディレクトリにしかファイルをアップロードできない理由
- コマンドラインからsftp接続した時のサーバーの様子をみてみよう
- サーバーマシン上でみんながアップしたファイルを見てみる
- index.php に記載されている内容の解説
- 複数端末から接続されていることをサーバーマシン上で確認する
- UbuntuノートPCにオーナー権限に近い権限でsshで入ってみたらどう見える？

