# 概要

EC外部連携API作成時にクローンするだけで動くサーバーが見つけられなかったので作成しました。

参考
https://github.com/EC-CUBE/ec-cube?tab=readme-ov-file

# サーバーのセットアップ

## SSL証明書の作成

mkdir -p app/ssl

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout app/ssl/server.key -out app/ssl/server.crt -subj "/CN=localhost"

## .envファイルの作成
html/.env.installを.envにする

## サーバーの起動
docker-compose up -d

https://localhost:8443
