# AWSフルコース 第１３回課題（最終課題）CloudFormationバージョン
## 概要
- CloudFormationによるインフラ構築
- Ansibleによるサーバー環境構築とアプリのデプロイ
- Serverspecによるインフラテスト
- 上記をGItHubへのpushをトリガーにCircleCIで、CloudFormation → Ansible → Serverspecを自動でおこなう。

## 構成図
![構成図](images/aws_lecture13_07diagram.png)

## 補足
- CloudFormationは[第１０回課題](https://github.com/mkmmr/aws-practice/tree/main/lecture10)で作成済みのものを使用しています。
- デプロイ用のアプリは課題用に提供されている[サンプルアプリ](https://github.com/yuta-ushijima/raisetech-live8-sample-app)を使用しています。
- この記事のコードは[こちらのリポジトリ](https://github.com/mkmmr/circleci-practice)をご参照ください。
- 同じ内容で[Terraformバージョン](https://github.com/mkmmr/terraform-practice)も作成しました。

## 実装手順
コードや実装手順の詳細は[こちらのリポジトリ](https://github.com/mkmmr/circleci-practice)をご参照ください。

1. Ansble 実装手順
    - ローカルPCにAnsbleをインストール
    - ローカルPCにSSH接続用キーを準備
    - AnsibleからEC2インスタンスに接続
    - playbook.ymlにサーバー環境構築とアプリのデプロイについて記述
    - Ansibleで遭遇したエラー
2. CircleCI 実装手順
    - CircleCIとAWSをOIDC連携
    - CircleCIにCloudFormationを実装
    - CircleCIにAnsibleを実装
3. Serverspec 実装手順
    - CircleCIにServerspecを実装
    - ServerspecからEC2にSSH接続
    - Serverspecテストの実装
    - Serverspecで遭遇したエラー

## 成功画面
### ◆ CircleCI成功画面
![CircleCIのWorkflow成功画面](images/aws_lecture13_01CircleCIWorkflow.png)
### ◆ CloudFormation成功画面
![CircleCIでのCloudFormation成功画面](images/aws_lecture13_02CiecleCICloudFormation.png)
### ◆ Ansible成功画面
![CircleCIでのAnsible成功画面](images/aws_lecture13_03CiecleCIAnsible.png)
### ◆ Serverspec成功画面
![CircleCIでのServerspec成功画面](images/aws_lecture13_04CiecleCIServerspec.png)

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題CloudFormationバージョン)

## アプリの正常動作確認
### ◆ New Fruit Saveした時
![アプリの正常動作確認](images/aws_lecture13_08AppNewItemSave.png)
### ◆ 新規追加後の一覧画面
![アプリの正常動作確認](images/aws_lecture13_05App.png)
### ◆ Destroyした時
![アプリの正常動作確認](images/aws_lecture13_09AppItemDestroy.png)

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題CloudFormationバージョン)

## S3への画像登録確認
![S3への画像登録確認](images/aws_lecture13_06S3status.png)

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題CloudFormationバージョン)
