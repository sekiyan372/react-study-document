# 練習問題をやってみよう

演習ではサンプルプログラムを使用します。

## 準備

1. サンプルプログラムの `/src/index.tsx` を開く
2. 4行目と9行目をコメントアウトまたは削除して、もともとコメントアウトされていた5行目と10行目のコメントアウトを外す
```typescript
import React from 'react'
import ReactDOM from 'react-dom'
import '~/index.css'
// import App from '~/App'         //ここをコメントアウトまたは削除
import Router from '~/Router'      //ここのコメントアウトを外す

ReactDOM.render(
  <React.StrictMode>
    {/* <App /> */}                //ここをコメントアウトまたは削除
    <Router />                     //ここのコメントアウトを外す
  </React.StrictMode>,
  document.getElementById('root')
)
```
3. ブラウザを開いて http://localhost:3000/weak1/hello にアクセスする

## 演習問題

問題は `/src/utils/weak1.ts` にあります。問題文に従って回答をしてください。

### 実行方法

1. `/src/pages/weak1/Hello.tsx` のコメントアウトされている import 文を有効にする
2. 作成した関数を import 文に追加する
```typescript
import {
  sample,
  ex1,     //ここを追加
} from '~/utils/weak1'
```
3. App コンポーネント内で関数を実行数する
```typescript
const App: VFC = () => {
  // sample("Hello World!")  //このコメントアウトを外すと例題が実行できます
  ex1("aaa", "bbb")          //ここを追加

  return <h1>Hello World!</h1>
}
```
4. ブラウザのコンソールで実行結果を確認する
