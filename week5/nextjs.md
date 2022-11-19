# Next.js の機能説明

ここでは `Next.js` の主要機能とよく使うものについて説明します。

## 全体の構成

### \_app.tsx

Next.js では App コンポーネントを使用して全てのページを初期化するようになっています。 そのため、このコンポーネントを継承したクラスがあるファイル、`_app.js(tsx)` を作成することでデフォルトの App コンポーネントを上書きできます。

つまり、 全ページで必要な処理をここに書くことができます。他にも App コンポーネントでは以下のようなことができます。

App コンポーネントでできることには以下のような例があります。

- ページ間共通のレイアウト(ヘッダーやフッターなど)
- 共通の state を持たせる(バケツリレー)
- グローバルな CSS の設定
- Provider の設定(グローバル State)

以下は week6 で使うブログの \_app.tsx です。

```tsx
import "~/globals.css";
import { NextPage } from "next";
import type { AppProps } from "next/app";
import Footer from "~/components/Footer";

const MyApp: NextPage<AppProps> = ({ Component, pageProps }) => {
  return (
    <>
      <main>
        <Component {...pageProps} />
      </main>
      <Footer />
    </>
  );
};

export default MyApp;
```

今後作成される全てのページコンポーネントは Component に渡されます。

### \_document.tsx

Next.js の Page コンポーネントはデフォルトでは<html>・<body>タグの定義を行いますが、それらを拡張したい場合は `_documet.js(tsx)` を作成し、その中で Document コンポーネントを継承したクラスを実装します。なので、\_document.js(tsx)は必ず必要ではありませんが、必要があれば定義するようにしましょう。

**\_document.js(tsx) だけは class コンポーネントで記述しないといけないことに注意してください。**

以下は week6 で使うブログの \_document.tsx です。

```tsx
import Document, {
  DocumentContext,
  Html,
  Head,
  Main,
  NextScript,
} from "next/document";
import { ServerStyleSheet } from "styled-components";

export default class MyDocument extends Document {
  //中略

  render() {
    return (
      <Html lang="ja">
        <Head />
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}
```

next/document には専用の要素が用意されており、それらを import して使用します。先程説明した \_app.tsx が `NextScript` に反映されます。

省略している部分については、Next.js で styled-components を使用するための設定なので気にしなくて大丈夫です(興味がある人は[Next.js で styled-components を使うときに最初に設定しておくこと【完全版】](https://zenn.dev/nbr41to/articles/c0c691653e3d55)を見てください)。

## ルーティング

Next.js は pages ディレクトリ以下のファイル構成に従って自動的にルーティングが設定されます。そして、ファイルの中でも特別な扱いが `index.tsx` です。これを各ディレクトリに配置すると、そこのルートページとしてルーティングが設定されるようになっています。

もし、ファイルがない url にアクセスした場合は 404 エラーになります。

以下は week6 で使うブログの初期状態のディレクトリ構成です。

```
pages
  |-blog
  |  |-index.tsx
  |-about.tsx
  |-index.tsx
```

サイトにアクセスすると pages の直下にある index.tsx が呼び出されます。

`/about`にアクセスすると pages の下にある about.tsx が呼び出されます。

そして`/blog`にアクセスすると blog ディレクトリの下にある index.tsx が呼び出されます。

### ダイナミックルーティング

ダイナミックルーティングとはブログの各記事のページのように、コンテンツなどに合わせて動的に生成されるルーティングのことです。

Next.js では `[id].js(tsx)` という形式でファイルを作成すると、それが第ナミックルーティング用のファイルとして認識されます。`[]` の中に入る値は自分で設定できます。

ダイナミックルート用のファイルでは、`getStaticPaths` と `getStaticProps` の関数が必要です。`getStaticProps` ついては後述する内容を見てください。

### getStaticPaths

ビルド時にレンダリングする必要のあるパスのリストを生成します。

以下では、取得してきたデータの id を文字列方にして、`paths` という生成する path の値の配列に格納されます。この配列を元にしてルーティングが生成されます。

```typescript
export const getStaticPaths = async () => {
  // 外部APIエンドポイントを呼び出しデータ取得
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // 事前ビルドしたいパスを指定
  const paths = posts.map((post) => ({
    params: {
      // ファイル名と合わせる ※文字列指定
      id: post.id.toString(),
    },
  }));
  // paths：事前ビルドするパス対象を指定するパラメータ
  // fallback：事前ビルドしたパス以外にアクセスしたときのパラメータ true:カスタム404Pageを表示 false:404pageを表示
  return { paths, fallback: false };
};
```

### next/link

Next.js では内部リンク用のコンポーネントが `next/link` として用意されています。

`next/link` は Props である `href` で、パス＋クエリ文字列を渡すことでその遷移先へ移動します。この Props は必須となっています。

```typescript
import Link from "next/link";

<Link href="/about">
  <a>こちら</a>
</Link>;
```

その他にも `next/link` には設定できる Props があるので、詳細は[ドキュメント](https://nextjs-ja-translation-docs.vercel.app/docs/api-reference/next/link)を参照してください。

## next/image

next/image とは画像サイズと拡張子をデバイスとブラウザに応じて最適な形で出し分けてくれる React コンポーネントです。

面倒な画像の最適化を行ってくれるコンポーネントになっているので、Next.js で画像を使用する時は HTML の img タグではなく next/image を積極的に使いましょう。

設定できる Props は HTML の img タグと似ていますが、固有の幅と高さを設定できます（これは単位を持たない値であり、比率のようなものです。実際の値は最適化されます。）

```tsx
import Image from "next/image";

<Image src="/me.png" alt="Picture of the author" width={500} height={500} />;
```

その他にも `next/image` には設定できる Props があるので、詳細は[ドキュメント](https://nextjs-ja-translation-docs.vercel.app/docs/api-reference/next/image)を参照してください。

また、`next/image` について詳細に知りたい人は[Next.js 10 の新機能 next/image のオプション全部触ってみる](https://www.forcia.com/blog/001561.html)を参考にしてみてください。

## SSG

### getStaticProps

ビルド時に静的なファイルを生成し、ページコンポーネントで使用する値を用意します。外部からデータを取得する必要がある場合は `getStaticProps` 関数を作成して、そこで処理を行います。

```typescript
const Blog = ({ posts }) => {
  // Render data...
};

export const getStaticProps = async () => {
  // posts を取得するため外部 API endpoint を読み込む
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // { props: { posts } }を返すことで、
  // Blog コンポーネントはビルド時に`posts`を prop として受け取る
  return {
    props: {
      posts,
    },
  };
};

export default Blog;
```

この例のように、取得したデータを return で返すと、それを Props として受け取ることができます。

## SSR

### getServerSideProps

リクエストごとに静的なファイルを生成し、ページコンポーネントで使用する値を用意します。外部からデータを取得する必要がある場合は `getServerSideProps` 関数を作成して、そこで処理を行います

```typescript
const Page = ({ data }) => {
  // Render data...
};

// すべてのリクエストの度に実行される
export const getServerSideProps = async () => {
  // 外部APIからデータフェッチ
  const res = await fetch(`https://.../data`);
  const data = await res.json();

  // props を通じて Page に data を渡す
  return { props: { data } };
};

export default Page;
```

使い方は getStaticProps とほぼ同じです。違いは getServerSideProps はビルド時ではなくてすべてのリクエストの度に実行されるということです。

## ISR

### getStaticProps

Next.js で ISR を実装するには、ISR をしたいページのコンポーネントで `getStaticProps` の返り値に `revalidate` を含めるだけです。

```typescript
export const getStaticProps: GetStaticProps<Props> = async () => {
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  return {
    props: {
      posts,
    },
    revalidate: 10, // 👈 ポイント
  };
};
```

このようにすると、キャッシュが作られた後 10 秒間はそのキャッシュを返し、10 秒経ったあとはキャッシュが古くなったとみなされる。ただし次のリクエストでも一旦はそのキャッシュを返し、その裏でキャッシュが再生成されて、次のリクエストでは再生成されたキャッシュを返します。

### getStaticPaths

ISR でダイナミックルーティングを使用する場合は `getStaticPaths` を以下のように記述します。

```typescript
export const getStaticPaths: GetStaticPaths = async () => {
  return {
    paths: [], // アプリのビルド時にはパスに何が入るかが分からないので空でOK
    fallback: "blocking", // 👈 ポイント
  };
};
```

`fallback: 'blocking'` は、ざっくりというと**キャッシュがまだ作られていないときは SSR を行う**という指定になります。指定しなかった場合、初回リクエスト（キャッシュ未生成時）には SPA のような動きになります。TwitterBot などのクローラーが動的に生成されたコンテンツの中身を読めるようにするために `fallback: 'blocking'` を指定しておいた方が良いと思います。
