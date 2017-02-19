<!-- toc -->

# Globals
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/globals.html  

Node.js固有のグローバルなオブジェクトです。  
これらのオブジェクトはすべてのモジュールで使用することが可能です。  
_一部、モジュールスコープ内にあるものもあります。_

## __filename
現在の実行(モジュール)ファイル名をフルパスで取得します。  
実際はグローバルモジュールではなく、各モジュールに対しローカルです。

```js
console.log(__filename);
// '/Users/Node/globals/index.js'
```

## __dirname
現在のディレクトリ名をフルパスで取得します。  
`require('path').resolve()`, `require('path').dirname(__filename)`と同じです。

```js
console.log(__dirname);
// '/Users/Node/globals'
```

## global
Node.jsではブラウザと異なりトップレベルのスコープがグローバルとなるわけではありません。  
Node.jsではトップレベルで宣言してもそのモジュール(そのファイル)のローカルとなります。  
他のモジュールでも使いたい場合は、`global`の中に入れる必要があります。(またはexportsする)

```js
const piyo = 'piyo';
global.piyo = 'piyo';
```


## console
stdoutとstderrに出力するのに使います。  
参照: [Console](../core-modules/console/index.md)

## process
