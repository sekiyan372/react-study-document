# 状態管理

## 状態とは

コンポーネント（画面）が持っている状態を指します。といってもイメージがつかないかもしれませんが、例えば以下のようなものが状態になります。

- エラーがあるか
- メニューが開かれているか
- テキストボックスに入力した値

etc...

React ではこのような状態のことを `State` と言い、イベントの実行に合わせて State を更新することでページ内で動的な表現をすることができます。

## React Hooks

関数コンポーネントでは React Hooks という様々な機能を持ったものを使います。React Hooks には useState、useEffect、useContext、useCollback など他にも様々なものがあり、先頭が `use` で始まるのが慣習になっています。

Hooks は関数とは違うものであり、ただ値を返したりするものではないことを覚えておきましょう。

React Hooks を使用するには React から import をします。

```typescript
import { useState } from "react";
```

## useState

React Hooks 中でも State の管理に使うのが `useState` という Hooks です。

useState では状態を保持する変数と、その状態を更新するための関数の 2 つをセットで定義します。それぞれ、以下のようにして `1つ目に State`、`2つ目に State を更新する関数`を定義します。

```typescript
const [num, setNum] = useState();
```

State を更新する関数は `set + State名` にするのが慣習です。

### 初期値

useState には初期値を設定することができます。

```typescript
const [num, setNum] = useState(0);
```

### 型

State には型も設定することができます。型は Generics を使って記述することができます。

```typescript
const [num, setNum] = useState<number>(0);

const [text, setText] = useState<string>("text");

const [bool, setbool] = useState<boolean>(true);
```

### State の更新

2 つ目の値に設定した関数を呼び出すことで、State を更新することができます。呼び出し時には引数として更新する値を引数として渡すことで、その値に State を更新することができます。

```typescript
const [num, setNum] = useState<number>(0);

const addNum = () => {
  // 指定した値に更新
  setNum(1);

  // 現在の State を使用して計算する
  setNum(num + 1);
};
```
