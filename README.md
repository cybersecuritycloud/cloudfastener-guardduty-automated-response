# cloudfastener-guardduty-automated-response

このリポジトリは、AWS GuardDutyの所見を自動で処理し、特定のセキュリティアクションを実施するCloudFormationテンプレートを提供します。

## 概要
このプロジェクトは、AWS Security Hubの所見をEventBridgeでキャプチャし、Step Functionsを使用して以下の2つのアクションを自動実行します。

1. **Security GroupのIngress/Egressルール削除**
   - GuardDutyの所見に基づいて、対象のEC2またはECS Fargateのセキュリティグループの`ingress`および`egress`ルールを削除します。

2. **AWS Network FirewallにIPアドレスを追加**
   - GuardDutyの所見に基づいて、悪意のあるIPアドレスをNetwork Firewallのブロックリストに追加します。

## ディレクトリ構成

| パス | 説明 |
|------|------|
| `guardduty-autoresponse/` | プロジェクトのルートディレクトリ |
| ├── `README.md` | プロジェクトの概要 |
| ├── `securitygroup-removal/` | Security Group ルール削除用のテンプレート |
| │ ├── `guardduty-autoresponse.yaml` | CloudFormationテンプレート |
| │ ├── `deployment-guide.md` | デプロイ手順 |
| ├── `networkfirewall-ipblock/` | Network Firewall にIPを追加するテンプレート |
| │ ├── `aws-networkfirewall-guardduty.template` | CloudFormationテンプレート |
| │ ├── `deployment-guide.md` | デプロイ手順 |
| ├── `LICENSE` | ライセンス情報 |

## デプロイ方法
各ディレクトリにある `deployment-guide.md` を参照してください。
