# AWSフルコース 第１３回課題（最終課題）Terraformバージョン
## 概要
- Terraformによるインフラ構築
- Ansibleによるサーバー環境構築とアプリのデプロイ
- Serverspecによるインフラテスト
- 上記をGItHubへのpushをトリガーにCircleCIで、Terraform → Ansible → Serverspecの実装を自動でおこなう。

## 構成図
![構成図](images/aws_lecture13_Terraform_12diagram.png)

## 補足
- Terraformの内容は[第１０回課題](https://github.com/mkmmr/aws-practice/tree/main/lecture10)で作成したCloudFormationと同じです。
- デプロイ用のアプリは課題用に提供されている[サンプルアプリ](https://github.com/yuta-ushijima/raisetech-live8-sample-app)を使用しています。
- この記事のコードは[こちらのリポジトリ](https://github.com/mkmmr/terraform-practice)をご参照ください。
- 同じ内容で[CloudFormationバージョン](https://github.com/mkmmr/circleci-practice)も作成しています。
- AnsibleとServerspecはCloudFormationバージョンと同じものを使用しているため、手順から割愛しています。詳しくは[CloudFormationバージョン](https://github.com/mkmmr/circleci-practice)をご参照ください。

## 実装手順
コードや実装手順の詳細は[こちらのリポジトリ](https://github.com/mkmmr/terraform-practice)をご参照ください。

1. Terraform 実装手順
    - ローカルPCにTerraformをインストール
    - TerrafromでIAM用SecretAccessKeyの発行
    - Terraformで遭遇したエラー
2. CircleCIへのTerraform実装手順
    - 準備
    - CircleCIにTerraformを実装
    - tfstateファイルをS3バケットで管理する
    - CircleCIで遭遇したエラー

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題Terraformバージョン)

## 成功画面
### ◆ CircleCI成功画面
![CircleCIのWorkflow成功画面](images/aws_lecture13_Terraform_01CircleCIWorkflow.png)
### ◆ Terraform成功画面
![CircleCIでのTerraform成功画面1](images/aws_lecture13_Terraform_02CircleCITerraform1.png)
![CircleCIでのTerraform成功画面2](images/aws_lecture13_Terraform_03CircleCITerraform2.png)
### .tfstateの管理をS3に変更成功
![CircleCIでのTerraform成功画面3](images/aws_lecture13_Terraform_04CircleCITerraform3.png)
![.tfstateファイルがS3に保管されている画面](images/aws_lecture13_Terraform_14tfstateinS3.png)
### ◆ Ansible成功画面
![CircleCIでのAnsible成功画面1](images/aws_lecture13_Terraform_05CircleCIAnsiible1.png)
![CircleCIでのAnsible成功画面2](images/aws_lecture13_Terraform_06CircleCIAnsiible2.png)
### ◆ Serverspec成功画面
![CircleCIでのServerspec成功画面](images/aws_lecture13_Terraform_07CircleCIServerspec.png)

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題Terraformバージョン)

## アプリの正常動作確認
### New Fruit Saveした時
![アプリの正常動作確認：新規追加した時の画面](images/aws_lecture13_Terraform_08AppNewItmSave.png)
### 新規追加後の一覧画面
![アプリの正常動作確認：新規追加後の一覧画面](images/aws_lecture13_Terraform_09App.png)
### Destroyした時
![アプリの正常動作確認：削除した時の画面](images/aws_lecture13_Terraform_10AppItemDestroy.png)

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題Terraformバージョン)

## S3への画像登録確認
![S3への画像登録確認](images/aws_lecture13_Terraform_11S3Status.png)

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題Terraformバージョン)

## 感想
- AssumeRoleを使う場合、一度CircleCIを止めると`$ terraform destroy`が使えないため、手動でリソースを削除しなければならず大変不便であり、誤って他のリソースを消す危険性がある。また、消し忘れるとその度にCIが止まるので作業効率が非常に悪い。RDSの削除にも時間がかかる。Terraformを使用する場合、開発時はAssumeRoleではなく、通常のIAMユーザを使用した方が良い。
- TerraformでIAMを作成しようとすると、AccessKey作成にgpgのペアキーが必要であり、実装が手間。
- 運用方法によってはCloudFormationの方が使い勝手が良いと感じた。

[\[↑ 上へ\]](#awsフルコース-第１３回課題最終課題Terraformバージョン)
