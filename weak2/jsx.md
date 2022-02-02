# JSX 記法

## JSX 記法とは？

JS (TS) ファイルの中で HTML のようなタグを書く記法です。

## JSX のルール

### return 以降は一つのタグで囲う

return で返せる要素は1つまでです。return以降で複数の要素を返す場合は、一つのタグで囲いましょう。

```typescript
//OK
return <h1>Title</h1>

//NG
return (
  <h1>Title</h1>
  <h2>Sub Title</h2>
)

//OK
return (
  <div>
    <h1>Title</h1>
    <h2>Sub Title</h2>
  </div>
)
```

また、div などの要素ではなく `Fragment` でも記述可能です。Fragment での書き方は２種類あります。

```typescript
return (
  <Fragment>
    <h1>Title</h1>
    <h2>Sub Title</h2>
  </Fragment>
)

//または

return (
  <>
    <h1>Title</h1>
    <h2>Sub Title</h2>
  </>
)
```

### className プロパティ

HTMLで使用できる class は JavaScript では予約語であるため使用できません。その代わりに、JSX では `className` を使用します。

```typescript
<h1 className="title">Title</h1>
```

### JavaScript 式

JSX では JS (TS) の式を HTML の中で扱うようなことができます。JSX 内で記述する場合は `{}` で囲います。

```typescript
//このような変数があったとして
const hello = "こんにちは"
const numbers = [0, 1, 2, 3, 4]

//このように記述できます
<div>{ hello }</div>

//より複雑にしても大丈夫です (これはよく使う記法なので覚えておきましょう)
<ul>
  {numbers.map(num => (
    <li key={ num }>{ num }</li>
  ))}
</ul>
```
