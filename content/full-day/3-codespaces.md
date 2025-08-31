# GitHub Codespaces を使ったクラウドベース開発

| [← Project management with GitHub Issues][walkthrough-previous] | [Next: Continuous integration and testing →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

組織が直面する最大の課題の一つは、新しい開発者をプロジェクトにオンボーディングすることです。インストールするライブラリ、設定するサービス、バージョンの問題、分かりにくいエラーメッセージがあります...開発者が最初のコード行を書けるようになる前に、すべてを動作させるのに文字通り数日かかることがあります。[GitHub Codespaces][codespaces] は、このプロセス全体を合理化するために構築されています。開発者が世界中のほぼどこからでも数回のクリックでアクセスできる開発用コンテナを設定できます。コンテナはクラウドで実行され、すべてが既にセットアップされ、すぐに使用できます。開発者は数日ではなく数秒でコードを書き始めることができます。

GitHub Codespaces では、クラウドベースのコンテナとブラウザウィンドウの Visual Studio Code を使用して開発できます。つまり、ローカルインストールは不要です。タブレットとキーボードで開発できます！[Visual Studio Code][vscode-codespaces] のローカルインスタンスに接続することもできます。

プロジェクト用の codespace を作成・設定する方法を探索し、ブラウザで開発する方法を見てみましょう。

## デフォルトコンテナの使用

GitHub はすべてのリポジトリに[デフォルトコンテナ][github-universal-container]を提供しています。このコンテナは Linux イメージに基づいており、Node.js、Python、PHP、.NET など多くの人気のあるランタイムが含まれています。多くのシナリオでは、このデフォルトコンテナが必要なすべてかもしれません。また、後でこの演習で見るように、リポジトリ用にカスタムコンテナを設定する機能もあります。今のところ、デフォルトコンテナの使用方法を探索しましょう。

1. まだ開いていない場合は、ブラウザでリポジトリを開きます。
1. リポジトリの **Code** タブから（新しいブラウザタブを開くことを提案）、緑色の **<> Code** ドロップダウンボタンにアクセスし、**Codespaces** タブから **Create codespace on main** をクリックします。
1. Codespace の読み込みを待ちます。デフォルトイメージを使用しているため、30秒未満で完了するはずです。

## カスタムコンテナの定義

本当に素晴らしいのは、[デフォルト dev container][github-universal-container-definition]に **.NET 7**、**node**、**python**、**mvn** などが含まれていることです。しかし、他のツールが必要な場合はどうでしょうか？または今回の場合、各開発者に **[GitHub Copilot Extension][copilot-extension]** をインストールしてもらいたくないので、最初からすべてを事前設定したいのです！

独自の dev container を作成しましょう！[dev container は設定][dev-containers-docs]されます。Codespaces がコンテナを作成・設定するために使用する Docker ファイルを作成し、`devcontainer.json` ファイルでカスタマイゼーションを提供します。`devcontainer.json` で提供されるカスタマイゼーションには、開くポート、実行するコマンド、Visual Studio Code にインストールする拡張機能（デスクトップまたはブラウザでローカルに実行）が含まれます。この設定はリポジトリの一部になります。貢献したいすべての開発者は、提供した設定に基づいてコンテナの新しいインスタンスを作成できます。

1. コマンドパレット（<kbd>F1</kbd> またはクリック ☰ → View → Command Palette）にアクセスし、**dev container** と入力し始めます。
2. **Codespaces: Add Development Container Configuration Files...** を選択します。
3. **Create a new configuration...** を選択します。
4. 下にスクロールして **Node.js & TypeScript** を選択します。
5. **22-bookworm (default)** を選択します。
6. コンテナに追加する以下の機能を選択します：
    - **Azure CLI**
    - **GitHub CLI**
    - **Python**

> [!NOTE]
> 機能の名前を入力してリストをフィルタできます。

7. **OK** を選択して機能を追加します。
8. **Keep defaults** を選択してデフォルト設定を使用します。
9. **File './.github/dependabot.yml' already exists, overwrite?** のプロンプトが表示された場合は、**Skip** を選択します。

> [!IMPORTANT]
> 新しいコンテナ定義ファイルは **.devcontainer** フォルダに作成されます。**Rebuild Now** は選択**しないでください**。すぐに実行します。

これで codespace で使用されるコンテナを定義しました。これにはコードに必要なサービスとツールが含まれています。

## 拡張機能をカスタマイズする

開発環境の作成は、サービスにのみ焦点を当てているわけではありません。開発者は[統合開発環境（IDE）][IDE]のための様々な拡張機能とプラグインに依存しています。一貫性を確保するために、自動的にインストールする拡張機能のセットを定義したい場合があります。GitHub Codespaces と Visual Studio Code のローカルインスタンスまたはブラウザベースのバージョンのいずれかを使用する場合、**devcontainer.json** ファイルに[拡張機能][vscode-extensions]のリストを追加できます。

コンテナを再構築する前に、拡張機能のリストに **GitHub.copilot** を追加しましょう。

1. codespace にとどまり、**.devcontainer** フォルダ内の **devcontainer.json** を開きます。
2. 次のセクションを見つけます：

    ```json
    "features": {
		"ghcr.io/devcontainers/features/github-cli:1": {},
		"ghcr.io/devcontainers/features/python:1": {}
	}
    ```

3. 最後の `}` の終わりにコンマ（`,`）を追加します。これは10行目にあるはずです。
4. その行のすぐ下に、dev container に必要な拡張機能のリストを提供する次のコードを貼り付けます：

    ```json
    "customizations": {
		"vscode": {
			"extensions": [
				"GitHub.copilot",
				"GitHub.copilot-chat",
                "ms-azuretools.vscode-azure-github-copilot",
				"alexcvzz.vscode-sqlite",
				"astro-build.astro-vscode",
				"svelte.svelte-vscode",
				"ms-python.python",
				"ms-python.vscode-pylance"
			]
		}
	},
    ```

5. カスタマイゼーションのすぐ下に、codespace によって開発用に利用可能にすべきポートのリストを提供する次のコードを貼り付けます：

    ```json
    "forwardPorts": [
		4321,
		5100,
		5000
	],
    ```

6. ポートのリストのすぐ下に、コンテナ定義にスタートアップスクリプトを実行するコマンドを追加します：

    ```json
    "postStartCommand": "chmod +x /workspaces/dog-shelter/scripts/start-app.sh && /workspaces/dog-shelter/scripts/start-app.sh",
    ```

これでカスタムコンテナを定義しました！

## 新しく定義されたカスタムコンテナを使用する

誰かがあなたが定義した codespace を使用するときはいつでも、Node.js と Mongo DB、そして GitHub Copilot 拡張機能がインストールされた環境を持つことになります。このコンテナを使用しましょう！

1. コマンドパレット（<kbd>F1</kbd> またはクリック ☰ → View → Command Palette）にアクセスし、**dev container** と入力し始めます。
1. **rebuild** と入力し、**Codespaces: Rebuild container** を選択します。
1. ダイアログボックスで **Rebuild Container** を選択します。コンテナが再構築されます。

> [!IMPORTANT]
> コンテナの再構築には数分かかる場合があります。これは、一からすべてを作成するよりも速いとはいえ、開発者への迅速なアクセスを提供するのに理想的な状況ではないことは明らかです。幸い、開発者が数秒で起動できるように[codespace を事前構築][codespace-prebuild]できます。
>
> また、拡張機能のインストール時にウィンドウの再読み込みを求められる場合があります。プロンプトに従ってウィンドウを再読み込みしてください。

## リポジトリとの相互作用

GitHub Codespaces のカスタムコンテナは、リポジトリのソースコードの一部になります。したがって、標準のソース管理を通じて維持され、将来フォークされるときにリポジトリに従います。これにより、この定義をプロジェクトに貢献するすべての開発者間で共有できます。開発環境を定義するために[作成した Issue][walkthrough-previous]を閉じながら、新しい設定をアップロードしましょう。

> [!IMPORTANT]
> この演習の目的で、デフォルトブランチである `main` にコードの更新を直接プッシュしています。通常は[GitHub flow][github-flow]に従い、[後の演習][github-flow-exercise]で行います。

1. <kbd>Ctl</kbd> + <kbd>Shift</kbd> + <kbd>`</kbd> を選択するか、☰ → View → Terminal をクリックして、codespace で新しいターミナルウィンドウを開きます。
2. 次のコマンドを入力して、codespace を定義するための Issue 番号を見つけます：

    ```bash
    gh issue list
    ```

> [!NOTE]
> おそらく #1 でしょう。この演習の後半でこの番号を使用します。

3. すべてのファイルをステージし、Issue を解決するメッセージで変更をコミットし、main にプッシュします。ターミナルウィンドウで次のコマンドを入力し、`<ISSUE_NUMBER>` を前のステップで取得した番号に置き換えます：

    ```bash
    git add .
    git commit -m "Resolves #<ISSUE_NUMBER>"
    git push
    ```
> [!NOTE]
> プロンプトが表示された場合は、**Allow** を選択して codespace のコピー/ペーストを有効にします。

4. コマンドが完了したら、次を入力してすべての開いている Issue をリストします：

    ```bash
    gh issue list
    ```

5. codespace を定義する Issue がもはやリストされていないことに注意してください。あなたはそれを完了し、プルリクエストでそのようにマークしました！


## まとめと次のステップ
おめでとうございます！すべてのサービスと拡張機能を含むカスタム開発環境を定義しました。これにより、プロジェクトに貢献する際に通常必要な初期セットアップのハードルが取り除かれます。この codespace を使用してプロジェクトの[テストと継続的インテグレーションを実装][walkthrough-next]しましょう。

## リソース
- [GitHub Codespaces][codespaces]
- [GitHub Codespaces を始める][codespaces-docs]
- [dev containers の定義][dev-containers-docs]
- [GitHub Skills: Codespaces でコーディング][skills-codespaces]

| [← Project management with GitHub Issues][walkthrough-previous] | [Next: Continuous integration and testing →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[codespaces]: https://github.com/features/codespaces
[copilot-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot
[codespaces-docs]: https://docs.github.com/en/codespaces/overview
[codespace-prebuild]: https://docs.github.com/en/codespaces/prebuilding-your-codespaces
[dev-containers-docs]: https://docs.github.com/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers
[github-flow]: https://docs.github.com/en/get-started/quickstart/github-flow
[github-flow-exercise]: ./7-github-flow.md
[github-universal-container]: https://docs.github.com/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers#using-the-default-dev-container-configuration
[github-universal-container-definition]: https://github.com/devcontainers/images/blob/main/src/universal/.devcontainer/Dockerfile
[IDE]: https://en.wikipedia.org/wiki/Integrated_development_environment
[skills-codespaces]: https://github.com/skills/code-with-codespaces
[vscode-codespaces]: https://docs.github.com/en/codespaces/developing-in-codespaces/using-github-codespaces-in-visual-studio-code
[vscode-extensions]: https://code.visualstudio.com/docs/editor/extension-marketplace
[walkthrough-previous]: 2-issues.md
[walkthrough-next]: 4-testing.md
