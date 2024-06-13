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

    CIC は `Auth0Provider` という React コンテキスト機能を提供しています。これをルートコンポーネント (一般的には `<App>`) に登録することにより、ルート配下のコンポーネントから認証情報を呼び出すことができるようになります。

    > 本サンプルアプリでは `RouterProvider` が既に `<App>` に登録されているため、それを囲うように登録しています

    `main.jsx` を開いて、以下のように編集します。

    [変更差分を開く](../assets/diff/2-3-3.html)

    パラメータは以下を指定します。
    * **domain** : https://<テナント名>.cic-demo-platform.auth0app.com
    * **clientId** : `2-2-6` 節で取得した `Client ID`
    * **authorizationParams.redirect_uri** : 認証後に戻される URL (今回は呼び出し元のオリジン `http://localhost:8201` )

    > CIC ドメインと管理ダッシュボードの URL とは異なることにご注意ください

1. **ログイン、ログアウト処理を実装**

    `ログイン` 、`ログアウト` ボタンをクリックすると Okta CIC に連携するような実装を行います。各処理は `useAuth0` というカスタムフックが提供していますので、これをボタンをクリックした時に実行できるようにします。

    `Auth.jsx` を開いて、以下のように編集します。

    [変更差分を開く](../assets/diff/2-3-4.html)

    * `useAuth0` : SDK が提供する React カスタムフック
    * `loginWithRedirect` : CIC のログイン画面に遷移させる
    * `logout` : CIC のログインセッションを終了させる

1. **ログインボタンをクリック**

    `ログイン` ボタンをクリックし、Okta CIC の認証画面 (`Universal Login`) に画面遷移することを確認します。

    ブラウザで `http://localhost:8201` にアクセスし、`ログイン` ボタンをクリックします。

    <img src="../assets/images/cic-handson-2-8.jpg?raw=true" style="max-height: 200px;" />

    Okta CIC のログイン画面が表示されれば成功です。

1. **ユーザのサインアップ**

    この時点では Okta CIC にユーザアカウントが全く存在しないため、ログインすることはできません。ここでは新規ユーザのサインアップを行うため、`Sign up` をクリックします。

    <img src="../assets/images/cic-handson-2-9.jpg?raw=true" style="max-height: 300px;" />

1. **メールアドレス、パスワードの登録**

    新規ユーザの `メールアドレス` 、`パスワード` を登録します。メールアドレスは実在のものでなくてもサインアップは可能ですが、メールを使ったワンタイムパスワード認証ができなくなります。
    入力後、`Continue` をクリックします。

    <img src="../assets/images/cic-handson-2-10.jpg?raw=true" style="max-height: 300px;" />

1. **ユーザ情報利用についての同意確認**

    ユーザプロファイル (名前やメールアドレスなど) を `Okta CIC` から `サンプルアプリ` に提供しても良いかの同意確認画面が表示されます。
    `Accept` をクリックします。

    <img src="../assets/images/cic-handson-2-11.jpg?raw=true" style="max-height: 300px;" />

   クリック後、サンプルアプリの画面に戻ります。一見何の変化も見えませんが、内部的にはログインが完了しています。

1. **ログアウト**

    `ログアウト` ボタンをクリックして、ログアウトを確認します。

    <img src="../assets/images/cic-handson-2-12.jpg?raw=true" style="max-height: 200px;" />

    この処理も一見何の変化も見えませんが、Okta CIC からはログアウトが完了しています。試しに再度 `ログイン` ボタンをクリックした際に認証を求められることを確認します。

1. **認証ステータスによって画面を変更**

    ログイン済みか否かに応じて画面を変更します。現在は常に `ログイン` 、`ログアウト` ボタンが表示されていますが、認証ステータスに応じてどちらかだけを表示するようにプログラムを修正します。

    認証ステータスは `isAuthenticated` プロパティから確認することができますので、`true` であればログアウトボタンを、`false` であればログインボタンだけを表示します。

    `Auth.jsx` を開いて、以下のように編集します。

    [変更差分を開く](../assets/diff/2-3-10.html)

    サンプルアプリを開き、現在の認証ステータスに応じてどちらかのボタンだけが表示されていることを確認します。また、ログイン、ログアウトを実行し、ボタンが変化することを確認します。

    <img src="../assets/images/cic-handson-2-13.jpg?raw=true" style="max-height: 200px;" />

1. **認証ユーザの情報をプロファイルページに表示**

    Okta CIC での認証が成功すると、認証されたユーザについての情報が取得できます。この情報をプロファイル画面に表示できるようにプログラムを追記します。

    ユーザ情報は `user` というプロパティに格納されているため、それをテーブルに書き出します。

    `Profile.jsx` を開いて、以下のように編集します。

    [変更差分を開く](../assets/diff/2-3-11.html)

    ソースコード更新後、サンプルアプリを開き、ログイン済みなことを確認してから `プロファイル` タブを開きます。ユーザ情報 (`nickname` など) が表示されていれば成功です。

    <img src="../assets/images/cic-handson-2-14.jpg?raw=true" style="max-height: 300px;" />

1. **ID Tokenを表示**

    Okta CIC での認証後、サンプルアプリは `ID Token` を取得しています。前項で表示した `user` プロパティも `ID Token` から抽出されたものです。ここでは `ID Token` をサンプルアプリに表示させます。

    `ID Token` は `getIdTokenClaims` メソッドで取得できます。ログインに成功して `isAuthenticated` が `true` になった時に自動的に取得するようにします。

    `Profile.jsx` を開いて、以下のように編集します。

    [変更差分を開く](../assets/diff/2-3-12.html)

    `プロファイル` タブを開き、以下のような画面が表示されていれば成功です。

    <img src="../assets/images/cic-handson-2-15.jpg?raw=true" style="max-height: 300px;" />

    `ID Token` には発行者情報 (`iss`) や有効期限 (`exp`) などの情報が記載されていることが分かります。

以上でサンプルアプリへの Okta CIC への組み込みは完了です。次章では認証の設定を行います。