<!-- toc -->

# QueryString
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/querystring.html
```js
const querystring = require('querystring');
```

## stringify
クエリオブジェクトを文字列へ直列化します。  

|パラメータ|型|説明|
|:-|:-|:-|
|obj|Object|URLクエリ文字列へシリアライズするクエリオブジェクト|
|sep|String|クエリ文字列を区切る文字。デフォルトは`&`|
|eq|String|クエリ文字列のキーと値を区切る文字列。デフォルトは`=`|
|options|Object||
|- encodeURIComponent|Function|安全でない文字列を%エンコーディングするために使う関数|

```js
const obj = {
  'foo': 'bar',
  'piyo': ['1', 2],
  'empty': ''
};

querystring.stringify(obj);
// 'foo=bar&piyo=1&piyo=2&empty='
querystring.stringify(obj, '||'); // sep = '||'
// foo=bar||piyo=%E3%81%82%E3%81%82||piyo=2||empty=
querystring.stringify(obj, null, '~'); // eq = '||'
// foo~bar&piyo~%E3%81%82%E3%81%82&piyo~2&empty~
```

## parse
クエリ文字列をオブジェクトへ復元します。  

|パラメータ|型|説明|
|:-|:-|:-|
|str|String|URLクエリオブジェクトへ復元するクエリ文字列|
|sep|String|クエリ文字列を区切る文字。デフォルトは`&`|
|eq|String|クエリ文字列のキーと値を区切る文字列。デフォルトは`=`|
|options|Object||
|- encodeURIComponent|Function|安全でない文字列を%エンコーディングするために使う関数|
|- maxKeys|Number|解析するキーの最大数。 デフォルトは1000で0で制限なし|

```js
querystring.parse('foo=bar&piyo=1&piyo=2&empty=');
// { foo: 'bar', piyo: [ '1', '2' ], empty: '' }
```

## escape
`querystring.stringify`で利用されており、通常は利用を期待されてません。  
必要に応じて、オーバーライドするために提供されます。  

|パラメータ|型|説明|
|:-|:-|:-|
|str|String|文字列|

```js
querystring.escape('foo=bar');
// 'foo%3Dbar'
```

## unescape
`querystring.parse`で利用されており、通常は利用を期待されてません。  
デフォルトでは`decodeURIComponent`を使い、デコードを試みます。  
必要に応じて、オーバーライドするために提供されます。

|パラメータ|型|説明|
|:-|:-|:-|
|str|String|文字列|

```js
querystring.unescape('foo%3Dbar');
// 'foo=bar'
```
