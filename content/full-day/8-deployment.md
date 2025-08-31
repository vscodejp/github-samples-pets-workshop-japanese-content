# プロジェクトをクラウドにデプロイする

| [← GitHub flow][walkthrough-previous] | [Next: Pets workshop selection →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

CI/CD の CD 部分は継続的デリバリーまたは継続的デプロイメントです。要するに、構築している製品を取り、それを必要とする人々がアクセスできる場所に配置することです。これを行う方法は数多くあり、プロセスはかなり複雑になることがあります。私たちはアプリケーションを取り、Azure にデプロイすることに焦点を当てます。

> [!NOTE]
> このワークショップでスムーズに動作するように、アプリケーション構造でいくつかのショートカットを取りました。

## シナリオ

プロトタイプが構築されたことで、シェルターは外部ユーザーからのフィードバックの収集を始める準備ができています。プロジェクトをインターネットにデプロイし、main にマージされた更新ができるだけ迅速に利用できるようにしたいと考えています。

## main に戻る

プロセスを合理化するために、**main** ブランチで直接作業します。**main** ブランチに戻り、以前にプッシュした更新を取得しましょう。

1. codespace に戻るか、リポジトリに移動して **Code** > **Codespaces** と codespace の名前を選択して再度開きます。
2. <kbd>Ctl</kbd>+<kbd>Shift</kbd>+<kbd>`</kbd> を選択して新しいターミナルウィンドウを開きます。
3. 次のコマンドを実行して main ブランチをチェックアウトし、リポジトリから更新を取得します：

    ```sh
    git checkout main
    git pull
    ```

## アイデンティティ管理

外部サービスと相互作用する際は、もちろん任意のアクションを実行するための認証情報が必要です。これは、GitHubでのワークフローなど、あらゆる形式の自動化されたタスクを作成する場合にも当てはまります。アクセストークン、共有パスワード、[Open ID Connect (OIDC)][oidc-docs]など、アイデンティティを管理する方法はいくつかあり、後者が最新で推奨されるメカニズムです。OIDCの利点は、短時間のトークンを使用し、実行可能な操作に対してきめ細かい制御を提供することです。

認証情報の作成と設定は、通常管理者が実行するタスクです。ただし、これを管理してくれるツールがあり、その一つを活用します！

## AzureにデプロイするためにAzureに尋ねる

以前、[GitHub Copilot chat の拡張機能][extensions-copilot-chat]について話しました。これにより、外部サービスと相互作用できます。これらの外部サービスは、DevOps フロー、データベース、その他のリソースに関する情報へのアクセスを提供できます。そのような拡張機能の一つが[Azure拡張機能][azure-copilot-extension]で、名前が示すようにAzureと相互作用できます。この拡張機能を使用して、アプリケーションのデプロイ方法についてアドバイスを得たり、サービスのステータスを確認したり、その他の操作を実行したりできます。この拡張機能を使用してアプリケーションのデプロイ方法を尋ねます。

他のタスクで行ったように、体験の一部としてGitHub Copilotと最適に相互作用する方法を学ぶことを目的としているため、Azureと話すときに使用する特定のプロンプトはありません。デプロイメントの要件は以下の通りです：

- プロジェクトをクラウドにデプロイする
- デプロイプロセスを管理するためにGitHub actionを使用する

1. GitHub Copilot Chatを開きます。
2. `@azure`と入力し、<kbd>Tab</kbd>を選択してAzure拡張機能を有効化し、実行したいタスクの実行方法を拡張機能に尋ねます（上記の要件を参照）。

> [!NOTE]
> これが拡張機能を初めて使用する場合、Azureにサインインするよう求められます。表示されるプロンプトに従ってください。

3. `azd`コマンドをハイライトした応答を受け取るはずです。これは、クラウド環境の初期化とワークフローの作成の両方に使用できます。

## Copilotからの応答の概要

GitHub Copilotからの応答には、おそらく以下のコマンドを使用する指示が含まれているでしょう：

- `azd init --from-code` [bicep][bicep-docs]を使用してAzure設定ファイルを作成する。
- `azd auth login` Azureに認証する。
- `azd pipeline config` GitHub Workflowを作成する。

[azd][azd-docs]は、Azureへのデプロイプロセスを合理化するのに役立つコマンドラインユーティリティです。これを使用して以下を行います：

- bicepファイルを生成する。
- ワークフローファイルを作成する。
- ワークフロー用のOIDCを作成・設定する。

**azd**やAzureについて興味がある場合は、GitHub Copilotを使用して拡張機能に質問することができます！

## azdをインストールする

**azd**をインストールすることから始めましょう。

1. ターミナルで以下のコマンドを実行して**azd**をインストールします：

    ```sh
    curl -fsSL https://aka.ms/install-azd.sh | bash
    ```

## bicepファイルを作成・設定する

BicepはAzureリソースを定義するためのドメイン固有言語（DSL）です。動的で、環境を正確に必要な通りに設定することを確実にできます。**azd**にbicepファイルを作成させることから始め、その後クライアントがサーバーに接続するために利用できる環境変数を確保するための更新を行います。

1. `init`コマンドを実行してbicepファイルを作成します。

    ```sh
    azd init --from-code
    ```

2. プロンプトに従い、ツールが提供するデフォルトを受け入れ、名前空間（Azureのリソースグループと様々なリソースの名前付けに使用される）をユニークな名前にします。
3. **infra**/**resources.bicep**にあるbicepファイルを開きます。
4. 次のように記述されているセクション（130行目付近）を見つけます：

    ```bicep
    {
      name: 'PORT'
      value: '4321'
    }
    ```

5. 閉じる`}`の下に新しい行を作成し、新しく作成されたFlaskサーバーのURLを含む環境変数を作成するために以下を追加します：

    ```bicep
    {
      name: 'API_SERVER_URL'
      value: 'https://${server.outputs.fqdn}'
    }
    ```

> [!NOTE]
> 構文はJSONに似ていますが、JSONではありません。そのため、値を区切るためにコンマを追加したい衝動を抑えてください！

## ワークフローを作成する

`azd`は、プロジェクトをデプロイするためのワークフロー（時にはパイプラインと呼ばれることもあります）を作成・設定できます。特に以下を行います：

- デプロイに使用するOIDC認証情報を作成する。
- **workflows**フォルダにYMLファイルを定義する。

`azd`に作業を行わせましょう！

1. ターミナルウィンドウに戻り、以下のコマンドを実行して`azd`で認証します：

    ```sh
    azd auth login
    ```

2. プロンプトに従い、以前に指定した認証情報を使用してAzureに認証します。
3. 以下のコマンドを実行してパイプラインを作成します：

    ```sh
    azd pipeline config
    ```

4. プロンプトに従い、デフォルトを受け入れます。プロンプトの一つで、今すぐデプロイを実行するかどうか尋ねられます - yesと答えてください！
5. アプリケーションがクラウドに向かいます！

## デプロイを追跡してアプリケーションをテストする

`azd pipeline config`コマンドは、**.github/workflows/azure-dev.yml**に新しいワークフローファイルを作成します。ワークフローを探索し、実行中のアクション（これには数分かかります）を追跡し、アプリケーションをテストしましょう！

1. **.github/workflows/azure-dev.yml**でワークフローを開きます。
2. `on`セクションに注意してください。これには`workflow_dispatch`（手動デプロイをサポートするため）と`push`（コードが**main**ブランチにプッシュされたときに自動的にデプロイするため）のフラグが含まれています。
3. コアステップに注意してください。これらはコードをチェックアウトし、Azureに認証し、インフラストラクチャを作成または更新し、アプリケーションをデプロイします。
4. ワークフローが何をしているかについて質問がある場合は、GitHub Copilotに尋ねてください！
5. GitHubのリポジトリに移動します。
6. **Actions**タブを開き、**.github/workflows/azure-dev.yml**という名前のアクションを開きます。アクションが実行されているのが見えるはずです（**workflow runs**セクションの下でアイコンが黄色になっています）。
7. 実行中のワークフロー（**Configure Azure Developer Pipeline**という名前になっているはずです）を選択します。
8. **build**ステップを選択します。
9. デプロイプロセスを追跡します。これには約5-10分かかります（水分補給のよい時間です！）。
10. プロセスが完了したら、**Deploy Application**セクションを展開します。クライアントとサーバーの両方がデプロイされたことを示すログが表示されるはずです：

    ```
    Deploying service client
    Deploying service client (Building Docker image)
    Deploying service client (Tagging container image)
    Deploying service client (Tagging container image)
    Deploying service client (Logging into container registry)
    Deploying service client (Pushing container image)
    Deploying service client (Updating container app revision)
    Deploying service client (Fetching endpoints for container app service)
    (✓) Done: Deploying service client
    - Endpoint: https://client.delightfulfield-8f7ef050.westus.azurecontainerapps.io/

    Deploying service server
    Acquiring pack cli
    Deploying service server (Building Docker image from source)
    Deploying service server (Tagging container image)
    Deploying service server (Tagging container image)
    Deploying service server (Logging into container registry)
    Deploying service server (Pushing container image)
    Deploying service server (Updating container app revision)
    Deploying service server (Fetching endpoints for container app service)
    (✓) Done: Deploying service server
    - Endpoint: https://server.delightfulfield-8f7ef050.westus.azurecontainerapps.io/
    ```

11. クライアント用のエンドポイントを選択します。アプリケーションが表示されるはずです！

これでプロジェクトをデプロイしました！

## まとめ

完全なCI/CDプロセスを作成・設定しました。セキュリティチェック、テスト、そして今度はデプロイメントを実装しました。前述したように、エンタープライズCI/CDプロセスはかなり複雑になることがありますが、その核心では、このワークショップで探索したスキルを使用しています。

## まとめとチャレンジ

おめでとうございます！完全なDevOpsプロセスを経験しました。必要な作業を文書化するIssueの作成から始まり、すべてが自動的に実行される場所にあることを確認しました。アプリケーションの更新を実行し、すべてをリポジトリにプッシュし、マージしました！

ここからさらに探索を続けたい場合は、いくつかのタスクを追求できます：

- ウェブサイトにさらに機能を追加しましょう！養子縁組フォームの追加や画像を保存する機能など、できることはたくさんあります。
- データベースをPostgresやSQL Serverなどのより強力なものに移行する。

今日学んだスキルを引き続き構築するために、必要に応じてワークショップリーダーと協力して質問し、ガイダンスを得てください！

## リソース

- [OpenID Connect を使ったセキュリティ強化について][oidc-docs]
- [GitHub Actions を使ったデプロイ][actions-deploy]
- [Azure Developer CLI とは？][azd-docs]

| [← GitHub flow][walkthrough-previous] | [Next: Pets workshop selection →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[actions-deploy]: https://docs.github.com/en/actions/use-cases-and-examples/deploying/deploying-with-github-actions
[azd-docs]: https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/overview?tabs=linux
[azure-copilot-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot
[bicep-docs]: https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep
[extensions-copilot-chat]: ./5-context.md
[oidc-docs]: https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect
[walkthrough-previous]: 7-github-flow.md
[walkthrough-next]: ../README.md