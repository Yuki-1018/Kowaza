# プロキシサーバー構築手順
squidを使う簡単なプロキシサーバーの構築手順です。
# 方法
まず必要なもの
- LinuxのPC (今回はAmazon Linux 2023をAWSのEC2で使用します。）
## squidのインストール
まずルートユーザーに切り替えます。
```
sudo su
```
squidをインストールし開始、自動起動をオンにする。
```
yum -y install squid
systemctl start squid
systemctl enable squid
```
## 設定ファイルの編集
ブラックリストの追加をします。
```
vim /etc/squid/squid.conf
```
下記のところのコメントアウトを外してください。
```
cache_dir ufs /var/spool/squid 100 16 256
```
そして最上部に下記のものを付け足してください。
```
acl blacklist dstdomain "/etc/squid/blacklist"
http_access deny blacklist
http_access allow all
```
:wqコマンドで保存し次にブラックリストのファイルを追加します。
```
cd /etc/squid/
touch blacklist
vim blacklist
```
ブラックリストの記述例です。
必ず前頭にドットを入れてください。
ブラックリストに追加したドメインへアクセスできなくなります。
```
.example.com
.google.com
.yahoo.co.jp
```
## squidを再起動して完了
```
systemctl restart squid
```
# プロキシ設定（クライアント側）
PCのグローバルIPアドレスとポート番号3128でログインしてください。ユーザー名、パスワードは入力しないでください。
