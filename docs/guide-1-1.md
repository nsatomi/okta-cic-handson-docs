# 1. CIC テナントの作成

ここでは [demo.okta](https://demo.okta.com) に CIC のテナントを作成します。

1. **[demo.okta](https://demo.okta.com) にアクセス**

1. **`Okta Partners で続ける` をクリック**

    ![1-1](../pics/cic-handson-1-1.jpg?raw=true)  

    事前準備で作成したパートナーアカウントのメールアドレスでログインしてください。なお、アカウント作成時に設定した二要素認証を求められます。

1. **`Demo Builder` をクリック**

    ![1-2](../pics/cic-handson-1-2.jpg?raw=true)

1. **以下のコードを作成します**

    ```javascript
    @Post('saml/acs/dummy')
    @Render('show-assertion')
    // @Header('Content-Type', 'application/xml')
    dummyACS(@Body() body: any) {
        const xml = atob(body.SAMLResponse);
        const parser = new XMLParser({});
        const object = parser.parse(xml);
        return {
            login: object['saml2p:Response']['saml2:Assertion']['saml2:Subject']['saml2:NameID'],
            assertion: new XmlBeautify({parser: DOMParser}).beautify(xml)
            // ...object
        }
    }
    ```

1. **以下のようにコードを書き換えます**

   ```diff
   - @Post('saml/acs/dummy')
   + @Post('hogehoge')
   + @UseGuard(AuthGuard('jwt'))
   ```
