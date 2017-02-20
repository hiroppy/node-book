<!-- toc -->

# Util
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/util.html

```js
const util = require('util');
```

## inspect
設定することが多くなければ、[`console.dir()`](../console/index.md#dir)を使うことができます。  

|パラメータ|型|説明|
|:-|:-|:-|
|object|Any||
|options|Object||
|- showHidden|Boolean|列挙できないプロパティ(シンボル含む)を表示する。デフォルトはfalse|
|- depth|Number|表示するための再帰する回数を指定する。 デフォルトは2、nullは無限|
|- colors|Boolean|ANSIカラーコードで出力する。カスタマイズ可能。デフォルトはfalse|
|- customInspect|Boolean||
|- showProxy|Boolean||
|- maxArrayLength|Number||
|- breakLength|Number||

## format

## debuglog

## depricate

## inherits
