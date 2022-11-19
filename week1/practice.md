# 練習問題をやってみよう

演習ではサンプルプログラムを使用します。

## 準備

1. サンプルプログラムの `/src/Router.tsx` を開く
2. 3 行目と 29 行目をコメントアウトまたは削除してする

```tsx
import React, { FC } from 'react'
import { BrowserRouter, Routes, Route } from 'react-router-dom'
import App from '~/App' //ここをコメントアウトまたは削除

...

const Router: FC = () => (
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />} /> //ここをコメントアウトまたは削除

      ...

    </Routes>
  </BrowserRouter>
)
```

3. 以下のコマンドでサーバーを起動

```bash
$ yarn start
```

4. ブラウザを開いて http://localhost:3000/week1/hello/ にアクセスする

## 演習問題

問題は `/src/utils/week1.ts` にあります。問題文に従って回答をしてください。

### 実行方法

1. `/src/pages/week1/Hello.tsx` のコメントアウトされている import 文を有効にする
2. 作成した関数を import 文に追加する

```typescript
import {
  sample,
  ex1, //ここを追加
} from "~/utils/week1";
```

3. App コンポーネント内で関数を実行数する

```tsx
const App: FC = () => {
  // sample("Hello World!")  //このコメントアウトを外すと例題が実行できます
  ex1("aaa", "bbb"); //ここを追加

  return <h1>Hello World!</h1>;
};
```

4. ブラウザのコンソールで実行結果を確認する
