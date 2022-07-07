# SpringWork2000G0

春課題のテンプレートリポジトリ

## 実行方法

### ローカル環境の Mysql と Gradle で起動する場合

1. プロジェクトのルートディレクトリで以下のどちらかで起動するコマンドを使用する．

```sh:console
# 開発環境にGradleの7.1系が入っている時
$ gradle tomcatRun

# 開発環境にGradleの7.1系が入っていない時
$ ./gradlew tR
```

2. http://localhost:8080/springwork2000g0 にアクセスする．

### docker-compose コマンドで Mysql と Gradle の 2 つを起動する場合

注意点として，Docker で起動する時に「8080，8081，3307」のポートがすでに使用されている時は正常に起動しません．

1. プロジェクトのルートディレクトリで以下ので起動するコマンドを使用する．

```sh:console
$ docker-compose -f docker/local/docker-compose.yml up --build
```

2. http://localhost:8080/springwork2000g0 にアクセスする．

## ディレクトリ構成

<pre>
.
├── README.md
├── build.gradle
├── docker
│   ├── README.md
│   ├── local
│   │   ├── docker-compose.yml
│   │   ├── java
│   │   ├── mysql
│   │   └── wait-for-it.sh
│   └── production
│       ├── docker-compose.yml
│       ├── java
│       └── mysql
├── docs
│   └── README.md
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── production-deploy.sh
├── setting
│   └── README.md
├── settings.gradle
└── src
    ├── README.md
    └── main
        ├── java
        └── webapp
</pre>
