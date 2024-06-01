# 0. CIC テナントの作成

ここでは [demo.okta](https://demo.okta.com) に CIC のテナントを作成します。

1. [demo.okta](https://demo.okta.com) にアクセスする

1. パートナーアカウントでログインする

   ![](pics/00-01.png)  

   アカウント作成時に設定した二要素認証を求められます。
> [!NOTE]
> いい感じ？

3. 以下のコードを作成します

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

1. 以下のようにコードを書き換えます

   ```diff
   - @Post('saml/acs/dummy')
   + @Post('hogehoge')
   + @UseGuard(AuthGuard('jwt'))
   ```
