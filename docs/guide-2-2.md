# 2.2 CIC へのアプリケーション登録

ここでは **Okta CIC** に `2-1` でデプロイしたアプリケーションを登録します。これにより連携に必要な `Client ID` などの情報を取得することができます。

1. **CIC 管理ダッシュボードにアクセス**

    `https://manage.cic-demo-platform.auth0app.com/dashboard/pi/<テナント名>/` にアクセスします。

    <img src="../assets/images/cic-handson-1-9.jpg?raw=true" style="max-height: 400px;" />

    > 再ログインを求められた場合は、`パートナーアカウント` でログインします

1. **アプリケーションメニューを開く**

    サイドバーから `Applications` -> `Applications` を開きます。

    <img src="../assets/images/cic-handson-2-2.jpg?raw=true" style="max-height: 200px;" />

1. **`Create Application` をクリック**

    <img src="../assets/images/cic-handson-2-3.jpg?raw=true" style="max-height: 200px;" />

1. **アプリケーション名、種別を設定**

    * **Name**: アプリケーション名を任意に入力します (例: `React SPA Primary` )
    * **application type**: 本セッションでは `Single Page Web Applications` を設定します

    <img src="../assets/images/cic-handson-2-4.jpg?raw=true" style="max-height: 300px;" />

    設定後、`Create` ボタンをクリックします。

1. **`Settings` タブをクリック**

    <img src="../assets/images/cic-handson-2-5.jpg?raw=true" style="max-height: 200px;" />

1. **`Client ID`を記録**

    サンプルアプリケーションとの連携時に `Client ID` が必要になりますので、任意の場所にコピーしておきます。

    <img src="../assets/images/cic-handson-2-6.jpg?raw=true" style="max-height: 200px;" />

1. **各種 `許可 URI` を設定する**

    Okta CIC でのログイン、ログアウト実行後に戻り先のページとして許可するアプリケーションの URL を設定します。本ハンズオンのサンプルアプリケーションでは `http://localhost:8201` のみを利用します。

    * **Allowed Callback URLs**: `http://localhost:8201`
      * ログイン完了後に戻るページの URL
    * **Allowed Logout URLs**: `http://localhost:8201`
      * ログアウト完了後に戻るページの URL
    * **Allowed Web Origins**: `http://localhost:8201`
      * [Silent Authentication](https://auth0.com/docs/authenticate/login/configure-silent-authentication) の実行に必要な Okta CIC へのアクセスを許可する URL

    <img src="../assets/images/cic-handson-2-7.jpg?raw=true" style="max-height: 400px;" />

    最後に画面下部の `Save Changes` をクリックして、設定を保存します。

1. diff テスト

    ```diff
    + import { useAuth0 } from '@auth0/auth0-react';
      unko
    - console.log('ochimai');
    + console.log('hajimari');
    ```

```diff
+ import { useAuth0 } from '@auth0/auth0-react';
  unko
- console.log('ochimai');
+ console.log('hajimari');
```

9. javascript テスト

    ```javascript
    ReactDOM.createRoot(document.getElementById('root')).render(
      <React.StrictMode>
        <Auth0Provider
          domain='https://gray-mule-75111.cic-demo-platform.auth0app.com'
          clientId='mdAoAoHT9Hjo0HGq2MkbIeIKZazvog1B'
          useRefreshTokens
          useRefreshTokensFallback
          authorizationParams={{
            redirect_uri: window.location.origin,
            audience: 'http://localhost:8202',
            scope: 'openid profile email offline_access'
          }}
        >
          <RouterProvider router={router} />
        </Auth0Provider>
      </React.StrictMode>,
    )
    ```
1. hello