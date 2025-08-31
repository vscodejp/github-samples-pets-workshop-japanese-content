原文: https://github.com/github-samples/pets-workshop/blob/6eaf29e155d12b62700aa06a97b803ac1aa1130a/content/1-hour/1-add-endpoint.md

# GitHub Copilotでコーディング

| [← ワークショップのセットアップ][walkthrough-previous] | [次へ: GitHub Copilotがコンテキストを理解するために →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|


コード補完により、GitHub Copilotはコーディング中にコードエディター内で提案を提供します。これによって、コメントをコードに変換したり、次の行のコードを生成したり、シグネチャだけから関数全体を生成したりできます。コード補完は、入力する必要がある定型コードや形式的な処理の量を削減し、作成している重要な側面に集中できるようにします。

## シナリオ

アプリケーションに機能を追加するときは、段階的に作業するのが標準的です。ユーザーが犬種に基づいて犬のリストをフィルタリングできるようにしたいことがわかっているので、すべての犬種のリストを提供するエンドポイントを追加する必要があります。後で残りの機能を追加しますが、今のところはこの部分に焦点を当てましょう。

アプリケーションは、バックエンドAPI（[/server][server-code]フォルダ内）としてSQLAlchemyを使用したFlaskアプリ、フロントエンド（[/client][client-code]フォルダ内）としてSvelteを使用したAstroアプリを使用しています。後でプロジェクトの詳細を探索しますが、この演習はFlaskアプリケーションのみに焦点を当てます。

> [!NOTE]
> アプリケーションに変更を加え始めると、常に重大な変更が作成される可能性があります。ページが動作しなくなった場合は、アプリケーションを開始するために以前に使用したターミナルウィンドウでエラーメッセージがないか確認してください。<kbd>Ctl</kbd>+<kbd>C</kbd>を使用してアプリを停止し、`./scripts/start-app.sh`を実行して再起動できます。

## Flaskルート

[Flaskでのルーティング][flask-routing]の完全な概要を提供することはできませんが、Pythonデコレータ`@app.route`を使用して定義されます。`@app.route`に提供できるパラメータがいくつかあり、ルートにアクセスするために使用するパス（またはURL）（**api/breeds**など）や、使用できる[HTTPメソッド][http-methods]が含まれます。

## コード補完

コード補完は、Copilotが持っているコンテキストに基づいて、次に入力しようとしているコードブロックを予測します。コード補完の場合、これには現在作業しているファイルとIDEで開いているタブが含まれます。

コード補完は、何をしたいかがわかっていて、途中で少し手助けをしてもらいながらコードを書き始めることに満足している状況に最適です。提案は、作成するコード（関数定義など）とコードに追加するコメントの両方に基づいて生成されます。

## breedsエンドポイントの作成

コード補完の助けを借りて、Flaskバックエンドでルートをビルドしましょう。

> [!IMPORTANT]
> この演習では、提供されたコードスニペットをコピー&ペーストするのではなく、手動で入力してください。これにより、デスクでコーディングしている場合と同じようにコード補完を体験できます。GitHub Copilotが残りを提案し始める前に、数文字しか入力する必要がないことがおそらくわかるでしょう。

1. プロジェクトが開いているIDEに戻ります。
2. **server/app.py**を開きます。
3. `## HERE`と書かれたコメントを見つけます。これは68行目にあるはずです。
4. Copilotの混乱を避けるためにコメントを削除し、カーソルをそこに置きます。
5. **api/breeds**のエンドポイントからすべての犬種を返すルートを作成するためのコードの追加を、次のように入力して開始します：

    ```python
    @app.route('/api/breeds', methods=['GET'])
    ```

6. 完全な関数シグネチャが表示されたら、<kbd>Tab</kbd>を選択してコード提案を受け入れます。
7. まだ表示されていない場合、コード補完は関数シグネチャの残りを提案するはずです。前回と同様に<kbd>Tab</kbd>を選択してコード提案を受け入れます。

    生成されたコードは次のようになるはずです：

    ```python
    @app.route('/api/breeds', methods=['GET'])
    def get_breeds():
        # Query all breeds
        breeds_query = db.session.query(Breed.id, Breed.name).all()

        # Convert the result to a list of dictionaries
        breeds_list = [
            {
                'id': breed.id,
                'name': breed.name
            }
            for breed in breeds_query
        ]

        return jsonify(breeds_list)
    ```

> [!IMPORTANT]
> LLMは確率的であり、決定論的ではないため、生成される正確なコードは異なる場合があります。上記は代表的な例です。あなたのコードが異なっていても、動作する限り問題ありません！

8. 新しく作成した関数にコメントを追加します。これを行うには、関数内にカーソルを置きます（`def get_breeds...`行と`return jsonify...`行の間の任意の場所）。次に、<kbd>Ctl</kbd>+<kbd>I</kbd>（Macでは<kbd>cmd</kbd>+<kbd>I</kbd>）を押してエディターインラインチャットを開きます。入力ボックスに`/doc`と入力します。（追加の詳細を提供することもできますが、必須ではありません）。これにより、GitHub Copilotが関数のドキュメントコメントを生成するよう促されます。提案されたコメントがコード内にインラインで表示されます（緑色でハイライト）。**Accept**をクリックしてコメントをコードに適用するか、**Close**をクリックして提案を破棄します。スラッシュコマンドを使用しました。これはタスクを合理化するショートカットであり、これらのコマンドは冗長なプロンプトの必要性を排除します。

9. ファイルを**保存**します。

## エンドポイントの検証

コードが作成され保存されたので、エンドポイントが動作することを確認するために簡単に検証しましょう。

1. [http://localhost:5100/api/breeds][breeds-endpoint]に移動してルートを検証します。犬種のリストを含むJSONが表示されるはずです！

## 概要と次のステップ

GitHub Copilotの助けを借りて新しいエンドポイントを追加しました！Copilotが次に探していそうなコードブロックを予測し、インラインで提案を提供して、手動で入力する手間を省いてくれることがわかりました。[プロジェクトを探索する][walkthrough-next]ことで、より複雑な操作を実行する道筋を始めましょう。

## リソース

- [IDEでGitHub Copilotを使ったコード提案][copilot-suggestions]
- [VS CodeでGitHub Copilotを使ったコード補完][vscode-copilot]
- [プロンプト作成][prompt-crafting]
- [インラインチャット][inline-chat]


| [← ワークショップのセットアップ][walkthrough-previous] | [次へ: GitHub Copilotがコンテキストを理解するために →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[breeds-endpoint]: http://localhost:5100/api/breeds
[client-code]: /client/
[copilot-suggestions]: https://docs.github.com/en/copilot/using-github-copilot/getting-code-suggestions-in-your-ide-with-github-copilot
[flask-routing]: https://flask.palletsprojects.com/en/stable/quickstart/#routing
[http-methods]: https://www.w3schools.com/tags/ref_httpmethods.asp
[prompt-crafting]: https://code.visualstudio.com/docs/copilot/prompt-crafting
[inline-chat]: https://code.visualstudio.com/docs/copilot/chat/inline-chat
[server-code]: /server/
[vscode-copilot]: https://code.visualstudio.com/docs/copilot/ai-powered-suggestions
[walkthrough-previous]: ./0-setup_jp.md
[walkthrough-next]: ./2-explore-project.md