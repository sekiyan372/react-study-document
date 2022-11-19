# 状態管理の例

## カウンター

[サンプルプログラム](https://github.com/sekiyan372/react-study-sample/blob/main/src/pages/week3/Count.tsx)

このサンプルは、ボタンを押すと表示されている数字が増えるカウンターのアプリケーションです。アプリケーションは以下のような機能を持っています。

- カウンターの値が表示される
- 「+1」を押すとカウンターの値が 1 増える
- 「+10」を押すとカウンターの値が 10 増える

ここでは、カウンターの値を状態として持っています。

```typescript
const [num, setNum] = useState<number>(0);
```

そして、ボタンを押すと onClick イベントで `handleClick` 関数を呼び出しています。

```tsx
<Button onClick={() => handleClick(1)}>
  +1
</Button>

<Button onClick={() => handleClick(10)}>
  +10
</Button>
```

handleClick は数値を引数として、 State を更新する関数を呼び出して State の値と引数の値を加算した値を新たな State として更新します。

```typescript
const handleClick = (value: number) => {
  setNum(num + value);
};
```

そして、State の値を表示しています。

```tsx
<View>count number: {num}</View>
```

サンプルを実行すると、ボタンを押すとすぐに State の値が更新されることを確認できると思います。

カウンタの値はページをリロードするとリセットされます。これにより、State はリロードすると初期化されることを理解してください。

## フォーム

[サンプルプログラム](https://github.com/sekiyan372/react-study-sample/blob/main/src/pages/week3/Form.tsx)

このサンプルは、フォームに値を入力するとリアルタイムで表示する値が切り替わり、送信することでリセットされるようなアプリケーションです。アプリケーションは以下のような機能を持っています。

- フォームに値を入力すると表示される値が切り替わる
- 送信ボタンを押すと、ダイアログが表示されて入力した値がリセットされる

ここでは、フォームで入力した値を状態として持っています。

```typescript
const [view, setView] = useState<string>("");
```

フォームを入力すると onChange イベントによって `handleInput`関数が呼び出されます。

```tsx
<Input type="text" value={view} onChange={(e) => handleInput(e)} />
```

handleInput 関数では State の値を event で発生した値から取り出した入力値に更新しています。

```typescript
const handleInput = (event: ChangeEvent<HTMLInputElement>) => {
  setView(event.target.value);
};
```

送信ボタンを押した時には form の onSubmit イベントにより `handleSubmit` 関数を呼び出します。

```tsx
<form onSubmit={(e) => handleSubmit(e)}>
```

handleSubmit では送信時の処理が記述されています。

```typescript
const handleSubmit = (event: FormEvent<HTMLFormElement>) => {
  event.preventDefault();
  setView("");
  alert("送信されました");
};
```

まず 1 行目では 送信時にページがリロードされることを防ぐことを防いでいます。これは JavaScript 自体の基本になりますが、これについて理解できていない人は[こちらの記事](https://qiita.com/yokoto/items/27c56ebc4b818167ef9e)を参考にしてみてください。

2 行目では、フォームの状態を空の文字列に初期化しています。そして 3 行目でアラートダイアログを表示させています。

2 行目の初期化時に大切なことは、Input の value を State の値に指定していることです。これがなくても form に入力した時の挙動は変わりませんが、リセットするときに form 側に反映されないことをコメントアウトをして確認してみてください。

```tsx
<Input
  ...
  value={view}
  ...
/>
```

このサンプルを通して、State を頻繁に更新する扱いに慣れてください。
