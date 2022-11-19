# React の基本

[サンプルプログラム](https://github.com/sekiyan372/react-study-sample/blob/main/src/index.tsx)

ブラウザで React を動作させるには、最低限 `React` と `ReactDOM` という 2 つのライブラリが必要になります。

- React: ビューを構築する
- ReactDOM: React で構築されたビューをブラウザで描画する

## SPA とは？

React の話をするにはまず `SPA (Single Page Application)` について理解しなくてはなりません。

通常の HTML で構成されたサイトでは、画面遷移時にその画面に対応する HTML ファイルを読み込みます。しかし、SPA では HTML ファイルは 1 つしか存在しません。初回に 1 度だけロードがされ、以降は画面遷移のたびに同じ HTML ファイルが部分的に更新されていきます。

## create-react-app

React プロジェクトを開始する最も一般的で簡単な方法が `create-react-app` です。この勉強会のサンプルプログラムもこれを元にして作成しています。

自分で試してみたい人は、以下のコマンドでプロジェクトを作成できます。(yarn 環境、typescript はオプション)

```bash
$ yarn create react-app [アプリケーション名] --template typescript
```

## ブラウザへの描画

サンプルプログラムの `/src/index.tsx` を見てみましょう。

ここでは ReactDOM の `createRoot` 関数を使って要素をぼ描画する場所（ルートノード）を指定し、それに対して `render` 関数を使用して要素を描画しています。（eslint-... と書いてある部分は eslint の設定なので気にしないでください。）

```tsx
import React from "react";
import { createRoot } from "react-dom/client";
import "~/index.css";
import Router from "~/Router";

const container = document.getElementById("root");
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion
const root = createRoot(container!);
root.render(
  <React.StrictMode>
    <Router />
  </React.StrictMode>
);
```

`/public/index.html` を見てみましょう。

注目して欲しいのは、body タグ内の部分です。ここに先程のルートノードを id で指定しています。この div タグ中に全ての要素が描画されていくことになります。

```html
<body>
  <div id="root"></div>
</body>
```
