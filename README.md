# github-action-demo
github action test
プログラミング方法論T2 プロポーザル (バージョン管理システムとDevOps) - github action demo です。
- サポーター：T2メンバー全員　`☕☕☕`
- デモ作者：york-yang 　`☕☕☕`
- デモ概要：Github actionでReactプロジェクトを構築し、GitHub Pagesに公開します。


## GitHub Actions 定義
GitHub Actionsは、ビルド、テスト、デプロイのパイプラインを自動化できる継続的インテグレーションと継続的デリバリー (CI/CD) のプラットフォームです。

## 目次
```
github-action-demo:
│  .gitignore
│  list.txt
│  package-lock.json
│  package.json
│  ReactREADME.md
│  README.md
│  
├─.github
│  └─workflows
│          deploy.yml
│          
├─img
│      action logs.png
│      actions workflow.png
│      failed action logs.png
│      github page link.png
│      new repository.png
│      personal access token.png
│      style_picture.png
│      token binding.png
│      token copy.png
│      token setting.jpg
│      web .png
│          
├─public
│      favicon.ico
│      index.html
│      logo192.png
│      logo512.png
│      manifest.json
│      robots.txt
│      
└─src
        App.css
        App.js
        App.test.js
        index.css
        index.js
        logo.svg
        reportWebVitals.js
        setupTests.js
```

## 主要なファイルの説明
1. ./githu/workflows/deploy.yml

   GitHub Actionsの設定ファイルはワークフローファイルと呼ばれ、コードリポジトリの **.github/workflows** ディレクトリに保存されています。

   ワークフローファイルはYAMLの形で、好きな名前をつけることができますが、.ymlサフィックスが必要です。`eg. deploy.yml`リポジトリにも複数のワークフローファイルを持つことができます。

   GitHubは **.github/workflows** に.ymlファイルを見つけると自動的に実行します。

2. public

   アイコンとか画像とか静的なウェブファイル（static files）を保存します。
   - index.html デフォルトウェブ画面
   - manifest.json　アイコンやUI等に関する設定の配置ファイル
   - robots.txt　収集されたくないコンテンツをクロールされないように制御するファイル
   
3. src
   
   ウェブ画面に関する動作ファイル(.js)、スタイルファイル(.css)を保存する場所です。

4. package.json
    
   Node.jsにおいてインストールするパッケージが記述されたファイルです。

5. img
   
   READMEに関するテスト画像です。


## 手順
1. 新しいGithubリポジトリを作ります。ここでgithub-action-demoというリポジトリを使って説明します。

  ![new pages](https://github.com/york-yang-me/github-action-demo/blob/master/img/new%20repository.png)
  
2. 個人用アクセス トークンを作成します。GitHub actionをリソースに自動的にアクセスするため、個人アカウントのセッティン画面で`Personal access tokens`を作ります。
   リンクはこちらへ：https://github.com/settings/tokens

  ![token](https://github.com/york-yang-me/github-action-demo/blob/master/img/personal%20access%20token.png)

  ![token setting](https://github.com/york-yang-me/github-action-demo/blob/master/img/token%20setting.jpg)

3. 指定されたリポジトリにトークンを保存します。リポジトリの`Settings/Secrets`にコピーします。

  ![token copy](https://github.com/york-yang-me/github-action-demo/blob/master/img/token%20copy.png)

  ![token binding](https://github.com/york-yang-me/github-action-demo/blob/master/img/token%20binding.png)

4. 個人PCで`create-react-app`を利用して、新規プロジェクトを構築します。`npx`コマンドを利用すれば、`npm`パッケージの「ダウンロード」と「実行」をまとめて行なってくれます。
   ```node.js
   npx create-react-app github-action-demo
   cd github-action-demo
   ```
   作業環境は以下の通りです：
   ```shell
   >> node -v
   v14.17.0
   >> npm -v
   6.14.13
   ```

5. `package.json`ファイルを開き、アプリケーションが公開されるルートディレクトリ(root directory)を示す`homepage`フィールドを追加します。
   ```
   "homepage": "https://[username].github.io/github-actions-demo",
   ```
   [username]は自分のGithubアカウント名を変更してください。

6. Github action workflowの作成します。リポジトリの`Actions`画面へ移動し、actionに関するワークフローを作ります。

   ![workflow](https://github.com/york-yang-me/github-action-demo/blob/master/img/actions%20workflow.png)

   - ここで他人が作た設定ファイルを利用します。[JamesIves/github-pages-deploy-action](https://github.com/marketplace/actions/deploy-to-github-pages)を使います。
 　
   - このアクションは、そのままコピーできるサンプルワークフローファイルを提供しています（[ソースコード](https://github.com/ruanyf/github-actions-demo/blob/master/.github/workflows/ci.yml)）。
   
   <details><summary>ここに参照の例があります。</summary>     
   <p>
           
   ```yml
        name: GitHub Actions Build and Deploy Demo
        on:
          push:
            branches:
              - master
        jobs:
          build-and-deploy:
            runs-on: ubuntu-latest
            steps:
              - name: Checkout 🛎️
                uses: actions/checkout@v2.3.1
                with:
                  persist-credentials: false

              - name: Install and Build 🔧
                run: |
                  npm install
                  npm run-script build

              - name: Deploy 🚀
                uses: JamesIves/github-pages-deploy-action@4.1.1
                with:
                  branch: gh-pages
                  folder: build
                  token: ${{ secrets.ACCESS_TOKEN }}   
   ```
           
   </p>
   </details>
   
   念のため、このワークフローの機能も簡単に説明します。
   - `master`ブランチで`push`イベントが発生すると、すべてのプロセスがトリガーされます。
   - `job`は1つだけで、仮想マシン環境`ubuntu-latest`上で実行します。
   - `action/checkout`というアクションを使って、ソースコードを取得します。
   - `npm`をインストールして、プロジェクトの環境(`build`)を構築します。
   - `JamesIves/github-pages-deploy-action`というアクションを使用して、デプロイを行います。
   - GitHubキー、リリースブランチ、構築環境が置かれるディレクトリ(`build`)という3つの環境変数が必要です。 
    
7. ローカルのリポジトリ`github-action-demo`をGithubに指定されたリポジトリ`[username]/github-action-demo`を`push`します。
   
   GitHubはワークフローファイルが見つかれば自動的に実行します。ログはウェブサイトでリアルタイムに見えます。
   
   ![action logs](https://github.com/york-yang-me/github-action-demo/blob/master/img/action%20logs.png)
   
   もしActionsを実行失敗したら、問題が発生したところもチェックできます。
   
   ![failed action logs](https://github.com/york-yang-me/github-action-demo/blob/master/img/failed%20action%20logs.png)
8. Github pagesでウェブ画面を公開します。

   まずはデプロイしたい分枝を指定します。リポジトリのセッティング画面で`pages`をクリックし、生成した`gh-pages`分枝を指定します。
    ![github pages link](https://github.com/york-yang-me/github-action-demo/blob/master/img/github%20page%20link.png)
   その後、`https://[username].github.io/github-action-demo/`をアクセスして、ウェブ画面をアクセスできます。
   ![web page](https://github.com/york-yang-me/github-action-demo/blob/master/img/web%20.png)
   

終わり(¦3[▓▓] (¦3[▓▓] (¦3[▓▓] 

![疲れわ!](https://github.com/york-yang-me/github-action-demo/blob/master/img/style_picture.png)
