<!-- toc -->

# Console
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/console.html
```js
const console = require('console');
```

## log
改行でstdoutに出力します。  
また、複数の引数を受け取ることが可能で内部では`util.format()`により処理されます。  
[printf(3)](http://man7.org/linux/man-pages/man3/printf.3.html)と同じように使用できます。  

|パラメータ|型|説明|
|:-|:-|:-|
|...args|Any|出力させるもの|

```js
console.log('piyo');
// piyo
console.log('piyo', 'fuga');
// piyo fuga

const piyo = 1;
console.log('piyo = %d', piyo);
// piyo = 1
```

## info
`console.log`のaliasです。

|パラメータ|型|説明|
|:-|:-|:-|
|...args|Any|出力させるもの|

```js
console.info('piyo');
// piyo
```

## error
改行でstderrに出力します。  
それ以外は[`console.log`](#log)と同じです。 

|パラメータ|型|説明|
|:-|:-|:-|
|...args|Any|出力させるもの|

```js
console.error('Error:', ';(');
// Error: ;(
```

## warn
`console.error`のaliasです。

|パラメータ|型|説明|
|:-|:-|:-|
|...args|Any|出力させるもの|

```js
console.warn('piyo');
// piyo
```

## assert
アサーションテストをし、エラーメッセージは`util.format()`を使用し出力されます。  
falseの場合は、AssertionErrorが投げられます。  
Nodeはブラウザと違い、AssertionErrorが投げられたら処理が中断されます。  
同じ挙動にする場合は`console.assert()`をオーバーライドしてください。  

|パラメータ|型|説明|
|:-|:-|:-|
|value|Boolean|値|
|message|String|メッセージ|
|...args|Any|出力させるもの|

```js
console.assert(true, 'ok');
// undefined
console.assert(false, 'damn');
// AssertionError: damn
//     at Console.assert (console.js:95:23)
//     at repl:1:9
//     at sigintHandlersWrap (vm.js:22:35)
//     at sigintHandlersWrap (vm.js:96:12)
//     at ContextifyScript.Script.runInThisContext (vm.js:21:12)
//     at REPLServer.defaultEval (repl.js:313:29)
//     at bound (domain.js:280:14)
//     at REPLServer.runBound [as eval] (domain.js:293:12)
//     at REPLServer.<anonymous> (repl.js:513:10)
//     at emitOne (events.js:101:20)
```

## trace
stderrに`util.format()`で処理されたメッセージとスタックトレースを出力します。

|パラメータ|型|説明|
|:-|:-|:-|
|...args|Any|出力させるもの|

```js
console.trace('piyo');
// Trace: piyo
//    at repl:1:9
//    at sigintHandlersWrap (vm.js:22:35)
//    at sigintHandlersWrap (vm.js:96:12)
//    at ContextifyScript.Script.runInThisContext (vm.js:21:12)
//    at REPLServer.defaultEval (repl.js:313:29)
//    at bound (domain.js:280:14)
//    at REPLServer.runBound [as eval] (domain.js:293:12)
//    at REPLServer.<anonymous> (repl.js:513:10)
//    at emitOne (events.js:101:20)
//    at REPLServer.emit (events.js:188:7)
```

## dir
第一のobjに対し、`util.inspect()`を使用し結果をstdoutに出力させます。  

|パラメータ|型|説明|
|:-|:-|:-|
|obj|Any|出力させるもの|
|options|Object|console.dirに対してのオプション|
|- showHidden|Boolean|列挙できないプロパティ(シンボル含む)を表示する。デフォルトはfalse|
|- depth|Number|表示するための再帰する回数を指定する。 デフォルトは2、nullは無限|
|- colors|Boolean|ANSIカラーコードで出力する。カスタマイズ可能。デフォルトはfalse|

```js
const obj = {
  1: {
    2: {
      3: {
        4: {
          5: 'piyo'
        }
      }
    }
  }
}

obj.func = function() {};
console.dir(obj, {showHidden: false});
// { '1': { '2': { '3': [Object] } }, func: [Function] }
console.dir(obj, {showHidden: true});
// { '1': { '2': { '3': [Object] } },
//   func:
//    { [Function]
//      [length]: 0,
//      [name]: '',
//      [arguments]: null,
//      [caller]: null,
//      [prototype]: { [constructor]: [Circular] } } }
console.dir(obj, {depth: null});
// { '1': { '2': { '3': { '4': { '5': 'piyo' } } } },
//   func: [Function] }
```

## time
タイマーをスタートさせます。  
固有のラベルで識別され、`timeEnd`との紐付けをします。  
タイマーはサブミリ秒まで正確です。  

|パラメータ|型|説明|
|:-|:-|:-|
|label|Number or String|ラベル|

```js
console.time('my-time');
// undefined
```

## timeEnd
タイマーをストップさせ、結果をstdoutに出力します。  

|パラメータ|型|説明|
|:-|:-|:-|
|label|Number or String|ラベル|

```js
onsole.timeEnd('my-time');
// my-time: 7129.192ms
```
