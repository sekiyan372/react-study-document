# レンダリングの最適化

ここは技術の紹介までとします。

## 最適化の必要性

実際の業務で作成するサイトでは、動作が重かったり動きがもっさりしているとユーザーやクライアントからクレームが入り仕事になりません。

そのため、より実践を想定した開発をするにはレンダリングの動作を理解し、それを最適化してパフォーマンスを改善していくことが必須となってきます。

ここではその方法について紹介します。

## メモ化とは

以下のようなことをすることを`メモ化`と言います。

1. 同じ結果を返す処理について初回のみ処理を実行して記録する
2. 値が必要となった 2 回目以降は、保持していた計算結果を再利用する

メモ化をすると、都度計算する必要がなくなるため**パフォーマンス向上**が期待できます。

## コンポーネントのメモ化

コンポーネントをメモ化すると、親のコンポーネントが再レンダリングしても子のコンポーネントの再レンダリングを防ぐことができます。

コンポーネントのメモ化を実装するには、React が提供している `memo` を使用します。使い方は、以下のようにコンポーネントを memo で囲むだけです。

```typescript
const Component = memo(() => {});
```

このように書き加えるだけでこのコンポーネントは Props に変更がない限り再レンダリングされないようになります。

また、以下のように export 時に記述することもできます。

```typescript
const Component = () => {};

export default memo(Component);
```

## 関数のメモ化

コンポーネント内で定義されている関数は、**再レンダリング等でプログラムが実行されるたびに常に新しい関数が再生成されています**。

これにより、Props で関数を渡したりすると、コンポーネントをメモ化していても再レンダリングが発生してしまうため、関数もメモ化をする必要があります。

関数をメモ化するには `useCallback` という Hook を使用します。useCallback は第 1 引数に関数、第 2 引数に依存配列という useEffect と同じような書き方をします。

```typescript
const handleClick = useCallback(() => {
  console.log("クリックされました");
}, []);
```

上記のようにすると、依存配列は空なので最初に呼び出された時のこの関数が使い回されるようになります。これも useEffect と同じで、依存配列に値があればそれが更新されるごとに新しい関数を再生成するようになります。

どのような時に使うのかやサンプルなどは[React hooks を基礎から理解する (useCallback 編+ React.memo)](https://qiita.com/seira/items/8a170cc950241a8fdb23)を参考にしてみてください。

## 変数のメモ化

関数と同じように、コンポーネント内で定義する変数もメモ化することができます。必要性としては関数の時に説明したことと同じなので省略します。

変数をメモ化するには `useMemo` という Hook を使用します。useMemo も useCallback と同じで第 1 引数に関数、第 2 引数に依存配列という書き方をして、依存配列によって実行タイミングを操作します。

```typescript
const sum = useMemo(() => {
  return 1 + 2;
}, []);
```

どのような時に使うのかやサンプルなどは[React hooks を基礎から理解する (useMemo 編)](https://qiita.com/seira/items/42576765aecc9fa6b2f8)を参考にしてみてください。

## 参考になる記事

[【React】もっと速くなる！？React.memo, useCallBack, useMemo でパフォーマンス最適化に挑戦！](https://qiita.com/seira/items/9e38204758030cd5442a)
