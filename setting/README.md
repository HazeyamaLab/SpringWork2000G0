# テンプレートからリポジトリを準備する手順

## リポジトリの作成

Hazeyamalab の GitHub から新しくレポジトリを作成する．
その時に下記の画像のように，Repository template で`Hazeyamalab/SpringWork2000G0`を選択し作成する．

<img width="1231" alt="スクリーンショット 2020-10-22 14 53 47" src="https://user-images.githubusercontent.com/38200453/96830640-bc226800-1476-11eb-8aa5-7a034b99bc50.png">

## プロジェクトのパスを変更

下記に示すファイルにおいて，テンプレートで設定してある「SpringWork2000G0」の部分をそれぞれのグループ名(SpringWork20XXGX)で変更する．

- SpringWork20XXGX/README.md
- SpringWork20XXGX/build.gradle
- SpringWork20XXGX/settings.gradle
- SpringWork20XXGX/docker/README.md
- SpringWork20XXGX/docker/local/docker-compose.yml
- SpringWork20XXGX/docker/production/docker-compose.yml
- SpringWork20XXGX/src/main/webapp/index.jsp
- SpringWork20XXGX/.github/workflows/ci.yml
- SpringWork20XXGX/.github/workflows/cd.yml

## デプロイの準備

### 手動で行う場合

[デプロイ方法](https://github.com/HazeyamaLab/SpringWork2000G0/tree/master/docker)を参考にしてデプロイをする．

### Portainer で行う場合
