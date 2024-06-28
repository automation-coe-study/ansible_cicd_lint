# ansible_cicd_lint
CICDパイプラインにてansibleの静的解析(lintチェック)を実行する

このリポジトリは、Ansible の Playbook および Role に対して `ansible-lint` チェックを実行するための再利用可能な GitHub Actions ワークフローを提供します。
CI コンポーネントとして利用することを目的としています。

## 目的
このリポジトリは、Ansible の Playbook および Role に対して `ansible-lint` チェックを実行するための再利用可能な GitHub Actions ワークフローを提供します。
CI コンポーネントとして利用することを目的としています。
原則AAPにて実行するPlaybookの格納されるリポジトリには必ず配置してください。これにより、すべての Playbook と Role が最適なプラクティスとコーディングスタンダードに準拠していることを保証します。

## 使用方法

この再利用可能な `ansible-lint` ワークフローを自分のリポジトリで使用するには、以下の手順に従ってください：

1. **GitHub Actions ワークフローファイルをリポジトリに追加**

   リポジトリの `.github/workflows` ディレクトリに新しいワークフローファイルを作成します（例： `.github/workflows/lint.yml`）。

   ```yaml
   name: Ansible Lint

   on:
     push:
       branches-ignore:
         - main

   jobs:
     lint:
       uses: automation-coe-study/ansible_cicd_lint/.github/workflows/lint.yml@main
   ```

2. リポジトリに変更をプッシュ  
   新しいワークフローファイルをコミットしてプッシュし、ansible-lint チェックをトリガーします。

## 要件
- セルフホステッドランナー: このワークフローは、ansible-lint がインストールされた環境のセルフホステッドランナーで実行することを前提としています。  
- GitHub Actions: リポジトリで GitHub Actions が有効になっていることを確認してください。  

## 環境変数
- `PYTHONUNBUFFERED: 1` ：Python の出力をバッファリングせず、すぐに標準出力に出力します。  
- `ANSIBLE_FORCE_COLOR: 1` ：Ansible の出力を常にカラー表示にします。  

