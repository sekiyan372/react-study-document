# Style
[サンプルプログラム](https://github.com/sekiyan372/react-study-sample/blob/main/src/pages/week2/StyledComponents.tsx)

## React と CSS

React で CSS を記述するには様々な方法があります。

- 直書き(Inline Styles): JSX の中で CSS を直接書く書き方
- 外部ファイル(CSS Modules など): CSS ファイルを用意して、JSX のファイルとは別に CSS を記述し、管理する
- CSS in JS: コンポーネントファイルに CSS も記述するやり方
  - Styled JSX
  - styled components
  - Emotion
- フレームワーク: すでにある程度作成されたコンポーネントをカスタマイズして使う
  - Material-UI
  - React-Bootstrap
  - Ant Design
  - Semantic UI React
  - Tailwind CSS

など

今回は特徴的である CSS in JS を採用します。CSS in JS にもさらに様々なライブラリがありますが、その中でも、今回は `styled components` を使用していきます。

この勉強会は React 自体に焦点を当てているので、styled components 以外の CSS のそれぞれの使い方については説明はしません。しかし、ここもとても奥が深いので、ぜひ自分で技術選定をする時はいろいろ調べてみてください！

## styled components

styled components は**スタイルをあてたコンポーネントを定義する**やり方で、実際に企業などでも採用されている技術です。

文章の説明よりも、実際に見た方が早いと思うので、以下のコードをみてください。
```typescript
import styled from 'styled-components'

const Title = styled.div`
  margin: 10px;
  padding: 10px;
  color: red;
  &:hover {
    opacity: 0.5;
  }
`

const Component: VFC = () => {
  return (
    <Title>タイトル</Title>
  )
}
```

このように、`styled.`の後に HTML に存在するタグを指定することでそのタグを拡張した形でスタイルを適用できます。その後ろは必ずバッククォートで囲み、その中にCSSを書いていきましょう。

styled components では SCSS 記法がそのまま使えるのも特徴の一つです。
