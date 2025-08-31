原文: https://github.com/github-samples/pets-workshop/blob/6eaf29e155d12b62700aa06a97b803ac1aa1130a/content/how-github-uses-github.md

# GitHubはGitHubをどのように使用しているか

GitHubはGitHub上で構築されています。私たちは新しいツール、機能、製品を作成するために自分たちのツールを使用しています。これにより、私たちは製品が生産性と開発ライフサイクルを支援することを確実にするために、すべてに対して開発者ファーストのアプローチを取ることになりました。

あなたの組織がGitHub、そして潜在的にDevOpsを開始する際には、良い基盤から始めることが最善です。基盤を確立した後に、組織の特定のニーズに合わせて適応し、修正することが最適です。これらの一部は復習かもしれませんが、目標は、私たちGitHubでのGitHubの使用方法を探索することで、プロセスと実践を管理する方法についての洞察を提供することです。

## コアDevOps

DevOpsは「エンドユーザーに価値の継続的な提供を可能にするための人、プロセス、製品の結合」です。目標は、正しい理由で正しい方法で正しいものを構築することです。

典型的なDevOpsフローは5つの主要段階に分かれています：

1. 計画：何を、誰が、どのようなタイムラインで構築するかを決定します。
2. 開発：構築すべき機能をビルドします。
3. 協力：新しく構築された機能をレビューします。
4. 提供：新しく構築された機能をリリースします。
5. 運用：新しく構築された機能を監視し、構築すべき新しい機能を特定します。

GitHubはDevOpsライフサイクルのすべての段階にソリューションを提供し、プロセスを統合・合理化し、継続的にするツールを提供します。

## DevOpsライフサイクルの詳細

### 計画

GitHubでは、新機能は通常[ディスカッション](https://docs.github.com/discussions)から始まります。ディスカッションは新機能について、何を構築すべきか、そしてなぜそうすべきかについてのオープンな会話に最適な場所です。さらに重要なのは、行われた決定とそれらがどのように到達されたかのアーカイブを提供することです。GitHubには「URLでなければ起こらなかった」という言葉があります。堅牢なディスカッションを文書化することで、チームは過去から学び、うまくいけば間違いを繰り返すことを避けることができます。

そこから、[イシュー](https://docs.github.com/issues/tracking-your-work-with-issues/about-issues)が作成されます。各イシューは何を誰が構築するかを特定します。これらは通常[ブランチ](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)にリンクされ、最終的に[プルリクエスト](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)にリンクされます。

イシューは[プロジェクト](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)で計画・管理されます。プロジェクトを使用すると、チームはバックログとスケジュールを特定し、進捗を追跡できます。日次スタンドアップを行う際のベストプラクティスは、各イシューの現在の状態を特定するために「ボードを歩く」ことです。

### 開発

人気のあるIDEにはすべてGitHubのプラグインがあり、開発者は[リポジトリのクローン](https://docs.github.com/repositories/creating-and-managing-repositories/cloning-a-repository)、コードの[プル](https://github.com/git-guides/git-pull)と[プッシュ](https://github.com/git-guides/git-push)の更新を迅速に行うことができます。

しかし、開発プロセスはコードの作成と管理だけに限定されません。開発者は様々なパッケージをインストールし、「私のマシンでは動く」状況を避けるために一貫した環境を確保する必要があります。[GitHub Codespaces](https://docs.github.com/codespaces/overview)は、開発者が使用するためのクラウドで実行されるコンテナを定義する能力をチームに提供します。開発者は、ブラウザベースのVisual Studio Code、デスクトップ版Visual Studio Code、Visual Studio、JetBrainsを使用してコンテナに接続できます。

> GitHub開発者はGitHub Codespacesを定期的に使用しています。[事前ビルド](https://docs.github.com/codespaces/prebuilding-your-codespaces/about-github-codespaces-prebuilds)の使用により、GitHub.comモノリスは30秒で起動します

### 協力

[プルリクエスト（PR）](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)はGitHubでの生活の一部です。誰もが自分のチームのプロジェクトだけでなく、エンタープライズ全体のプロジェクトに対してもイシューを提出したり変更を提案したりすることが奨励されています。PRはこの哲学の中心です。

PRが提出されると、チームは[更新をレビューしてフィードバックを提供する](https://docs.github.com/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews)ことが奨励されています。PRテンプレートを作成して、イシューへのリンクや従うべきステップなど、PRで適切な情報が提供されることを確実にできます。[ステータスチェック](https://docs.github.com/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks)を定義して、変更がコードベースにマージされる前にテストが通過し、その他の品質メトリクスが満たされることを確実にできます。

### 提供

CI/CDはDevOpsで人気のある流行語です。CI/CDは製品の継続的な更新と改善に焦点を当てています。継続的インテグレーション（CI）はコードベースへの更新の取り込みに焦点を当て、継続的デプロイメントは新機能のデプロイメントを対象としています。成功するCI/CD実装の鍵は検証と自動化です。

検証はPRライフサイクルの一部であり、定義されたステータスチェックによって管理されます。自動化は、ステータスチェック、デプロイメント、その他のタスクに必要なプロセスが開発者の介入なしに実行されることを確実にします。開発者が別のツールを開いたり、手動でプロセスを実行したりする必要がある場合、それはフローから外れることを意味し、生産性の低下とタスクがスキップされる可能性を意味します。

[GitHub Actions](https://docs.github.com/actions)を使用すると、PRの作成、コードのコミット、イシューの提出など、様々なトリガーに応じて実行されるワークフローを定義できます。GitHub Actionsはテストを実行し、さまざまな操作を実行し、コードをデプロイできます。

### 運用

機能がデプロイされると、チームはアプリケーションを監視して問題を検出するためにさまざまなツールを使用します。問題が発生した場合にイシューを作成するために[GitHubのAPI](https://docs.github.com/rest)を使用できます。さらに、GitHub Actionsはwebhookに応答して実行でき、バグをフラグしたり、失敗したデプロイメントを特定したりできます。

## オープンソースコミュニティからの教訓

ほとんどのオープンソースソフトウェア（OSS）プロジェクトは、さまざまな背景とスキルレベルを持ち、地理的に分散している一連の貢献者によって維持されています。多くの貢献は、OSSをサイドプロジェクトと見なす人々から来ています。貢献者をサポートするためにOSSコミュニティによって開発された実践は、内部開発にも適用できます。このプロセスは通常InnerSourceと呼ばれます。

InnerSourceの完全な会話はこのセッションの範囲を超えていますが、InnerSourceは以下に重点を置いています：

- デフォルトとしての非同期コミュニケーション。
- すべてのプロジェクトの変更に対するPRの提出。
- 早期かつ頻繁なPRの提出、PRを小さく保つ。
- 新しいコードを作成する前に再利用するコードを検索する。
- デフォルトでリポジトリを公開にする。
- チーム間での協力を奨励する。

GitHubは内部でこれらの実践に従っています。これにより、集団思考を避け、開発者が最適に動作するスケジュールで貢献する柔軟性を確保し、誰もが貢献する機会を提供します。

## GitHub Enterpriseを始める

GitHub Enterpriseには、リポジトリやイシューなどのGitHubのコア機能と、企業やエンタープライズ向けのその他のツールスイートが含まれています。これは、GitHubを探索する一連のエンゲージメントのキックオフです。その結果、今日の焦点はあなたの組織のGitHubでの最初のステップになります。

### ユーザーと権限の管理

期待されるように、GitHubにアクセスするにはユーザーはアカウントが必要です。GitHubでアカウントを作成・管理する主な方法は2つあります：SAMLシングルサインオン（SSO）とEnterprise Managed Users（EMU）です。SSOアカウントでは、ユーザーは通常のGitHubアカウントを使用し、これがOktaやAzure Active Directory（AAD）などのアイデンティティプロバイダー（IdP）を使用して会社アカウントにリンクされます。Enterprise Managed Accountsは、会社アカウントに直接関連付けられたユーザー向けの新しいアカウントです。

EMUには、エンタープライズ外のプロジェクトに貢献できないなど、[いくつかの制限](https://docs.github.com/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users#abilities-and-restrictions-of-managed-user-accounts)があります。しかし、EMUはGitHub Enterprise（GHE）クラウドのウォールドガーデンを作成し、権限をユーザーの会社アカウントに直接関連付けることで、より高いセキュリティを提供します。SSOとEMUの選択は、作成しているプロジェクトの機密性と、ユーザーが会社外のプロジェクトに貢献する希望によって決まります。

個々のユーザーに権限を適用することは、管理オーバーヘッドの増加につながります。GitHubでは、[チーム](https://docs.github.com/organizations/organizing-members-into-teams/about-teams)の使用によってユーザーをグループ化できます。チームはユーザーのグループであり、リソースへのアクセスを提供するために使用できます。

リポジトリへのアクセスは[ロール](https://docs.github.com/organizations/managing-access-to-your-organizations-repositories/repository-roles-for-an-organization)によって管理されます。これらのロールは、ユーザーがリポジトリの内容を読むことのみを許可するReadから、リポジトリの削除を含むすべてのアクションを実行できるAdminまでの範囲があります！GitHub Enterpriseを使用する場合、必要な権限レベルに応じて[カスタムロール](https://docs.github.com/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/managing-custom-repository-roles-for-an-organization)を作成するオプションもあります。

#### GitHubがアカウントを管理する方法

- 多要素認証（MFAまたは2FA）はすべてのアカウントで**必須**です。
- 個別のアカウントに権限を付与するのではなく、チームを使用します。
- GitHubは、より高い機密性を持つプロジェクトにEMUを展開しながら、ほとんどのプロジェクトにSSOを使用します。
- [最小権限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)の原則を適用します。

### リポジトリ

[リポジトリ](https://docs.github.com/repositories/creating-and-managing-repositories/about-repositories)には、プロジェクトのファイル、メタデータ、履歴が含まれています。単なるファイルの場所以上に、リポジトリには作業項目の管理と変更の文書化のための[イシュー](https://docs.github.com/issues/tracking-your-work-with-issues/about-issues)と[プロジェクト](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)、プロジェクトの方向性についてコメントを提供するための[ディスカッション](https://docs.github.com/discussions)、そして過去と現在のすべてのファイルのすべてのバージョンがあります。

> GitHub内には「URLでなければ起こらなかった」という言葉があります。イシュー、ディスカッション、PRでの堅牢な履歴を持つことで、チームはプロジェクトがどこにあったか、どこに向かっているかを見ることができます。これは、何が試されたか、何が試されていないか、そしてなぜそれらの決定が行われたかのガイドとして機能します。このアーカイブが提供する答えは、過去の間違いが繰り返されないことを確実にし、プロジェクトが現在の状態にどのように到達したかの理解を助けます。

#### GitHubがリポジトリを管理する方法

- 一般的なルールとして、モノリポジトリは避けるべきです。大きなリポジトリは時間の経過とともに管理が困難になります。
- 権限は個別のフォルダーやファイルではなく、リポジトリにのみ付与できるため、リポジトリはセキュリティ要件に基づいて作成すべきです。
- 個別のチームではなく、組織全体でリポジトリをデフォルトで利用可能にすることで、発見、協力、コードの再利用を促進します。
- 可能な限り多くのタスクを自動化します。

> リポジトリを構造化する方法は数多くあり、必ずしも1つの「正しい方法」があるわけではありません。異なるチームは、構築しているもの、チームの文化とアプローチ、プロジェクトのデプロイ方法に基づいて異なる技術を使用します。

### GitHubでのプロジェクト管理

> プロジェクト管理についての完全な会話はこのワークショップの範囲を超えています。このセクションは、GitHubで利用可能な機能の紹介として設計されています。あなたの組織が機能をどのように使用するかを選択することは異なります。

[GitHub Projects](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)を使用すると、チームはプロジェクトを追跡、管理、計画できます。スプリントを特定し、イシューのバックログと状態を管理し、作業を割り当て、レポートを表示できます。

プロジェクトは複数のリポジトリにまたがることができます。その結果、より高いレベルでプロジェクトを管理し、チームと構築されているものを最もよくサポートするようにリポジトリを構造化できます。GitHub Projectsは軽量で、チームが適切と考える方法で使用する柔軟性を提供します。

イシューはリポジトリで作成されます。[イシューテンプレート](https://docs.github.com/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)を作成して、イシューに構造を提供し、必要な情報が文書化されることを確実にできます。

イシューは[ラベル](https://docs.github.com/issues/using-labels-and-milestones-to-track-work/managing-labels)でタグ付けでき、これによりアドホックなグループ化が可能になります。ラベルは機能、プロジェクト、またはその他の分類を特定するために使用できます。ラベルは迅速なフィルタリングと検索、ビューの作成に使用できます。検索条件はクエリ文字列の一部であるため、フィルタリングされたビューをブックマークして共有できます。

#### GitHubがプロジェクト管理にProjectsを使用する方法

- READMEを使用してプロジェクトを文書化します。
- リポジトリへの提案されたすべての変更に対してイシューを作成します。これにより、より良い履歴を提供し、プロジェクト管理を可能にします。
- すべての開発者やその他の貢献者にイシューで可能な限り多くの情報を提供するよう奨励します。「ドキュメントが多すぎる」ということはありません。
- 単一の信頼できる情報源を持ちます。プロジェクト管理に他のツールを使用している場合は、1つに決めてください。
- プロジェクトとイシュー管理を自動化します。自動化はラベルの適用、状態の管理、イシューの移行を行うことができます。
- 行われている作業の種類だけでなく、「Good first issue」、「Documentation」、「Urgent」、「Nice to have」などの他のメタデータをタグ付けするためにラベルを使用します。これにより、他のチームの開発者が注意が必要なイシューや、作業を始めるのに良い最初の項目を理解するのに役立ちます。

### フォークとブランチ

[ブランチ](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)はコードベースのバージョンです。すべてのリポジトリには1つのデフォルトブランチがあり、通常は**main**と呼ばれます。新しいブランチは、変更を他のブランチやデフォルトブランチにマージする前に導入してテストする新しいバージョンが必要な際に作成されます。ブランチは作成されたリポジトリ内に存在します。

[フォーク](https://docs.github.com/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks)は、開発者のユーザーアカウントなど、異なるアカウントや組織への、リポジトリ全体の特定時点でのコピーです。フォークを作成することで、開発者または開発者グループは元のソースコードに影響を与えることなく変更を行うことができます。変更はプルリクエストの使用により元のリポジトリにマージバックできます。

#### GitHubがフォークとブランチを使用する方法

- 常にブランチまたはフォークを作成することから始める。mainに直接編集またはプッシュしない。
- フォークは個別の探索や外部協力者を招待するのに最適です。
- ブランチは現在のプロジェクトチームによる協力と探索に最適です。

### プルリクエスト

プルリクエスト（PR）は、誰かにあなたの変更をリポジトリにプルしてもらうためのリクエストです。PRはGitHubでの協力の中核です。リポジトリの内容を変更するための通常のワークフローは以下のとおりです：

1. 見たい望ましい変更を文書化するためのイシューを作成します。
2. 必要なコードを追加または変更するためのフォークまたはブランチを作成します。
3. フォークまたはブランチから元のブランチへのプルリクエストを作成します。
4. コードレビューを要求し、必要に応じて更新を行います。
5. 自動テスト、セキュリティチェック、その他のバリデーターが、リポジトリに関連付けた[Actions](https://docs.github.com/actions)の一部として実行されます。
6. すべてのチェックが完了し、全員が変更に署名したら、プルリクエストが元のリポジトリにマージされます。

PRは変更の完全なアーカイブとして機能します。行われた変更、レビュアーによって提供されたフィードバック、検証やその他の自動ジョブの結果が含まれます。PRはすべての変更の履歴を提供し、チームがいつ、なぜ変更が行われたかを決定する能力を提供します。また、必要に応じて以前のバージョンに戻すことも簡素化します。

#### GitHubがプルリクエストを使用する方法

- PR履歴はプロジェクトの優れたアーカイブを提供します。
- 見たい変更をPRしてください！パッケージやプロジェクトが期待どおりに動作しない場合は、必要な更新でPRを作成してください。
- PRを小さく頻繁に保ちます。大きなPRよりも小さなPRの方が管理とマージがはるかに簡単です。大きなPRはスコープクリープの影響も受けやすいです。
- PRを受け入れないことは問題ありません。時々PRの目標は代替ルートを探索することです。時々要求された変更がプロジェクトに適切ではありません。
- [GitHub Actions](https://docs.github.com/actions)でプロセスを可能な限り自動化します。

### 保護されたブランチ

PRの提出には通常、コードがマージされる前に満たさなければならない要件のセットがあります。これらのルールの施行は[保護されたブランチ](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches)によって処理されます。保護されたブランチは、少なくとも1人のレビュアーが変更に署名している、特定の検証が実行されている、ルールが管理者に適用されるかどうかなど、いくつかの要件を特定できます。

> GitHubは、ほぼすべてのリポジトリのメインまたは中央ブランチに対して保護されたブランチを内部で使用しています。

#### GitHubが保護されたブランチを使用する方法

- ほぼすべてのリポジトリの中央またはメインブランチが保護されています。
- コードカバレッジ、テストの合格、その他の検証などのルールは、保護されたブランチとGitHub Actionsを通じて実装されています。

## 次のステップ

利用可能な新しいツールを使い始める最良の時期は今です！ユーザーのアカウントを作成・設定することから始めましょう。開発プロセスを管理するプロジェクトを作成します。リポジトリの構造を決定し、それらの作成を開始します。PRのルールを定義し、保護されたブランチを設定します。

チームがGitHubの使用を開始すると、利用可能なものについてより多くを学び、より多くの質問が出てくるでしょう。これは、GitHubを最大限に活用し、開発者の生産性を向上させるためのオンボーディングイベントシリーズの最初です。質問があれば担当者に連絡でき、次のイベントに参加してGitHubが提供するすべてをより深く掘り下げることができます。
