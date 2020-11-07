# argocd-install

ArgoCD インストール用リポジトリ

## はじめに

GKE を頻繁に削除する事を想定しているため、ArgoCD インストールパイプラインを構築する  
このパイプラインの実行は、GKE 構築後の初回のみ成功する

## JOB の手動実行

以下のコマンドで push を行わずに master ブランチの状態で JOB の実行ができる

```bash
curl -vv \
  -H "Authorization: token $PERSONAL_ACCESS_TOKEN" \
  -H "Accept: application/vnd.github.everest-preview+json" \
  "https://api.github.com/repos/sabure500/argocd-install/dispatches" \
  -d '{"event_type": "argocd-install", "client_payload": {"target_brunch": "master"}}'
```

## 設定が必要な Secrets

- PROJECT_ID : GCP のプロジェクト
- SA_EMAIL : パイプライン実行で利用する ServiceAccount の ID
- SA_KEY : 上記サービスアカウントの Key
- PERSONAL_ACCESS_TOKEN : ArgoCD の初期設定が入ったリポジトリへの権限を持つパーソナルアクセストークン
- ARGOCD_PASSWORD : ArgoCD の管理者ユーザーのパスワードに設定する値

## 参考

- [GCP 用 GithubActions リポジトリ](https://github.com/GoogleCloudPlatform/github-actions/blob/master/setup-gcloud/README.md)
- [Argocd 公式リポジトリ](https://github.com/argoproj/argo-cd)
- [actions/checkout の使い方](https://github.com/actions/checkout)
