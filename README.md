# argocd-install
ArgoCDインストール用リポジトリ

## はじめに
GKEを頻繁に削除する事を想定しているため、ArgoCDインストールパイプラインを構築する  
このパイプラインの実行は、GKE構築後の初回のみ成功する  

## JOBの手動実行
以下のコマンドでpushを行わずにmasterブランチの状態でJOBの実行ができる
```bash
curl -vv \
  -H "Authorization: token $PERSONAL_ACCESS_TOKEN" \
  -H "Accept: application/vnd.github.everest-preview+json" \
  "https://api.github.com/repos/sabure500/argocd-install/dispatches" \
  -d '{"event_type": "argocd-install", "client_payload": {"target_brunch": "master"}}'
```

## 設定が必要なSecrets
* PROJECT_ID : GCPのプロジェクト
* SA_EMAIL : パイプライン実行で利用するServiceAccountのID
* SA_KEY : 上記サービスアカウントのKey
* PERSONAL_ACCESS_TOKEN : ArgoCDの初期設定が入ったリポジトリへの権限を持つパーソナルアクセストークン
* ARGOCD_PASSWORD : ArgoCDの管理者ユーザーのパスワードに設定する値

## 参考
* [GCP用GithubActionsリポジトリ](https://github.com/GoogleCloudPlatform/github-actions/blob/master/setup-gcloud/README.md)
* [Argocd公式リポジトリ](https://github.com/argoproj/argo-cd)
* [actions/checkoutの使い方](https://github.com/actions/checkout)