# terraform_sample

### 環境

```
brew install terraform
gem install terraforming
```

### 命名規約

https://blog.kenjiskywalker.org/2016/07/06/terraform-newbie/

>resourceはあくまでTerraform内での管理するためだけの命名


### コマンドメモ

.awsの下にprofileを作って、それを指定してinitする

```
#初期化
AWS_PROFILE=<aws profile name> terraform init

#作るものは　VPCとサブネット、インターネットゲートウェイ、ルートテーブル、サブネットとルートテーブル紐付け、セキュリティグループなど

```

### 現在のAWSからtfファイルを作成する例

#### VPC作成の例


```
空のnetwork.tfを作成

```:network.tf
resource "aws_vpc" "terraform-vpc" {

}
```

#VPC IDを指定
terraform import aws_vpc.terraform-vpc vpc-xxxxxxxxxxxxx

terraform state show aws_vpc.terraform-vpc

の内容をnetwork.tfにうつす。arn, id, owner_idなどエラーになる部分を消す。



terraform planで差異がないことを確認。

```
AWS_PROFILE=profile_name terraform plan
```

他のリソースの場合

```
#EC2のimport
terraform import aws_instance.<任意の名前> <インスタンスID>
s3のimport
terraform import aws_s3_bucket.<任意の名前> <バケット名>
ALBのimport
terraform import aws_alb.<任意の名前> <ARN>
```

