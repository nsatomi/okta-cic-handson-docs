# 1. CIC テナントの作成

ここでは [demo.okta](https://demo.okta.com) に CIC のテナントを作成します。

1. **[demo.okta](https://demo.okta.com) にアクセス**

1. **`Okta Partners で続ける` をクリック**

    <img src="../pics/cic-handson-1-1.jpg?raw=true" style="max-height: 200px;" />

    > 事前準備で作成したパートナーアカウントのメールアドレスでログインしてください。なお、アカウント作成時に設定した二要素認証を求められます。

1. **demo.okta ログイン後 `Demo Builder` をクリック**

    <img src="../pics/cic-handson-1-2.jpg?raw=true" style="max-height: 400px;" />

1. **`New Demo` をクリック**

    <img src="../pics/cic-handson-1-3.jpg?raw=true" style="max-height: 200px;" />

1. **テナントの情報を入力し、`Create` をクリック**

    * **Purpose**: `Personal Enablement / Accreditation` を選択
    * **Label**: demo.okta での表記名 (分かりやすい任意の名前) を入力
    * **Identity Provider Platform**: `Customer Identity Cloud` を選択
    * **Identity Provider Name**: 任意のテナント名を入力 (テナント URL に影響)

    <img src="../pics/cic-handson-1-4.jpg?raw=true" style="max-height: 400px;" />

1. **ステータスが `Active` になったことを確認し、`Accept Invitation` をクリック**

    <img src="../pics/cic-handson-1-5.jpg?raw=true" style="max-height: 200px;" />

1. **`CONTINUE TO AUTH0` をクリック**

    <img src="../pics/cic-handson-1-6.jpg?raw=true" style="max-height: 200px;" />

1. **`demo.okta SSO で続ける` をクリック**
   
    <img src="../pics/cic-handson-1-7.jpg?raw=true" style="max-height: 200px;" />

1. **`ACCEPT` をクリック**

    <img src="../pics/cic-handson-1-8.jpg?raw=true" style="max-height: 200px;" />

1. **CIC 管理ダッシュボードが表示される**

    <img src="../pics/cic-handson-1-9.jpg?raw=true" style="max-height: 400px;" />

    > ダッシュボードの URL は、`https://manage.cic-demo-platform.auth0app.com/dashboard/pi/<テナント名>/` になります

1. **コード表記**

    ```
    title: ハンズオンガイド
    ```

    ```javascript
    const App = props => {

        // 状態変数 value を定義
        // これをしないと値の更新ができない
        const [value, setValue] = useState(0);

        return (
            <h1>現在の値は {value} です</h1>
        );
    }
    ```