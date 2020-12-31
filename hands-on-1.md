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

### サーバーにファイルを置いてみよう

- FTPクライアントでアクセスしたホームディレクトリに自分の名前のディレクトリを作る
- そこにindex.phpを置いて任意の文字列を出力するように記述する
- ブラウザからアクセスしてファイルの中身が表示されるかどうかを確かめよう

### DEMO

- コマンドラインからsftp接続した時のサーバーの様子をみてみよう
- UbuntuノートPCにオーナー権限に近い権限でsshで入ってみたらどう見える？

