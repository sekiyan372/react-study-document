# Props

[サンプルプログラム](https://github.com/sekiyan372/react-study-sample/blob/main/src/pages/week2/PropsSample.tsx)

## Props とは？

Props はコンポーネントに渡す引数のようなもので、コンポーネントは受け取った Props に応じて表示する内容を変化させます。

Props を使うことでコンポーネントを動的に使うことができので、コンポーネントに汎用性を持たせることができます。逆に言えば、この Props がなければコンポーネントに分ける意味はほぼなくなってしまうでしょう。

## Props の使い方

TypeScript ではまず Props の型を宣言します。

```typescript
type Props = {
  ja: string;
  en: string;
};
```

VFC 型では `<型名>` をつけることで宣言した型を使用することができます（ここで勘が鋭い人は気づいたかもしれませんが、これが week1 で学んだ Generics の使い方の一つです！）。

そして、引数には props を渡すと、JSX の中で `props.名前` とすることで型宣言した値を使用することができます。

```tsx
export const Child: FC<Props> = (props) => {
  return (
    <div>
      <p>日本語: {props.ja}</p>
      <p>英語: {props.en}</p>
    </div>
  );
};
```

もしくは、引数に `{}` で囲んでそれぞれの値を展開して宣言することもできます。

```tsx
export const Child: VFC<Props> = ({ ja, en }) => {
  return (
    <div>
      <p>日本語: {ja}</p>
      <p>英語: {en}</p>
    </div>
  );
};
```

そして使用する親コンポーネントでは、子コンポーネントを宣言する時に Props を渡します。

```tsx
import { Child } from "パス名";

const Parent: FC = () => {
  return (
    <>
      <Child ja="こんにちは" en="Hello" />
    </>
  );
};
```

## children

Props には任意の名称を設定してきましたが、それ以外に特別な Props が children です。コンポーネントでも通常の HTML タグのように要素を囲って使用することができます。この囲まれた部分が children として Props に設定されます。

子コンポーネントでは通常の Props と同じように children を受け取ります。

```tsx
const Child = ({ children }) => {
  return <div>{children}</div>;
};
```

親コンポーネントでは、HTML のようにタグの中に children として渡す値を入れます。

```tsx
const Parent = () => {
  return (
    <>
      <Child>こんにちは</Child>
    </>
  );
};
```

## children の型

`FCはデフォルトでは children を含まない` ため、自分で `React.ReactNode` という型で children を使用する際は定義してあげる必要があります。

```tsx
const Child: FC = ({ children }) => <div>{children}</div>; //×

//このようにして children を宣言する
type Props = {
  children: React.ReactNode;
};
const Child: VFC<Props> = ({ children }) => <div>{children}</div>;
```
