## 手元の環境での実行方法

下記を実行する．

```console:console
$ docker-compose -f docker/local/docker-compose.yml up --build
```

以下でも実行可能です．

```console:console
$ gradle composeUp -Penvironment="local"
```

以上で http://localhost:8080/springwork2000g0 にアクセスできれば完了．

## 本番環境へのデプロイ方法

### 1. docker image のビルド

ローカル環境で本番用の`docker-compose.yml`を使って docker image を build する．

```console:console
$ docker-compose -f docker/production/docker-compose.yml build
```

以下でも実行可能です．

```console:console
$ gradle composeUp -Penvironment="production"
```

以上で`diamond.u-gakugei.ac.jp/springwork2000g0_db`と`diamond.u-gakugei.ac.jp/springwork2000g0_app`の 2 つの docker image がビルドされる．

`docker image ls`でイメージ一覧を確認した際に以下のような出力がされていれば成功です 🙆‍♂️

```console:console
$ docker image ls
REPOSITORY                                                        TAG                          IMAGE ID            CREATED             SIZE
diamond.u-gakugei.ac.jp/springwork2000g0_db                                    latest                       0d7bc01e233e        4 minutes ago       581MB
diamond.u-gakugei.ac.jp/springwork2000g0_app                                   latest                       ecf65aee74c0        4 minutes ago       447MB
```

### 2. diamond に push

1.でビルドした docker image を diamond に push する．

はじめに`docker login`で diamond の docker registry に認証を通す．

```console:console
$ docker login diamond.u-gakugei.ac.jp
```

ユーザー名とパスワードを聞かれるので入力する．

認証ができたら以下のコマンドで push する．

```
docker push diamond.u-gakugei.ac.jp/springwork2000g0_app:latest
docker push diamond.u-gakugei.ac.jp/springwork2000g0_db:latest
```

### 3. diamond に アクセス

ここからの操作は diamond にアクセスしてから行う．

2.で push したイメージを pull する．

```
docker pull diamond.u-gakugei.ac.jp/springwork2000g0_app:latest
docker pull diamond.u-gakugei.ac.jp/springwork2000g0_db:latest
```

pull したイメージを元にコンテナを生成する ✨

```
docker container run -d --net=springwork2000g0 --name=springwork2000g0_app diamond.u-gakugei.ac.jp/springwork2000g0_app
docker container run -d --net=springwork2000g0 --name=springwork2000g0_db diamond.u-gakugei.ac.jp/springwork2000g0_db
```

### 4. nginx のリバースプロキシの設定

nginx のリバースプロキシを設定しアプリケーションにアクセスできるようにする．

そのためにまずアプリケーションが動作している IP アドレスを調べる．

`docker container inspect`コマンドを使う．

```
docker container inspect springwork2000g0_app | grep IPAddress
            "SecondaryIPAddresses": null,
            "IPAddress": "",
                    "IPAddress": "172.18.0.2",
```

この設定を nginx に加える．

```
sudo vi /etc/nginx/nginx.conf
```

tomcat は 8080 ポートで動いてるので注意

```conf
location /springwork2000g0 {
  proxy_pass http://172.18.0.2:8080;
}
```

設定したあとは nginx を再起動する．

```
sudo systemctl restart nginx
```

以上で https://diamond.u-gakugei.ac.jp/springwork2000g0 にアクセスできれば完了です．
