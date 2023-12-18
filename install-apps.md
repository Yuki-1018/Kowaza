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
