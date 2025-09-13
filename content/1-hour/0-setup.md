原文: https://github.com/github-samples/pets-workshop/blob/6eaf29e155d12b62700aa06a97b803ac1aa1130a/content/1-hour/0-setup.md

# ワークショップのセットアップ

| [← GitHub Copilotの開始][walkthrough-previous] | [次へ: GitHub Copilotでコーディング →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

このワークショップを完了するには、このリポジトリの内容をコピーしたリポジトリを作成する必要があります。これは[リポジトリのフォーク][fork-repo]で行うことができますが、フォークの目的は最終的にコードを元の（またはアップストリーム）ソースにマージすることです。私たちの場合、変更をマージする意図がないため、別のコピーが必要です。これは[テンプレートリポジトリ][template-repo]の使用によって実現されます。テンプレートリポジトリは、組織にスターターを提供し、プロジェクト間での一貫性を確保する優れた方法です。

このワークショップのリポジトリはテンプレートとして設定されているため、これを使用してあなたのリポジトリを作成できます。

> [!IMPORTANT]
> [必要なソフトウェア][required-software]と[必要なリソース][required-resources]のセットアップが完了していることを確認してください。

## リポジトリの作成

ワークショップで使用するリポジトリを作成しましょう。

> [!IMPORTANT]
> (日本コミュニティ補足) DevContainer及び、GitHub Codespacesを利用する場合には、以下のリポジトリではなく、[https://github.com/vscodejp/github-samples-pets-workshop-japanese-template](https://github.com/vscodejp/github-samples-pets-workshop-japanese-template)を利用してください。必要な設定が追加されています。

1. [翻訳前のワークショップリポジトリ https://github.com/github-samples/pets-workshop/](https://github.com/github-samples/pets-workshop/) に移動します
2. **Use this template** > **Create a new repository**を選択します

    ![Use this templateドロップダウンのスクリーンショット](images/0-setup-template.png)

3. **Owner**の下で、あなたのGitHubハンドルの名前、またはワークショップリーダーが指定した所有者を選択します。
4. **Repository**の下で、名前を**pets-workshop**に設定するか、ワークショップリーダーが指定した名前にします。
5. 可視性に**Public**が選択されていることを確認するか、ワークショップリーダーが指示した値にします。
6. **Create repository from template**を選択します。

    ![設定されたテンプレート作成ダイアログのスクリーンショット](images/0-setup-configure.png)

しばらくすると、このワークショップのテンプレートから新しいリポジトリが作成されます！

## リポジトリのクローンとアプリの開始

> ![IMPORTANT]
> (日本コミュニティ補足) Dev Container及び、GitHub Codespacesを利用する場合には手順が異なります。["DevContainerの利用"](#devcontainerの利用)、["GitHub Codespacesの利用"](#github-codespacesの利用)を参照してください。

リポジトリが作成されたので、今度はリポジトリをローカルにクローンします。BASHコマンドを実行できるシェルから行います。

1. 前のセットで作成したリポジトリのURLをコピーします。
2. ターミナルまたはコマンドシェルを開きます。
3. 次のコマンドを実行してリポジトリをローカルにクローンします（適切に親ディレクトリにディレクトリを変更してください）：

    ```sh
    git clone <INSERT_REPO_URL_HERE>
    ```

4. 次のコマンドを実行してクローンしたリポジトリにディレクトリを変更します：

    ```sh
    cd <REPO_NAME_HERE>
    ```

5. 次のコマンドを実行してアプリケーションを開始します：

    ```sh
    ./scripts/start-app.sh
    ```

スタートアップスクリプトは2つのアプリケーションを開始します：

- [localhost:5100][flask-url]のバックエンドFlaskアプリ。[dogs API][dogs-api]を開くことで犬のリストを見ることができます。
- [localhost:4321][astro-url]のフロントエンドAstro/Svelteアプリ。そのURLを開くことで[ウェブサイト][website-url]を見ることができます。

### 日本コミュニティの補足

#### bashの代わりにPowerShellでの実行

Windowsを使用していて、PowerShell 7+がインストールされている場合`./scripts/start-app.ps1`が使用できます。Windows11はPowerShell 5であるため、追加のインストールが必要です。

```
# wingetでのインストール
winget install --id Microsoft.Powershell --source winget

pwsh .\scripts\start-app.ps1
```

#### nodejs、pythonを環境管理ツールで実行している方

環境を立ち上げるコマンド[./scripts/start-app.sh](https://github.com/github-samples/pets-workshop/blob/main/scripts/start-app.sh)は、Python、Node.jsのパッケージをインストールし、さらに開発サーバを立ち上げるスクリプトです。

macOS/linuxでは`python3`、`pip`、`npm`、Windowsでは`py`、`pip`、`npm`のコマンドが実行できることを前提とされています。

このコマンドは、パッケージのインストール段階として以下のことを行っています。

**macOS/Linuxの場合**

```
# Pythonの仮想環境の作成
python3 -m venv venv

# Pythonの仮想環境の有効化
source venv/bin/activate || . venv/bin/activate

# Pythonのパッケージのインストール
pip install -r server/requirements.txt

# クライアントディレクトリへに移動
cd ./client

# Node.jsのパッケージのインストール
npm install
```

**Windowsの場合**

```
# Pythonの仮想環境の作成
py -m venv venv

# Pythonの仮想環境の有効化
source venv/Scripts/activate || . venv/Scripts/activate

# Pythonのパッケージのインストール
pip install -r server/requirements.txt

# クライアントディレクトリへに移動
cd ./client

# Node.jsのパッケージのインストール
npm install
```

プログラムの実行には以下のコマンドを実行しています。
それぞれプロセスとして動作するため、別のターミナルを立ち上げて実行してください。

**macOS/Linuxの場合**

```
# Pythonのプログラムの起動
cd ./server
python3 app.py

# Nodejsのプログラムの起動
cd ./client
npm run dev
```

**Windowsの場合**

```
# Pythonのプログラムの起動
cd ./server
py app.py

# Nodejsのプログラムの起動
cd ./client
npm run dev
```

Pythonのパッケージマネージャであるpyenvを利用している場合は以下のようにしてください。

```
# 新しめのPythonをインストール
pyenv install 3.13.7
# ローカルディレクトリでの有効化
pyenv local 3.13.7

# ~/.penv/shims にパスが通っていない場合、以下のコマンドを実行してください
eval "$(pyenv init -)"

# Pythonパッケージのインストール
pip install -r server/requirements.txt
# Pythonのプログラムの起動
cd ./server
python app.py
```

Pythonのパッケージマネージャであるuvを利用している場合は以下のようにしてください。

```
# Pythonの仮想環境の作成
uv venv -p3.13
# Pythonパッケージのインストール
uv pip install -r server/requirements.txt
# Pythonのプログラムの起動
cd ./server
uv run python app.py
```

Node.jsのバージョン管理ツールnodenvを利用している場合は以下のようにしてください。

```
# 新しめのバージョンのインストール
nodenv install 22.18.0
# ローカルディレクトリでの有効化
nodenv local 22.18.0
# nodeのバージョン確認
node -v

# ~/.nodenv/shims にパスが通っていない場合、以下のコマンドを実行してください
eval "$(nodenv init -)"

# Node.jsのパッケージのインストール
cd ./client
npm install
# Nodejsのプログラムの起動
npm run dev
```

## エディターを開く

コードをローカルにクローンし、サイトが動作しているので、VS Codeでコードベースを開きましょう。

1. VS Codeを開きます。
2. **File** > **Open Folder**を選択します。
3. この演習で先ほどクローンしたプロジェクトが含まれるフォルダに移動します。
4. フォルダがハイライトされた状態で、**Open folder**を選択します。

## DevContainerの利用

以下の手順で利用します。

## GitHub Codespacesの利用

前述の通り、テンプレートリポジトリが通常と異なり、https://github.com/vscodejp/github-samples-pets-workshop-japanese-template となります。

以下の手順で利用します。

1. 前のセットで作成したリポジトリのURLをコピーします。
2. ターミナルまたはコマンドシェルを開きます。
3. 次のコマンドを実行してリポジトリをローカルにクローンします（適切に親ディレクトリにディレクトリを変更してください）：

    ```sh
    git clone <INSERT_REPO_URL_HERE>
    ```
4. VS Codeを開きます。
5. **ファイル(File)** > **フォルダーを開く(Open Folder)**を選択します。
6. この演習で先ほどクローンしたプロジェクトが含まれるフォルダに移動します。
7. フォルダがハイライトされた状態で、**開く(Open folder)**を選択します。
8. F1を押して、コマンド「開発コンテナー: コンテナーで再度開く(Dev Containers: Reopen in Container)」を実行します。
9. しばらくすると、コンテナが立ち上がり、VS Codeが再起動します。
10. VS Code内のターミナルを開きます（下部のパネル内にあります）。
11. 次のコマンドを実行してアプリケーションを開始します：

    ```sh
    ./scripts/start-app.sh
    ```

## GitHub Codespacesの利用

前述の通り、テンプレートリポジトリが通常と異なり、https://github.com/vscodejp/github-samples-pets-workshop-japanese-template となります。

以下の手順で利用します。

1. 前のセットで作成したリポジトリにおいて、"Code"ボタンから、"Codespaces"タブを選択し、"Create codespace on main"を選択します。

    <img src="images/vscodejp_added/create_codespace_on_main.png" width="70%" />

2. Webブラウザ上にVS Codeが表示されます。構築完了までに時間がかかります。右下のインジケータが消えるまでお待ちください。
3. Webブラウザ上のVS Code内でも作業できますが、ローカルのVS Codeから接続した方が操作しやすいです。左下のCodespacesと書かれた部分をクリックし、表示されるメニューから"Open in VS Code Desktop"を選択します。

    <img src="images/vscodejp_added/remote_button.png" width="50%" />

4. ローカルのVS Codeが起動し、Codespacesに接続されます。
5. VS Code内のターミナルを開きます（下部のパネル内にあります）。
6. 次のコマンドを実行してアプリケーションを開始します：

    ```sh
    ./scripts/start-app.sh
    ```

## 準備の完了について、日本コミュニティ補足

./scripts/start-app.sh を実行または、上記補足の代替の「プログラムの実行コマンド」を実行し、Astro/Svelteの開発サーバが起動し、以下のように http://localhost:4321 にて表示アプリケーションが表示されていれば正常です。

DevContainer、Codespacesを利用する場合、4321ポート以外にポート転送されている可能性があります。ポートの転送リストが、下部パネル中のポートタブにありますので、確認してください。

![](./images/vscodejp_added/first_app_screen.png)

ハンズオン参加までに、ここまで進めておいてください。

もし、うまくいかない場合にはリポジトリのDiscussionにて、状況をお知らせください。

https://github.com/vscodejp/github-samples-pets-workshop-japanese-content/discussions/categories/vs-code-dev-day-tokyo-2025-09-q-a

## 概要と次のステップ

このワークショップで使用するリポジトリをクローンし、IDEのセットアップが完了しました！次に[サーバーに新しいエンドポイントを追加][walkthrough-next]しましょう！


| [← GitHub Copilotの開始][walkthrough-previous] | [次へ: GitHub Copilotでコーディング →][walkthrough-next] |
|:-----------------------------------|------------------------------------------:|

[astro-url]: http://localhost:4321
[dogs-api]: http://localhost:5100/api/dogs
[flask-url]: http://localhost:5100
[fork-repo]: https://docs.github.com/en/get-started/quickstart/fork-a-repo
[required-resources]: ./README.md#required-resources
[required-software]: ./README.md#required-local-installation
[template-repo]: https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository
[walkthrough-previous]: README.md
[walkthrough-next]: ./1-add-endpoint.md
[website-url]: http://localhost:4321
