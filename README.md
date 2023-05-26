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
│  style_picture.png
│  
├─.github
│  └─workflows
│          deploy.yml
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


## 手順
1. 新しいGithubリポジトリを作ります。ここでgithub-action-demoというリポジトリを使って説明します。

3.
4.

後で書くわ～～～～
(¦3[▓▓] (¦3[▓▓] (¦3[▓▓] 

![疲れわ!](https://github.com/york-yang-me/github-action-demo/blob/master/style_picture.png)
