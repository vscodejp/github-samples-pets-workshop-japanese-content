# GitHub Issues を使ったプロジェクト管理

| [← Securing the development pipeline][walkthrough-previous] | [Next: Cloud-based development with GitHub Codespaces →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

「URL がないとそれは起こらなかった」は GitHub での共通のマントラで、開発プロセスを文書化することの重要性を強調するために使用されています。機能リクエストには履歴が必要です：誰がリクエストしたか、根拠は何か、プロセスに誰が関与したか、どのような決定が下されたか、なぜそれらが下されたか、機能が実装されたか、どのように実装されたか...このすべての情報は、将来の決定を推進し、過去の間違いを繰り返すことを避けるためのコンテキストを提供するのに役立ちます。

GitHub は、[GitHub Discussions][discussions]、[wikis][wikis]、[プルリクエスト][about-prs]、[GitHub Issues][issues] など、コラボレーションとプロジェクト管理を可能にする様々な機能を提供しています。これらのそれぞれが、組織の作成プロセスを推進するのに役立ちます。私たちは GitHub Issues に焦点を当てます。これは GitHub でのプロジェクト管理の基盤です。

その核心において、Issue は何らかの形でのアクションを文書化します。それは機能のリクエスト、バグレポート、またはチームによって実行されるその他の操作である可能性があります。GitHub Issues を使用するための規定された方法論はなく、チームがプロジェクトを管理し推進する最適な方法を決定できます。チームが Issue に実装する一般的なフローは：

1. 新しい機能をリクエストしたり、バグレポートをファイルするために Issue をファイルする。
1. Issue について議論し、リクエストを解決するための適切な人とメカニズムを決定する。
1. リクエストの提案された実装でプルリクエストを作成する。
1. プルリクエストについてさらに議論し、レビューする。
1. 全員が満足してサインオフしたら、プルリクエストをマージして Issue をクローズする。

## シナリオ

シェルターはウェブサイトに新機能を追加し始めたいと考えています。まず、ランディングページに当日の営業時間を表示することから始めたいと考えています。また、現在および将来の更新の両方について開発と DevOps をサポートするための更新も必要です。これらの更新を追跡して、実行されている作業を文書化したいと考えています。リポジトリに Issue を作成することでこれを行います。

## 機能リクエストを管理するための Issue の作成

私たちのプロジェクトには2つの主要な更新が必要です。プロジェクトの開発をサポートするための更新と、シェルターの営業時間を表示する新しいコンポーネントをウェブサイトに追加することです。これらのそれぞれに対して Issue を作成しましょう。次のいくつかの演習で、これらのリクエストを解決するためにプロジェクトに適切な更新を加え始めます。

1. このワークショップの開始時に作成したリポジトリに戻ります。
1. **Issues** タブを選択します。
1. **New issue** を選択します。
2. タイプを求められた場合は、**Blank issue** を選択します。
3. 作成プロセスを効率化するために、ページの下部にある **Create more** を選択します。
4. 下の表に示された情報を追加して新しい Issue を作成し、それぞれを作成した後に **Submit new issue** を選択します：

    | タイトル                | 説明                                                                            |
    | ----------------------- | ------------------------------------------------------------------------------ |
    | Define codespace        | クラウド開発を可能にするために codespace に必要な定義を作成する                      |
    | Implement testing       | 継続的インテグレーションのためのテストを自動化するワークフローを作成する                 |
    | Add filters to dog list | ユーザーが犬を品種と利用可能性でフィルタリングできるようにするコードを追加する           |

> [!TIP]
> タイトルまたは説明フィールドで <kbd>Ctl</kbd> - <kbd>Enter</kbd>（Mac では <kbd>Cmd</kbd> - <kbd>Return</kbd>）を押すことで Issue を保存することもできます。

これで、ワークショップのすべての Issue を定義しました！これらの Issue を使用して、ワークショップ全体での進捗をガイドします。

## まとめと次のステップ
GitHub Issues は GitHub でのプロジェクト管理の核心です。その柔軟性により、組織は開発ライフサイクルの方法論をサポートする最適な行動方針を決定できます。Issue を作成したので、プロジェクトへの最初の大きな変更である[codespace の定義][walkthrough-next]に注意を向ける時です。

## リソース
- [GitHub Issues][issues-docs]
- [Markdown を使ったコミュニケーション][skills-markdown]
- [GitHub Projects][projects-docs]

| [← Securing the development pipeline][walkthrough-previous] | [Next: Cloud-based development with GitHub Codespaces →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[discussions]: https://github.com/features/discussions
[wikis]: https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis
[about-prs]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests
[issues]: https://github.com/features/issues
[issues-docs]: https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues
[projects-docs]: https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects
[skills-markdown]: https://github.com/skills/communicate-using-markdown
[walkthrough-next]: 3-codespaces.md
[walkthrough-previous]: 1-code-scanning.md