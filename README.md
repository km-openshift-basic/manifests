# OpenShift Workshop Manifests

OpenShift コンテナアプリケーション ハンズオンワークショップ用の Kubernetes/OpenShift マニフェストです。

## 構成

```
manifests/
├── base/                          # 共通リソース定義
│   ├── kustomization.yaml
│   ├── app-deployment.yaml        # Quarkus アプリ
│   ├── app-service.yaml           # アプリ Service
│   ├── app-route.yaml             # アプリ Route (外部公開)
│   ├── app-configmap.yaml         # アプリ設定
│   ├── db-deployment.yaml         # PostgreSQL
│   ├── db-service.yaml            # DB Service (ClusterIP)
│   ├── db-secret.yaml             # DB 認証情報
│   └── db-pvc.yaml                # DB データ永続化
└── overlays/
    ├── dev/                       # dev 環境 (replicas=1)
    └── prod/                      # prod 環境 (replicas=2, image tag=promoted)
```

## デプロイ方法

### 事前準備: イメージ名の設定

`base/kustomization.yaml` および各 overlay の `kustomization.yaml` 内の `images` セクションで、
`NAMESPACE` をご自身のプロジェクト名に変更してください。

### dev 環境

```bash
oc apply -k overlays/dev/
```

### prod 環境

```bash
oc apply -k overlays/prod/
```

## 前提条件

- アプリのコンテナイメージが OpenShift 内部レジストリに push 済みであること
- `kustomization.yaml` の `images` セクションで正しいプロジェクト名を設定していること
