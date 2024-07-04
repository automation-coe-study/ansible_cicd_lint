# ansible_cicd_lint
CICDパイプラインにてansibleの静的解析(lintチェック)を実行する

## 目的
このリポジトリは、Ansible の Playbook および Role に対して 自動化CoE指定の`ansible-lint`および`yamllint` チェックを実行するための再利用可能な GitHub Actions ワークフローを提供する。
原則AAPにて実行するPlaybookの格納されるリポジトリには必ず配置すること。  
これにより、すべての Playbook と Role が最適なプラクティスとコーディングスタンダードに準拠していることを保証する。

## 使用方法
この再利用可能な `lint` ワークフローを自分のリポジトリで使用するには、以下の手順に従う：  

1. **GitHub Actions ワークフローファイルをリポジトリに追加**

   リポジトリの `.github/workflows` ディレクトリに新しいワークフローファイルを作成する（例： `.github/workflows/lint.yml`）。  
   ※onセクションは標準例で、mainブランチ以外のブランチに対するpushおよびmainブランチに対するプルリクエストをトリガーにする。  

   ```yaml
   name: Ansible Lint

   on:
     push:
       branches-ignore:
         - main
     pull_request:
       branches:
         - main

   jobs:
     lint:
       uses: automation-coe-study/ansible_cicd_lint/.github/workflows/lint.yml@main
   ```

2. リポジトリに変更をプッシュ  
   新しいコミットしてプッシュし、lintチェックをトリガーする。  

## 要件
- セルフホステッドランナー: このワークフローは、ansible-lintおよびyamllintがインストールされた環境のセルフホステッドランナーで実行すること。  
- GitHub Actions: リポジトリで GitHub Actions が有効になっていること。  

## 環境変数
- `PYTHONUNBUFFERED: 1` ：Python の出力をバッファリングせず、すぐに標準出力に出力します。  
- `ANSIBLE_FORCE_COLOR: 1` ：Ansible の出力を常にカラー表示にします。  

