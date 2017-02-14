<!-- toc -->

# Path
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/path.html  
ここでは、POSIXメインで書いていきます。
```js
const path = require('path');
```

## sep
各プラットフォーム固有のパスセグメント区切り文字を提供します。
```js
path.sep;
// '/'
// windowsの場合は '\\'
'foo/bar/piyo.js'.split(path.sep);
// [ 'foo', 'bar', 'piyo.js' ]
```

## delimiter
各プラットフォーム固有のパス区切り文字を提供します。  
```js
path.delimiter;
// ':'
console.log(process.env.PATH);
// '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'
process.env.PATH.split(path.delimiter)
// ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']
```

## posix
posix固有実装のアクセスを提供します。  
```js
path.posix
// Object
```
## win32
windows固有実装のアクセスを提供します。  
```js
path.win32
// Object
```

---

## basename
ディレクトリのパスを抜いたファイル名を取得する。  
第二引数に拡張子を指定することにより、その拡張子を除くことができる。  

|パラメータ|型|説明|
|:-|:-|:-|
|path|String|ファイルパス|
|ext(opt)|String|拡張子|

```js
path.basename('/foo/bar/piyo.js');
// 'piyo.js'
path.basename('/foo/bar/piyo.js', 'js');
// 'piyo'
```

## dirname
path.basenameとは反対に、ディレクトリのパスからファイル名を抜いたパスを取得します。  

|パラメータ|型|説明|
|:-|:-|:-|
|path|String|ファイルパス|

```js
path.dirname('/foo/bar/piyo.js');
// '/foo/bar'
```

## extname
そのファイルの拡張子を取得します。  
ない場合は空文字を返します。  

|パラメータ|型|説明|
|:-|:-|:-|
|path|String|ファイルパス|

```js
path.extname('/foo/bar/piyo.js');
// '.js'
path.extname('piyo.js.x');
// '.x'
```

## format
整形されたファイルパスを生成します。

以下の点に注意してください。
- dirが指定されている時、rootは無視されます
- baseが指定されている時、nameとextは無視されます

|パラメータ|型|説明|
|:-|:-|:-|
|pathObject|Object||
|- dir|String|ディレクトリ名|
|- root|String|基底パス|
|- base|String|ファイル名(拡張子含む)|
|- name|String|ファイル名(拡張子含まない)|
|- ext|String|拡張子|

パラメータ定義
```
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
└──────┴──────────────┴──────┴─────┘
```

```js
path.format({
  dir: '/foo/bar',
  root: '/ignored', // dirが指定されているので無視される
  base: 'piyo.js'
});
// '/foo/bar/piyo.js'

path.format({
  ext: 'ignored', // baseが指定されているので無視される
  root: '/',
  base: 'piyo.txt'
});
// '/piyo.txt'

path.format({
  ext: '.js',
  root: '/',
  name: 'piyo'
});
// '/piyo.js'
```

## parse
formatとは反対に、整形されたファイルパスを分解します。  

|パラメータ|型|説明|
|:-|:-|:-|
|path|String|ファイルパス|

```js
path.parse('piyo.js');
// {
//   root: '',
//   dir: '',
//   base: 'piyo.js',
//   ext: '.js',
//   name: 'piyo'
// }
path.parse('/foo/bar/piyo.js');
// {
//   root: '/',
//   dir: '/foo/bar',
//   base: 'piyo.js',
//   ext: '.js',
//   name: 'piyo'
// }
```

## join
与えられたパスをすべて結合し正規化したパスを取得します。  
結合のデリミタはプラットフォームに依存します。  
引数が空の場合は`.`を返します。  

|パラメータ|型|説明|
|:-|:-|:-|
|...paths|String|ファイルパス|

```js
path.join('foo', '/bar', 'piyo.js');
// 'foo/bar/piyo.js'
path.join('foo', '/bar', 'piyo.js', '..');
// 'foo/bar'
```

## normalize
与えられたパスの`..`, '.'セグメントの解決を行います。  
引数が空の場合は`.`を返します。  

|パラメータ|型|説明|
|:-|:-|:-|
|path|String|ファイルパス|

```js
path.normalize('/foo/bar/../bar/piyo.js');
// '/foo/bar/piyo.js'
```

## resolve
与えられたパス、またはパスセグメントを絶対パスへ変換します。  
引数が空の場合は現在の作業ディレクトリの絶対パスを返します。  

|パラメータ|型|説明|
|:-|:-|:-|
|...paths|String|ファイルパス|

```js
path.resolve('/foo/bar', 'piyo.js');
// '/foo/bar/piyo.js'
path.resolve('foo/bar', 'piyo.js');
// '/Users/about_hiroppy/foo/bar/piyo.js'
```

## relative
resolveとは反対に、与えられたfromからtoへの相対パスを返します。

|パラメータ|型|説明|
|:-|:-|:-|
|from|String|基準となるディレクトリ|
|to|String|目的となるディレクトリ|

```js
path.relative('/foo/bar/piyo.js', '/foo/hoge');
// '../../hoge'
```

## isAbsolute
与えられたパスが絶対パスになっているかどうかを判断します。

|パラメータ|型|説明|
|:-|:-|:-|
|path|String|ファイルパス|

```js
path.isAbsolute('/foo/bar');
// true
path.isAbsolute('./foo/bar');
// false
```
