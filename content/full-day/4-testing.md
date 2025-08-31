# 継続的インテグレーションとテスト

| [← Cloud-based development with GitHub Codespaces][walkthrough-previous] | [Next: Helping GitHub Copilot understand context →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

CI/CD という略語を聞いたことがあるでしょう。これは継続的インテグレーションと継続的デリバリー（または継続的デプロイメント）を表しています。CI は新しいコードを既存のコードベースに統合することを中心とし、通常はテストの実行とビルドの実行を含みます。CD は次の論理的なステップに焦点を当て、検証されたコードを取り、クラウドやその他の宛先にプッシュするために必要な出力を生成します。これはおそらく DevOps の最も注目されるコンポーネントです。

CI/CD は迅速な開発、コラボレーション、継続的改善の文化を促進し、組織がソフトウェアの更新と新機能をより確実かつ迅速に提供できるようにします。一貫性を確保し、開発者が手動プロセスを実行するのではなく、コードの記述に集中できるようにします。

[GitHub Actions][github-actions] は、CI/CD プロセスを構築できる自動化プラットフォームです。画像のリサイズや機械学習モデルの検証など、他のタスクの自動化にも使用できます。

## シナリオ

プロジェクトの Python サーバー用の単体テストのセットが存在します。誰かが[プルリクエスト][about-prs]（PR）を作成したときに、これらのテストが実行されることを確認したいと考えています。この要件を満たすには、プロジェクトのワークフローを定義し、main へのプルリクエストに対する[トリガー][workflow-triggers]があることを確認する必要があります。幸い、[GitHub Copilot][copilot] が必要な YML ファイルの作成を支援できます！

## テストを探索する

プロジェクトで定義されているテストを確認してみましょう。

> [!NOTE]
> このプロジェクトでは定義されているテストは少数です。多くのプロジェクトでは、信頼性を確保するために数百または数千のテストが存在します。

1. Codespaceに戻るか、リポジトリに移動し**Code** > **Codespaces**とCodespaceの名前を選択して再度開きます。
2. **Explorer**で、**server**に移動し**test_app.py**を開きます。
3. GitHub Copilot Chatを開き、ファイルの説明を求めます。

> [!NOTE]
> テストの理解を深めるために、以下のGitHub Copilotのヒントを使用することを検討してください：
>
> - `/explain`は説明を素早く求めるための[スラッシュコマンド][copilot-slash-commands]です
> - ファイルの特定のセクションをハイライトして、疑問がある箇所に焦点を当てます

## ワークフローを理解する

PRが作成されるたびにテストが実行されるようにするため、プロジェクト用のワークフローを定義します。ワークフローは、セキュリティ脆弱性のチェック、プロジェクトのデプロイ、または（今回の場合は）ユニットテストの実行など、多数のタスクを実行できます。これらはCI/CDの中核となります。

YMLファイルの作成は少し難しい場合があります。幸い、GitHub Copilotがプロセスを効率化してくれます！Copilotと連携してファイルを作成する前に、ワークフローの主要セクションを探索してみましょう：

- `name`: ワークフローの名前を提供し、ログに表示されます。
- `on`: ワークフローの実行をトリガーする条件を定義します。一般的なトリガーには、`pull_request`（PRが作成された時）、`merge`（コードがブランチにマージされた時）、`workflow_dispatch`（手動実行）があります。
- `jobs`: このワークフローの一連のジョブを定義します。各ジョブは作業単位と見なされ、名前があります。
    - **name**: ジョブの名前とコンテナ。
    - `runs-on`: ジョブの操作が実行される場所。
    - `steps`: 実行される操作。

## ワークフローファイルを作成する

ワークフローの構造の概要を理解したので、Copilotにファイルを生成してもらいましょう！

1. **.github**の下に**workflows**という名前の新しいフォルダを作成します。
2. **server-test.yml**という名前の新しいファイルを作成し、ファイルが開いていることを確認します。
3. **GitHub Actions**拡張機能のインストールを求められた場合は、**Install**を選択します。
4. GitHub Copilot Chatを開きます。
5. Chatダイアログボックスで`#`を使用し、**test_app.py**と入力を始めてテストファイル**test_app.py**をコンテキストに追加し、ハイライトされたら<kbd>enter</kbd>を押します。
6. CopilotにGitHub Actionワークフローを作成してテストを実行するよう促します。自然言語を使用して作成したいワークフロー（test_app.pyで定義されたテストを実行する）を説明し、マージ時（新しいコードがプッシュされた時）、PRが作成された時、およびオンデマンドで実行したいことを説明します。

  > [!IMPORTANT]
  > この演習の一部は GitHub Copilotとの対話に慣れることであるため、規定のプロンプトは提供されていません。

7. 提案されたコードにカーソルを合わせて**Insert at cursor**ボタンを選択することで、生成されたコードを新しいファイルに追加します。生成されたコードは以下のようなものになるはずです：

```yml
name: Server Tests

on:
  push:
    branches: [ main ]
    paths:
      - 'server/**'
  pull_request:
    branches: [ main ]
    paths:
      - 'server/**'

jobs:
  server-test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        if [ -f server/requirements.txt ]; then pip install -r server/requirements.txt; fi
        pip install pytest

    - name: Run tests
      working-directory: ./server
      run: |
        python -m pytest test_app.py -v
```

> [!IMPORTANT]
> 注意：生成されるファイルは上記の例と異なる場合があります。GitHub Copilotは生成AIを使用するため、結果は決定論的ではなく確率的になります。

> [!TIP]
> 作成したワークフローについてさらに詳しく知りたい場合は、GitHub Copilotに質問してみてください！

## ワークフローをリポジトリにプッシュする

ワークフローが作成されたので、リポジトリにプッシュしましょう。通常は、新しいコード（これもその一つです）に対してPRを作成しますが、プロセスを効率化するため、[後の演習][github-flow-exercise]でプルリクエストと[GitHub flow][github-flow]を探索する予定なので、今回は直接mainにプッシュします。まず[以前に作成したissue][issues-exercise]の番号を取得し、新しいコードのコミットを作成し、mainにプッシュします。

> [!NOTE]
> すべてのコマンドはCodespaceのターミナルウィンドウを使用して入力します。

1. Codespaceで開いているターミナルウィンドウを使用するか、（必要に応じて）<kbd>Ctl</kbd> + <kbd>`</kbd>を押して開きます。
1. ターミナルウィンドウで以下のコマンドを入力して、リポジトリのすべてのissueを一覧表示します：

    ```bash
    gh issue list
    ```

1. **Implement testing**というタイトルのissue番号をメモします。
1. ターミナルウィンドウで以下のコマンドを入力してすべてのファイルをステージします：

    ```bash
    git add .
    ```

1. ターミナルウィンドウで以下のコマンドを入力してすべての変更をメッセージと共にコミットします。**<ISSUE_NUMBER>**を**Implement testing** issueの番号に置き換えてください：

    ```bash
    git commit -m "Resolves #<ISSUE_NUMBER>"
    ```

1. ターミナルウィンドウで以下のコマンドを入力してすべての変更をリポジトリにプッシュします：

    ```bash
    git push
    ```

おめでとうございます！継続的インテグレーション（CI）の中核コンポーネントであるテストを実装しました！

## ワークフローの動作を確認する

ワークフロー定義をリポジトリにプッシュすることは `main` へのプッシュとしてカウントされ、ワークフローがトリガーされることを意味します。リポジトリの **Actions** タブに移動することで、ワークフローの動作を確認できます。

1. リポジトリに戻ります。
2. **Actions** タブを選択します。
3. 左側で **Server test** を選択します。
4. 使用したコミットメッセージと一致する **Resolves #<ISSUE_NUMBER>** のメッセージが付いた右側のワークフロー実行を選択します。
5. ジョブ名を選択してワークフロー実行を探索します

これでワークフローを見て、実行の詳細を探索しました！

## まとめと次のステップ

おめでとうございます！成功する DevOps にとって重要な継続的インテグレーションの標準的な部分である自動テストを実装しました。これらのプロセスを自動化することで一貫性が確保され、開発者と管理者に必要な作業負荷が軽減されます。コードベースの新しいコードでテストを実行するワークフローを作成しました。[GitHub Copilot チャットでのコンテキスト][walkthrough-next]を探索しましょう。

### リソース
- [GitHub Actions][github-actions]
- [GitHub Actions Marketplace][actions-marketplace]
- [継続的インテグレーションについて][about-ci]
- [GitHub Skills: Actions でテスト][skills-test-actions]

| [← Cloud-based development with GitHub Codespaces][walkthrough-previous] | [Next: Helping GitHub Copilot understand context →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[about-ci]: https://docs.github.com/en/actions/automating-builds-and-tests/about-continuous-integration
[about-prs]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests
[actions-marketplace]: https://github.com/marketplace?type=actions
[workflow-triggers]: https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows
[copilot]: https://gh.io/copilot
[copilot-slash-commands]: https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/github-copilot-chat-cheat-sheet
[github-actions]: https://github.com/features/actions
[github-flow]: https://docs.github.com/en/get-started/quickstart/github-flow
[github-flow-exercise]: ./7-github-flow.md
[issues-exercise]: ./2-issues.md
[skills-test-actions]: https://github.com/skills/test-with-actions
[walkthrough-previous]: 3-codespaces.md
[walkthrough-next]: 5-context.md
