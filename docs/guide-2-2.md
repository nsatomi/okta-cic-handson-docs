# 2.2 CIC へのアプリケーション登録

ここでは **Okta CIC** に `2-1` でデプロイしたアプリケーションを登録します。これにより連携に必要な `Client ID` などの情報を取得することができます。

1. **CIC 管理ダッシュボードにアクセス**

    `https://manage.cic-demo-platform.auth0app.com/dashboard/pi/<テナント名>/` にアクセスします。

    <img src="../pics/cic-handson-1-9.jpg?raw=true" style="max-height: 400px;" />

    > 再ログインを求められた場合は、`パートナーアカウント` でログインします

1. **アプリケーションメニューを開く**

    サイドバーから `Applications` -> `Applications` を開きます。

    <img src="../pics/cic-handson-2-2.jpg?raw=true" style="max-height: 200px;" />

1. **`Create Application` をクリック**

    <img src="../pics/cic-handson-2-3.jpg?raw=true" style="max-height: 200px;" />

1. **アプリケーション名、種別を設定**

    * **Name**: アプリケーション名を任意に入力します (例: `React SPA Primary` )
    * **application type**: 本セッションでは `Single Page Web Applications` を設定します

    <img src="../pics/cic-handson-2-4.jpg?raw=true" style="max-height: 300px;" />

    設定後、`Create` ボタンをクリックします。

1. **`Settings` タブをクリック**

    <img src="../pics/cic-handson-2-5.jpg?raw=true" style="max-height: 200px;" />