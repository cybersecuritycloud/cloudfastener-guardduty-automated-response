## アーキテクチャ図


![alt text](aws-automated-responce.png)

## ワークフロー図

```mermaid
flowchart TD
    A["Security Hub イベント<br>(GuardDuty 所見：CRITICAL / HIGH)"]
    B["EventBridge ルール<br>(イベント検出)"]
    C["Step Functions 状態マシン<br>(SecurityGroupRevokerStateMachine)"]
    D{"リソースタイプ判定"}
    E["EC2 用 Lambda<br>(SecurityGroupRevokerFunctionEC2)"]
    F["Fargate 用 Lambda<br>(SecurityGroupRevokerFunctionFargate)"]
    G["セキュリティグループの<br>ルール削除処理"]

    A --> B
    B --> C
    C --> D
    D -- "AwsEc2Instance" --> E
    D -- "AwsEcsTask" --> F
    E --> G
    F --> G

```


## **デプロイ手順（CLI）**

次のコマンドを実行し、CloudFormation スタックをデプロイします。

```sh
aws cloudformation deploy \
  --stack-name securitygroup-rule-removal \
  --template-file securitygroup-removal/securitygroup-removal.yaml \
  --capabilities CAPABILITY_NAMED_IAM
```

## **削除手順（CLI）**
```
aws cloudformation delete-stack --stack-name securitygroup-rule-removal
```