# GitHub を使ったモダンな DevOps

| [← Pets workshop selection][walkthrough-previous] | [Next: Workshop setup →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[DevOps][devops] は **development（開発）** と **operations（運用）** を組み合わせた[複合語][portmanteau]です。その核心には、開発のプラクティスを運用により近づけ、運用のプラクティスを開発により近づけたいという願いがあります。これにより、チーム間のより良いコミュニケーションとコラボレーションが促進され、障壁が取り除かれ、私たちが出荷するソフトウェアで顧客に喜んでもらうための投資を全員が行うことができます。

このワークショップは、GitHub で最も一般的な DevOps タスクのいくつかをガイドするために構築されています。探索内容：

- [GitHub Issues][github-issues] を使ったプロジェクト管理
- [GitHub Codespaces][github-codespaces] を使った開発環境の作成
- AI ペアプログラマーとしての [GitHub Copilot][github-copilot] の使用
- [GitHub Advanced Security][github-security] を使った開発パイプラインのセキュリティ保護
- [GitHub Actions][github-actions] を使ったタスクと CI/CD の自動化

## 前提条件

ワークショップで使用するアプリケーションは、主に Python（Flask と SQLAlchemy）と Astro（Tailwind と Svelte を使用）で構築されています。これらのフレームワークと言語の経験があると役立ちますが、Copilot を使ってプロジェクトを理解し、コードを生成する手助けを受けることになります。そのため、プログラミングに慣れていれば、演習を完了することができます！

## 必要なリソース

このワークショップを完了するには、以下が必要です：

- [GitHub アカウント][github-signup]
- [GitHub Copilot][github-copilot] へのアクセス

## はじめに

始める準備はできましたか？さあ行きましょう！ワークショップのシナリオでは、ペット収養センターでボランティアとして時間を提供する開発者として想像します。開発環境の作成、コードの作成、セキュリティの有効化、プロセスの自動化のプロセスを通して作業します。

0. ワークショップ用に[環境をセットアップ][walkthrough-next]する
1. 新しいコードが安全であることを確認するために[コードスキャンを有効化][code-scanning]する
2. 機能リクエストを文書化するために[Issue を作成][issues]する
3. コードの記述を開始するために[Codespace を作成][codespaces]する
4. 継続的インテグレーションを補完するために[テストを実装][testing]する
5. 質の高いコード提案を生成するために[Copilot にコンテキストを提供][context]する
6. GitHub Copilot で[アプリに機能を追加][code]する
7. [GitHub flow を使用][github-flow]して変更をコードベースに組み込む
8. ユーザーがアプリケーションを利用できるように[アプリケーションを Azure にデプロイ][deployment]する

## さらに深く学ぶためのリソースをチェック
[**GitHub-Copilot-Resources.md**][GitHub-Copilot-Resources] のリソースをチェックしてください。

このリソースリストは、GitHub Copilot について詳しく学び、効果的に使用する方法、将来の予定などを学ぶのに役立つように注意深くキュレーションされています。GitHub Developer Relations チームや GitHub の他のメンバーからの最新ビデオを含む YouTube プレイリストもあります。

| [← Pets workshop selection][walkthrough-previous] | [Next: Workshop setup →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[code]: ./6-code.md
[code-scanning]: ./1-code-scanning.md
[codespaces]: ./3-codespaces.md
[context]: ./5-context.md
[deployment]: ./8-deployment.md
[devops]: https://en.wikipedia.org/wiki/DevOps
[github-actions]: https://github.com/features/actions
[github-codespaces]: https://github.com/features/codespaces
[github-copilot]: https://github.com/features/copilot
[github-flow]: ./7-github-flow.md
[github-issues]: https://github.com/features/issues
[github-security]: https://github.com/features/security
[github-signup]: https://github.com/join
[issues]: ./2-issues.md
[portmanteau]: https://www.merriam-webster.com/dictionary/portmanteau
[testing]: ./4-testing.md
[walkthrough-next]: ./0-setup.md
[walkthrough-previous]: ../README.md
[GitHub-Copilot-Resources]: ../GitHub-Copilot-Resources.md
