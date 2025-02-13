## アーキテクチャ図


![alt text](aws-automated-responce.png)

## ワークフロー図

```mermaid
flowchart TD
    A["Security Hub イベント\n(GuardDuty 所見：CRITICAL / HIGH)"]
    B["EventBridge ルール\n(イベント検出)"]
    C["Step Functions 状態マシン\n(SecurityGroupRevokerStateMachine)"]
    D{"リソースタイプ判定"}
    E["EC2 用 Lambda\n(SecurityGroupRevokerFunctionEC2)"]
    F["Fargate 用 Lambda\n(SecurityGroupRevokerFunctionFargate)"]
    G["セキュリティグループの\nルール削除処理"]
    H["SNS 通知\n(成功/失敗)"]

    A --> B
    B --> C
    C --> D
    D -- "AwsEc2Instance" --> E
    D -- "AwsEcsTask" --> F
    E --> G
    F --> G
    G --> H

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