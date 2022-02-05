# ルーティング

## React Router

複数のページを持つサイトでは、どのURLにどのページ（コンポーネント）を割り当てるのか、いわゆるルーティングが必要になります。それを実装できるライブラリが React Router になります。

## ルーティング設定

まず、ルーティング設定するには、全体の一番外側の要素に `BrowserRouter` を設定します。

そして、それぞれのページにアクセスがあったときにルーティングを行えるように `Routes` を設定して、その中に `Route` でどの URL にどのページコンポーネントを対応させるのかを設定します。

Route コンポーネントでは、`path` にURLを、`element` に対するページコンポーネントを指定します。

path では、ルートは `/` に設定します。設定していないパスにアクセスされた場合には `*` を設定することでその場合に表示するページ (404ページ) を設定できます。

`Routes` の外側に要素を置くと、全ページで共通して表示される要素を設定することができます（header や footer に使えますね）。

```typescript
import ReactDOM from 'react-dom'
import { BrowserRouter, Routes, Route } from 'react-router-dom'

ReactDOM.render(
  <BrowserRouter>
    <h1>Hello React Router v6</h1>
    <Routes>
      <Route path="/" element={<Top />} />
      <Route path="/about" element={<About />} />
      <Route path="/contact" element={<Contact />} />
      <Route path="*" element={<NotFound> />} />
    </Routes>
  </BrowserRouter>,
  document.getElementById('root')
)
```

## より複雑なルーティング

動的なルーティングなど、より高度なルーティングも React Router では設定できます。それらの機能を知りたい人は以下のサイトを参考にすることがおすすめです。

- [React Router 公式](https://reactrouter.com/)
- [React Router v6 はじめでもわかるルーティングの設定方法の基礎](https://reffect.co.jp/react/react-router-6)

ここでしっかり説明しないのには理由があります。それは、動的ルーティングなどを必要とするサイトを作成する場合は `Next.js` などのフレームワークを使用することがほとんどだからです。

そして、Next.js には React Router を設定しなくても使用できるようになっています。高度なルーティングを使用する時はそちらを学んでしまった方が早いので、ここでは割愛します。
