<!-- toc -->

# Assert
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/assert.html

基本的にstrict系を使いましょう。  
```js
const assert = require('assert');
```

## 一つの値でテスト
### assert
[`assert.ok()`](#ok)のaliasです。  
falseのときにエラーを出します。  

|パラメータ|型|説明|
|:-|:-|:-|
|value|Any|評価する値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert(true);
// undefined
assert(false, 'error;(');
// AssertionError: error;(
//     at repl:1:1
//     at sigintHandlersWrap (vm.js:22:35)
//     at sigintHandlersWrap (vm.js:96:12)
//     at ContextifyScript.Script.runInThisContext (vm.js:21:12)
//     at REPLServer.defaultEval (repl.js:313:29)
//     at bound (domain.js:280:14)
//     at REPLServer.runBound [as eval] (domain.js:293:12)
//     at REPLServer.<anonymous> (repl.js:513:10)
//     at emitOne (events.js:101:20)
//     at REPLServer.emit (events.js:188:7)
```

### ok
valueがtrueかどうかを評価します。  

|パラメータ|型|説明|
|:-|:-|:-|
|value|Any|評価する値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.ok(true); // ok
// undefined
assert(false, 'error;(');
// AssertionError: error;(   // stack traceは省略
```

### ifError
valueがfalseかどうかを評価します。  
コールバックで引数がエラーかどうかをテストするときに便利です。 

|パラメータ|型|説明|
|:-|:-|:-|
|value|Any|評価する値|

```js
assert.ifError(''); // ok
// undefined
assert.ifError(1);
// 1
assert.ifError(new Error(';('));
// Error: ;(
```

## プリミティブ型の比較
### equal
`==`でオペランドを比較し、shallowテストを行います。   
FYI: [MDN/比較演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.equal(1, 1); // ok
// undefined
assert.equal(1, '1'); // ok
// undefined
assert.equal({a:1}, {a:1}); // オブジェクト型なので、参照先が違うからerror
// AssertionError: { a: 1 } == { a: 1 }
assert.equal([], []);
// AssertionError: [] == []
```

### notEqual
`!=`でオペランドを比較し、shallowテストを行います。   

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.notEqual(1, 1);
// AssertionError: 1 != 1
assert.notEqual(1, 20); // ok
// undefined
assert.notEqual([], []); // ok
// undefined
```

### strictEqual
`===`でオペランドを比較し、shallowテストを行います。   

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.strictEqual(1, 1); // ok
// undefined
assert.strictEqual(1, '1');
// AssertionError: 1 === '1'
assert.strictEqual({a:1}, {a:1}); // オブジェクト型なので、参照先が違うからerror
// AssertionError: { a: 1 } == { a: 1 }
assert.strictEqual([], []);
// AssertionError: [] == []
```

### notStrictEqual
`!==`でオペランドを比較し、shallowテストを行います。   

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.notStrictEqual(1, 1);
// AssertionError: 1 !== 1
assert.notStrictEqual(1, '1'); // ok
// undefined
assert.notStrictEqual({a:1}, {a:1}); // ok
// undefined
assert.strictEqual([], []); // ok
// undefined
```

## オブジェクト型での比較
### deepEqual
オブジェクト型に対してdeepテストを行います。  
プリミティブ型の場合は、`==`で比較されます。  

列挙可能な独自プロパティのみ考慮される点に注意してください。  
オブジェクトのプロトタイプ、添付されたシンボル、列挙できないプロパティはテスト外です。  

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.deepEqual({}, {}); // ok
// undefined
assert.deepEqual([], ['2']);
// AssertionError: [] deepEqual [ '2' ]
assert.deepEqual(1, '1'); // ok
// undefined
```

### notDeepEqual
オブジェクト型に対してdeepテストを行います。  
プリミティブ型の場合は、`!=`で比較されます。  

[deepEqual](#deepequal)の逆です。  

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.notDeepEqual({}, {});
// AssertionError: {} notDeepEqual {}
assert.notDeepEqual([], ['2']); // ok
// undefined
assert.notDeepEqual(1, '1');
// AssertionError: 1 notDeepEqual '1'
```

### deepStrictEqual
一般的に`assert.deepEqual()`と同様です。  
違う点として以下の点があります。  
- プリミティブ型の場合、厳密等価演算子`===`で比較されます。
- オブジェクト型の比較ではプロトタイプの厳密な等価確認が行われます。

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.deepStrictEqual({}, {}); // ok
// undefined
assert.deepStrictEqual([], ['2']);
// AssertionError: [] deepEqual [ '2' ]
assert.deepStrictEqual(1, '1');
// AssertionError: 1 deepStrictEqual '1'
```

### notDeepStrictEqual
`assert.deepStrictEqual()`の反対です。  
プリミティブ型の場合は、`!==`で比較されます。

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message(opt)|String|エラーのときに出すメッセージ|

```js
assert.notDeepStrictEqual({}, {});
// AssertionError: {} notDeepStrictEqual {}
assert.notDeepStrictEqual([], ['2']); // ok
// undefined
assert.notDeepStrictEqual(1, '1'); // ok
// undefined
```

## fail
AssertionErrorを投げます。  
messageがfalseの場合、operatorの値がactualとexpectedの期待値として設定されます。

|パラメータ|型|説明|
|:-|:-|:-|
|actual|Any|実際値|
|expected|Any|期待される値|
|message|String|エラーのときに出すメッセージ|
|operator|String|オペレータ|

```js
assert.fail(1, 2, 'piyo', '<');
// AssertionError: piyo
assert.fail(1, 2, '', '<'); // messageがfalse
// AssertionError: 1 < 2
```

## throws
関数内でエラーが投げられることを期待します。  
指定できるメッセージはコンストラクタ、RegExp、バリデーション関数です。  

|パラメータ|型|説明|
|:-|:-|:-|
|block|Function|コードブロック|
|error|Constructor, RegExp, Function|投げられるエラーを検証するもの|
|message|String|エラーのときに出すメッセージ|

```js
assert.throws(() => {
  throw new TypeError('typo');
}, /^TypeError: typo$/); // 投げられたエラーと一致しているので何も出力されない(つまりok)
// undefined
assert.throws(() => { // 投げられる例外がない場合はAssertionErrorが投げられる
}, /^TypeError: typo$/);
// AssertionError: Missing expected exception..
```
## doesNotThrow
関数内でエラーが投げられないことを期待します。
ほかは、`assert.throws()`と同様です。

|パラメータ|型|説明|
|:-|:-|:-|
|block|Function|コードブロック|
|error|Constructor, RegExp, Function|投げられるエラーを検証するもの|
|message|String|エラーのときに出すメッセージ|

```js
assert.doesNotThrow(() => {
  throw new TypeError('typo');
}, /^TypeError: typo$/);
// AssertionError: Got unwanted exception..
assert.doesNotThrow(() => {
}, /^TypeError: typo$/); // ok
// undefined
```
