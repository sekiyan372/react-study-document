# TypeScript の紹介

## TypeScript とは？

簡単に言うと `型のある JavaScript` であり、コンパイル時に JS に変換します。
基本はほとんど JavaScript の書き方のままで記述することができます。

## どうしてわざわざ型をつけるの？

JavaScipt は動的型付け言語であり、基本的に型を指定して記述することはありません。
しかし、変数や関数で意図しない型が使われることでエラーが出ることもあり、特に大規模開発では問題になってきました。
そこで型を定義して記述することで、コンパイル時に未然にエラーに気付くことができようになっています。

また、型を記述することでどのようなコードなのかがわかりやすくなります。
よく型付けはドキュメントになるみたいな言い方もされますね。

## 型推論

TypeScript では型推論という、自動で型を予測する機能があるので、全てに型を記述せずともある程度予測してくれます。
なので、一般的には明らかに宣言しなくてもわかる場面では型を指定しないことも多いですが、必要な場面では自分で型を決めるようにしましょう。

また、動的片付けと何が違うの？と思うかもしれませんのでそれぞれの違いをまとめておきます。

- 型推論: コンパイルのタイミングで型が決定され、その型が変更されることはない

```typescript
let x = 1; //xはnumber型となる
x = "hello"; //xはnumber型と決定しているのでstring型を代入するとエラー
console.log(x.substring(1, 3));

//エラーになる
```

- 動的型付け: 実行時に型が決まるので、実行タイミングにより型が変化する

```javascript
let x = 1; //xはnumber型となる
x = "hello"; //xはstring型となる
console.log(x.substring(1, 3));

//el
```

## 基本的な型の種類

| 型       | 種類                   | 補足                                 |
| -------- | ---------------------- | ------------------------------------ |
| string   | 文字列                 |
| number   | 数値                   |                                      |
| boolean  | 真偽値 (true, false)   |                                      |
| Array    | 配列                   | `Array<型名>` または `型名[]` で記述 |
| Object   | オブジェクト           | `interface` や `type` を使って型指定 |
| null     | 存在しない値           |                                      |
| undefind | 未定義の値             |                                      |
| void     | 関数で何も値を返さない |                                      |
| any      | どんな値でも許容する   | できる限り使用しない                 |

**細かく見ると他にもいろいろな型があるので、その時は 1 回 1 回調べよう！！**

## 記法

### 変数

- 型名は小文字始まり

```typescript
const text: string = "hello";
const num: number = 100;
```

### 配列

- 配列を示す `Array` は大文字始まり
- ２種類の記法がある

```typescript
const arr1: Array<string> = ["hoge", "fuga", "piyo"];
const arr2: string[] = ["foo", "bar", "baz"];
```

### オブジェクト

- `interface` や `type` を使ってまとめて中身の型を指定する
- どちらを使うかは使い方やチームのやり方に合わせるのが無難
- 本勉強会では `type` を使った書き方を紹介

```typescript
type Profile = {
  name: string
  age: number
  hobby: {
    type: string
    content: string
  }
}

const myProfile: Profile = {
  name: "せきやん"
  age: 25
  hobby: {
    type: "楽器"
    content: "エレキベース"
  }
}
```

### 関数

- 引数、戻り値それぞれで指定できる

```typescript
const func = (num: number): number => num * 2;
```

### 複合的な型 (ユニオン型)

- 複数の型を許容することができる `union` を指定することができる

```typescript
let num: string | number = 0;
num = 1; //◯
num = "1"; //◯
num = true; //×
```

### Generics

- 動的な型付けを行う時に使用する
- 実は配列の時に使ってたのもこれ

関数を例にした使用例

```typescript
//通常
const func1 = <T>(value: T) => console.log(value);
func1<string>("hello");

//複数指定
const func2 = <T, K>(value1: T, value2: K) => console.log(value1, value2);
func2<string, number>("hello", 1);

//継承
const func3 = <T extends unknown>(value: T) => console.log(value);
func3<string>("hello");
```

# 参考になるサイト

困った時の参考書！

- [サバイバル TypeScript](https://typescriptbook.jp/)

interface と type について詳しく知りたい人

- [interface と type の違い、そして何を使うべきかについて](https://zenn.dev/luvmini511/articles/6c6f69481c2d17)
