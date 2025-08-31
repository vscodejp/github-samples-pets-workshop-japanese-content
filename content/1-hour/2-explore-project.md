# GitHub Copilotがコンテキストを理解するために

| [← GitHub Copilotでコーディング][walkthrough-previous] | [次へ: カスタム指示の提供 →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

コーディング（そして人生の多く）における成功の鍵はコンテキストです。コードベースにコードを追加する前に、すでに設置されているルールと構造を理解したいと思います。GitHub CopilotなどのAIコーディングアシスタントと作業する場合も同じ概念が適用されます - 提案の品質はCopilotが持っているコンテキストに直接比例します。この機会を使用して、与えられたプロジェクトを探索し、Copilotが最高の仕事をするために必要なコンテキストを確実に持っているようにCopilotとやり取りする方法の両方を学びましょう。

## シナリオ

ウェブサイトに新しい機能を追加する前に、既存の構造を探索して、更新が必要な場所を決定したいと思います。

## チャット参加者と拡張機能

GitHub Copilot Chatには、GitHub Copilotに指示を提供したり、外部サービスにアクセスしたりするために利用できる[チャット参加者][chat-participants]と[拡張機能][copilot-extensions]のセットがあります。チャット参加者はIDE内で動作し、プロジェクトにアクセスできるヘルパーであり、拡張機能は外部サービスを呼び出して、別のツールを開くことなく情報を提供できます。1つのコアチャット参加者である`@workspace`に焦点を当てます。

`@workspace`はプロジェクトのインデックスを作成し、現在作業している内容について質問したり、プロジェクト内のリソースを見つけたり、コンテキストに追加したりできます。プロジェクト全体を考慮すべき場合や、どこから始めればよいかわからない場合に使用するのが最適です。現在のシナリオでは、プロジェクトについて質問したいので、`@workspace`は仕事に最適なツールです。

> [!NOTE]
> この演習では、学習体験の一部としてCopilotとやり取りする方法を発見することなので、入力する特定のプロンプトを提供しません。自然言語で自由に話し、探していることや達成する必要があることを説明してください。

1. プロジェクトが開いているIDEに戻ります。
2. IDEで開いている可能性のあるタブをすべて閉じて、Copilotチャットのコンテキストがからであることを確認します。
3. GitHub Copilot Chatを開きます。
4. Copilotチャットの上部にある`+`アイコンを選択して新しいチャットを開始します。
5. チャットプロンプトウィンドウで`@workspace`と入力し、<kbd>tab</kbd>を押して選択またはアクティブ化し、Copilotにプロジェクトについて尋ねることを続けます。使用されている技術、プロジェクトが何をするか、機能がどこに存在するかなどについて尋ねることができます。
6. 数分間探索して、次の質問への答えを見つけてください：
    - プロジェクトが使用するデータベースはどこにありますか？
    - 犬をリストするために関与するファイルは何ですか？

## 概要と次のステップ

GitHub Copilotでコンテキストを探索しました。これは品質の高い提案を生成するための鍵です。チャット参加者を使用してGitHub Copilotをガイドする方法と、自然言語でプロジェクトを探索する方法を見ました。[Copilot指示][walkthrough-next]の使用を通じて、Copilotチャットにさらに多くのコンテキストを提供する方法を見てみましょう。

## リソース

- [Copilot Chatクックブック][copilot-cookbook]
- [VS CodeでCopilot Chatを使用][copilot-chat-vscode]
- [Copilot拡張機能マーケットプレース][copilot-marketplace]

| [← GitHub Copilotでコーディング][walkthrough-previous] | [次へ: カスタム指示の提供 →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[chat-participants]: https://code.visualstudio.com/docs/copilot/copilot-chat#_chat-participants
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/copilot-chat
[copilot-cookbook]: https://docs.github.com/en/copilot/copilot-chat-cookbook
[copilot-extensions]: https://docs.github.com/en/copilot/using-github-copilot/using-extensions-to-integrate-external-tools-with-copilot-chat
[copilot-marketplace]: https://github.com/marketplace?type=apps&copilot_app=true
[walkthrough-previous]: ./1-add-endpoint.md
[walkthrough-next]: ./3-copilot-instructions.md