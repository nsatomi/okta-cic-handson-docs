# 2-3. サンプルアプリへの CIC ライブラリの組み込み

ここではサンプルアプリケーションに Okta CIC のライブラリを組み込み、Okta CIC を介してログイン、ログアウトを実行できるようにします。本サンプルアプリは `React` フレームワークで開発されておりますので、`React` 用の SDK を利用します。

1. **`auth0-react` をインストール**

    `npm install` コマンドを使って `auth0-react` をインストールします。

    ```bash
    > npm install @auth0/auth0-react
    ```

    > アプリケーションが起動中の場合は `Ctr-C` または `q + Enter` でアプリケーションを終了させてから、インストールを実行してください

1. **サンプルアプリケーションを起動**

    ```bash
    > npm run dev
    ```

1. **`Auth0Provider` をルートコンポーネントに登録**

    CIC は `Auth0Provider` という React コンテキスト機能を提供しています。これをルートコンポーネント (一般的には <App>) に登録することにより、ルート配下のコンポーネントから認証情報を呼び出すことができるようになります。

    `main.jsx` を開いて、以下のように編集します。

    [変更差分](../assets/diff/2-3-3.html)

    <details>
    <summary>完成コード</summary>

    ```javascript
    import React from 'react'
    import ReactDOM from 'react-dom/client'
    import App from './App.jsx'
    import { RouterProvider, createBrowserRouter } from 'react-router-dom';
    import Home from './routes/Home.jsx';
    import Profile from './routes/Profile.jsx';
    import { Auth0Provider } from '@auth0/auth0-react';

    const router = createBrowserRouter([
      {
        path: '/',
        element: <App />,
        children: [
          { index: true, element: <Home /> },
          { path: 'profile', element: <Profile /> }
        ]
      },
    ]);

    ReactDOM.createRoot(document.getElementById('root')).render(
      <React.StrictMode>
        <Auth0Provider
          domain='https://<テナント名>.cic-demo-platform.auth0app.com'
          clientId='<クライアント ID>'
          authorizationParams={{
            redirect_uri: window.location.origin
          }}
        >
          <RouterProvider router={router} />
        </Auth0Provider>
      </React.StrictMode>,
    )
    ```
    </details>