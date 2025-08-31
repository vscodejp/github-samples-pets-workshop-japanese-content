# GitHub Copilot を使ったコーディング

| [← Helping GitHub Copilot understand context][walkthrough-previous] | [Next: GitHub flow →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

私たちは GitHub Copilot を使ってプロジェクトを探索し、期待する品質の提案を確実に受け取るためのコンテキストを提供する方法を探索してきました。今度は、新しいコードを生成してこれらすべての準備作業を実行に移すことに注意を向けましょう！GitHub Copilot を使ってウェブサイトに機能を追加し、必要な単体テストを生成する手助けを受けます。

## シナリオ

ウェブサイトは現在、データベース内のすべての犬をリストしています。シェルターに犬が少ししかいなかった時はこれで適切でしたが、時間が経つにつれて数が増え、人々が採用可能な犬を探すのが困難になりました。シェルターは、ユーザーが犬の品種を選択し、採用可能な犬のみを表示できるフィルターをウェブサイトに追加するよう依頼しました。

## この演習の概要

次のいくつかのステップで、以下を行います：

- 利用可能な品種をリストする新しい Flask エンドポイントを作成する。
- 関連する単体テストを追加する。
- シナリオで要求されるリストを表示し、フィルターを追加するためにバックエンドとフロントエンドを更新する。

## GitHub Copilot インターフェース

これまで、主に GitHub Copilot チャットに焦点を当ててきました。これはおそらく GitHub Copilot と対話する最も一般的な方法になるでしょう。対話的に質問することができ、個々のファイルや（Copilot Edits を使用して）複数のファイルにわたって操作を実行する能力があります。また、コード補完からも GitHub Copilot のサポートを受けることができ、これはコーディング中に提案を提供します。これらの3つの機能のそれぞれを探索していきます。

## コード補完で新しい Flask ルートを作成する

コード補完は、Copilot が持つコンテキストに基づいて、あなたが次に入力しようとしているコードブロックを予測します。コード補完の場合、これには現在作業しているファイルと IDE で開いているタブが含まれます。

> [!IMPORTANT]
> 現時点では、Copilot 指示ファイルは Copilot チャットでのみ利用可能です。

コード補完は、何をしたいかがわかっていて、途中でちょっとした手助けを受けながらコードを書き始めることに満足している状況に最適です。提案は、書いたコード（例：関数定義）とコードに追加したコメントの両方に基づいて生成されます。

> [!NOTE]
> GitHub Copilot にコンテキストを提供する素晴らしい方法の一つは、コードにコメントを追加することです。何が行われているかを説明するコメントは時々余計な場合がありますが、Copilot が何を構築しているかをより良く理解するのに役立ちます。

コード補完の助けを借りて、Flask バックエンドで新しいルートを構築しましょう。

1. Codespace に戻るか、リポジトリに移動し**Code** > **Codespaces**とCodespaceの名前を選択して再度開きます。
2. **server/app.py**を開きます。
3. サーバーを起動する最下部のコードセクションを見つけ、その直上にカーソルを置きます。これは70行目で、コードは以下のようになっているはずです：

    ```python
    if __name__ == '__main__':
      app.run(debug=True, port=5100) # Port 5100 to avoid macOS conflicts
    ```

4. データベースを呼び出してすべての品種を見つけ、それらの名前とIDを含むJSON配列を返すルートを作成します。`@app.route`と入力を始めるか、`# Route to get all breeds`のような要件を含むコメントを追加すると、GitHub Copilot によって生成されたイタリック体のテキストに気づくはずです。
5. <kbd>Tab</kbd>を選択してコード提案を受け入れます。
6. [http://localhost:5100/api/breeds][localhost-breeds]に移動してルートを検証します。

> [!NOTE]
> 前の演習と同様に、学習体験の一部として Copilot との対話方法を発見することを目的としているため、Copilot で使用する特定のプロンプトは提供していません。Flask やルートの追加方法に慣れていない場合は、上記で定義されたルートを参考にするか、Copilot チャットにガイダンスを求めることができます！

## ユニットテストを生成する

ルートが作成されたので、コードが正しいことを確認するためにテストを追加したいと思います。GitHub Copilot チャットのスラッシュコマンド **/tests** を使用してテストを作成できます！

1. Codespace または VS Code に戻ります。
2. 前のステップで生成したコードをハイライトします。
3. GitHub Copilot チャットを開きます。
4. `+`ボタンを選択して新しいチャットを開始します。
5. **/tests**と入力し、<kbd>tab</kbd>を選択してコマンドを有効化し、<kbd>enter</kbd>を押してコマンドを実行します。GitHub Copilot がテストを生成します！
6. 生成されたコード提案の上にある**Apply edits**ボタンを選択して、**test_app.py**に変更を適用します。
7. コードをレビューして検証し、必要な変更を行います。満足したら**Keep**を選択します。
> [!IMPORTANT]
> GitHub Copilot は、他の生成AI ソリューションと同様に間違いを犯すことがあります。生成されたコードを常にレビューし、正確で期待通りに動作することを確認するために必要な変更を行ってください。
8. <kbd>Ctl</kbd>+<kbd>Shift</kbd>+<kbd>`</kbd>を選択して、Codespace または VS Code でターミナルウィンドウを開きます。
9. ターミナルコマンド`source ./venv/bin/activate`を実行して仮想サーバーが有効化されていることを確認します。
10. ターミナルコマンド`cd server`を実行して**server**フォルダに移動します。
11. ターミナルコマンド`python -m unittest`を実行してテストを実行します。
12. すべてのテストが合格することを確認してください！

## フィルターを追加する

ページにフィルターを追加するには、最低3つのファイルの更新が必要です - Flask バックエンド、Flask バックエンドのユニットテスト、Svelte フロントエンド。幸い、Copilot Edits は複数のファイルを更新できます！Copilot Edits の助けを借りてページを更新しましょう。

1. IDE で以下のファイルを開きます（Copilot チャットがコンテキストとして参照できるように）：
   - **server/app.py**
   - **server/test_app.py**
   - **client/src/components/DogList.svelte**
2. GitHub Copilot Chat を開きます。
3. チャットビューの下部のチャットモードドロップダウンで**Edit**を選択して編集モードに切り替えます（現在は**Ask**になっているはずです）。
4. 利用可能な場合は、モデルに**Claude 3.7 Sonnet**を選択します。
5. チャットウィンドウで**Add Context...**を選択します。
6. **server/app.py**、**client/src/components/DogList.svelte**、**server/test_app.py**ファイルを選択します（各ファイルに対して**Add context**を選択する必要があります）。
> [!TIP]
> **Add context**をクリックした後にファイル名を入力すると、フィルターに表示されます。ファイルをドラッグしたり、エクスプローラーでファイルを右クリックして`Copilot -> Add File to Chat`を選択することもできます）
7. Copilot に実行したい操作を依頼し、フィルターを追加するためにページを更新します。以下の要件を満たす必要があります：
    - すべての品種を含むドロップダウンリストを提供する
    - 利用可能な犬のみを表示するチェックボックスを利用可能にする
    - 変更が行われるたびにページが自動的に更新される
    - エンドポイントへの変更に対してテストを更新する
8. コード提案をレビューして期待通りに動作することを確認し、必要な変更を行います。満足したら、ファイルを個別に**Keep**を選択するか、Copilot Chat ですべての変更を受け入れることができます。
9. [http://localhost:4321][localhost]でページを開いて更新を確認してください！
10. 以前に行ったように、ターミナルで`python -m unittest`を使用して Python テストを実行します。
11. 変更が必要な場合は、GitHub Copilot に必要な更新を説明し、新しいコードを生成させます。

> [!IMPORTANT]
> AI ペアプログラマーとのコーディングでは、反復的に作業することが通常の側面です。Copilot が理解できるようにより多くのコンテキストを提供したり、追加のリクエストを行ったり、元のプロンプトを言い換えたりすることができます。

## まとめと次のステップ
おめでとうございます！GitHub Copilot と協力してウェブサイトに新機能 - 犬のリストをフィルタリングする機能を追加しました。[新機能でプルリクエストを作成する][walkthrough-next]ことで締めくくりましょう！

## リソース
- [IDE で GitHub Copilot に質問する][copilot-questions]
- [Copilot Edits][copilot-chat-edits]
- [Copilot Chat クックブック][copilot-chat-cookbook]

| [← Helping GitHub Copilot understand context][walkthrough-previous] | [Next: GitHub flow →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[copilot-chat-cookbook]: https://docs.github.com/en/copilot/copilot-chat-cookbook
[copilot-chat-edits]: https://code.visualstudio.com/docs/copilot/copilot-edits
[copilot-questions]: https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/asking-github-copilot-questions-in-your-ide
[localhost]: http://localhost:4321
[localhost-breeds]: http://localhost:5100/api/breeds
[walkthrough-previous]: 5-context.md
[walkthrough-next]: 7-github-flow.md
