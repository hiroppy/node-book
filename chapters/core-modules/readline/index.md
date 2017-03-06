<!-- toc -->

# ReadLine
公式ドキュメント: https://nodejs.org/dist/latest-v7.x/docs/api/readline.html
```js
const readline = require('readline');
```

## createInterface
インターフェイスを作ります。

|パラメータ|型|説明|
|:-|:-|:-|
|options|Object||
|input|Readable|読み込み可能なストリームを指定。必須オプション|

```js
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
  prompt: 'Hi> '
});

```

## event
```js
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
```
入力用のstreamと出力用のstreamの指定が必要です。  
[createInterface](#createinterface)

### line
入力された文字列がコールバックの第一引数に与えられます。

```js
rl.on('line', (line) => {
  console.log(line);
});
```
```sh
> piyo
> piyo # output
```

### close
終了した時に呼び出されます。  
`ctrl + c`が押されたときに呼び出されます。  <!-- [TODO] もっと詳細に -->

```js
rl.on('close', () => {
  console.log('Readline closaed.');
});
```

### resume
入力streamが再開されたときに呼び出されます。

```js
rl.on('resume', () => {
  console.log('Readline resumed.');
});
```

### pause
入力streamが一時停止されたときに呼び出されます。

```js
rl.on('pause', () => {
  console.log('Readline paused.');
});
```

### SIGINT
`ctrl + c`が押されるたびに呼び出されます。  
もし、SIGINTのイベントリスナーが登録されていない場合は`pause`イベントが送られます。

```js
rl.on('SIGINT', () => {
});
```

### SIGTSTP
windowsではサポートされていません。

```js
rl.on('SIGTSTP', () => {
});
```

### SIGCONT
`ctrl + z`でバックエンドへNodeプロセスをされたものを`fg`を使いフォアグラウンドへ戻すと呼び出されます。

```js
rl.on('SIGCONT', () => {
});
```
