# 知ってて欲しい！モダンJSの知識
## 変数宣言
**var は使わずに let と const を使う**

変数宣言方法による仕様
| | 上書き | 再宣言 |
| ---- | :----: | :----: |
| var | ◯ | ◯ |
| let | ◯ | × |
| const | × | × |

```javascript
var val = 2
val = 3            //◯
var val = "hello"  //◯

let val = 2
val = 3            //◯
let val = "hello"  //×

const val = 2
val = 3              //×
const val = "hello"  //×
```

## テンプレート文字列
文字列の中に変数を埋め込む書き方

```javascript
const name = "関谷"
const age = 25
console.log(`私の名前は${name}で、${age}歳です。`)

//私の名前は関谷で、25歳です。
```

## アロー関数
シンプルに書ける関数の書き方

従来の関数
```javascript
function func(value) {
  return value
}

//もしくは

const func = function (value) {
  return value
}
```

アロー関数
```javascript
const func = (value) => {
  return value
}
```

## 分割代入
オブジェクトや配列から値を抽出する方法

### オブジェクトの分割代入
```javascript
const profile = {
  name: "関谷",
  age: 25
}

const { name, age } = profile
console.log(`私の名前は${name}で、${age}歳です。`)

//別名をつける
const { name: newName, age: newAge } = profile
console.log(`私の名前は${newName}で、${newAge}歳です。`)

//私の名前は関谷で、25歳です。
```

### 配列の分割代入
```javascript
const profile = ["関谷", 25]

const [name, age] = profile
console.log(`私の名前は${name}で、${age}歳です。`)

//私の名前は関谷で、25歳です。
```

## スプレッド構文
配列やオブジェクトの処理をまとめて書く記法

```javascript
const nums = [1, 2]
const addNum = (num1, num2) => num1 + num2
console.log(addNum(...nums))

//1 2
```

## map, filter 関数
モダンな書き方では for 文を使う機会は少なく、map や filter といった関数を駆使して書く場合がほとんどです！

### map
配列を順番に処理して、処理した結果を `新しい配列として` 返す

```javascript
const nums = [2, 3, 5, 7, 11]
const doubleNum = nums.map((num) => num * 2)
console.log(...doubleNum)

//4 6 10 14 22
```

### filter
配列を順番に処理して、条件に一致した値のみを抽出した `新しい配列として` 返す

```javascript
const nums = [1, 2, 5, 8, 12]
const multiples2 = nums.filter((num) => num % 2 === 0)
console.log(...multiples2)

//2 8 12
```
