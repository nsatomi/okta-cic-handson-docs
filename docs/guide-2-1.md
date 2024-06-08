# 2-1. サンプルアプリのデプロイ

ここでは **Okta CIC** と連携するサンプルアプリをローカル環境にデプロイします。サンプルアプリは `React` フレームワークで実装された非常にシンプルなものです。

1. **アプリケーションのダウンロード**

    ターミナルから任意のディレクトリに移動し、`cic-handson` ディレクトリを作成します。続いて `git clone` コマンドを使って、アプリケーションをダウンロードします。

    ```bash
    > mkdir cic-handson
    > cd cic-handson
    > git clone https://github.com/nsatomi/okta-cic-handson-react-primary.git
    > cd okta-cic-handson-react-primary
    ```

1. **モジュールをインストール**

    `npm install` コマンドで必要なモジュールをインストールします。

    ```bash
    > npm install
    ```

1. **アプリケーションの起動**

    アプリケーションを開発モードで起動します。

    ```bash
    > npm run dev
    ```

    > アプリケーションはポート `8201` を利用します

1. **ブラウザでアプリケーションにアクセス**

    ブラウザで `http://localhost:8201` にアクセスします。下記の画面が表示されれば成功です。

    <img src="../pics/cic-handson-2-1.jpg?raw=true" style="max-height: 200px;" />

1. **アプリケーションの動作確認**

    この時点ではアプリケーションにはほぼ何の機能も実装されていません。

    * `ログイン` 、`ログアウト` ボタンを押しても反応なし
    * ナビゲーションバーの `ホーム` 、`プロファイル` でページ切り替えが可能

1. **アプリケーションのファイル構成**

    ```bash
    ├── README.md
    ├── index.html
    ├── node_modules
    ├── package-lock.json
    ├── package.json
    ├── src
    │   ├── App.jsx
    │   ├── Auth.jsx
    │   ├── assets
    │   │   └── images
    │   │       └── handson.jpg
    │   ├── main.jsx
    │   └── routes
    │       ├── Home.jsx
    │       └── Profile.jsx
    └── vite.config.js
    ```

    本ハンズオンで編集を行うファイルは以下3ファイルのみです。

    * `main.jsx`: アプリケーションのエントリポイント
    * `Auth.jsx`: ログイン、ログアウトを処理するコンポーネント
    * `Profile.jsx`: プロファイルを取得、表示するコンポーネント

    次の章からはこれらのファイルを編集して、このアプリケーションに認証機能を実装していきます。