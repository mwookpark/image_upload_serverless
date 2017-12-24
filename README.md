# Serverless練習


レポジトリのままだとデプロイ時に失敗する為、以下の内容を修正
・本来設定しているaws cliのリージョンに合わせる。（us-west-2　→　ap-northeast-1）
・DynamoBDのストリームを設定（原本はcommentされている）
・デプロイ時に「{bucket名} already exists.」とエラーになる為、下記を修正

sample-thumbnails→sample-thumbnails-park
sample-uploads   →sample-uploads-park

## デプロイ失敗時の手順

・S3から作られているbucketを削除
・CloudFormationからスタックを削除

原文は下記を参考。

# ServerlessSample
[Software Design 2017年10月号](http://gihyo.jp/magazine/SD/archive/2017/201710)にピクスタでも一部のシステムで使用している[ServerlessFramework](https://serverless.com/)のハンズオン記事を寄稿しました。
これはその記事の中で使用するサンプルアプリケーションリポジトリです。

## 概要
AWSの各サービスとServerlessFrameworkを使用し、画像アップロードシステムを作成します。具体的な処理は下記の通りです。
1. API Gatewayで設定したAPIエンドポイントに画像データをPOST
2. Lambdaが画像を受けとり、S3に格納
3. S3にアップロードされたことをトリガーにDynamoDBに画像情報などを格納
4. DynamoDBに格納したことをDynamoDBStreamsを通じてサムネイル作成処理用のLambdaが起動

## インストール
まず初めに、ServerlessFrameworkのインストールを行います。
```
$ npm install serverless
$ sls -v
1.10.2
```

アプリケーションをデプロイするには`aws configure`コマンドでアクセスキーなどのクレデンシャル情報を設定します。aws cliのインストールは[公式ドキュメント](http://docs.aws.amazon.com/ja_jp/streams/latest/dev/kinesis-tutorial-cli-installation.html)を参照

```
$ aws configure
AWS Access Key ID [********************]: 
AWS Secret Access Key [********************]: 
Default region name [us-west-2]: 
Default output format [text]:
```

## 使い方
awsコマンドの設定ができたらデプロイの準備が完了です。デプロイコマンドは下記の通りです。
```
$ sls deploy -v
```

## ライセンス

[MIT](https://github.com/tcnksm/tool/blob/master/LICENCE)

## 作者

[星 直史](http://blog.naoshihoshi.com/)
