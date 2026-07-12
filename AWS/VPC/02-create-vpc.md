# VPCの作成とネットワーク構成

## 概要

VPCを作成し、パブリックサブネットとプライベートサブネットを持つ基本的なネットワーク環境を構築した。

## なぜ必要か

AWSでは、VPC（Virtual Private Cloud）を利用して独立した仮想ネットワークを構築できる。

パブリックサブネットとプライベートサブネットを分けることで、インターネットへ公開するリソースと公開しないリソースを分離し、セキュリティを向上させることができる。

## 構成

| リソース | CIDR |
| -------- | ----------- |
| VPC | `10.0.0.0/16` |
| Public Subnet | `10.0.10.0/24` |
| Private Subnet | `10.0.20.0/24` |

### ネットワーク構成

```text
Internet
    │
Internet Gateway
    │
┌────────────────────────────┐
│ VPC (10.0.0.0/16)                                      │
│                                                        │
│ Public Subnet                                          │
│ 10.0.10.0/24                                           │
│   └─ EC2(Web) ※今後構築予定                         │
│                                                        │
│ Private Subnet                                         │
│ 10.0.20.0/24                                           │
│   └─ DB ※今後構築予定                               │
└────────────────────────────┘
```

## 手順

1. VPCを作成する
2. Public Subnetを作成する
3. Private Subnetを作成する
4. Internet Gatewayを作成する
5. Internet GatewayをVPCへアタッチする
6. Public SubnetのルートテーブルにInternet Gatewayへのルートを追加する

## 学んだこと

- VPCはAWS上に独立したネットワークを構築するサービスである。
- Public SubnetはInternet Gatewayとルートテーブルを設定することでインターネットと通信できる。
- Private SubnetはInternet Gatewayへ接続しないため、インターネットから直接アクセスできない。
- WebサーバはPublic Subnet、データベースはPrivate Subnetに配置する構成が一般的である。

## 詰まったこと

- 

## 今後試したいこと

- Public SubnetにEC2（Webサーバ）を構築する。
- Private SubnetにRDSまたはEC2でデータベースを構築する。
- NAT Gatewayを利用してPrivate Subnetからインターネットへ接続できるようにする。

## 参考

- 