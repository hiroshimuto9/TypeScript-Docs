# 基本の型

---

## 型アノテーション

```typescript
const name: string = "型アノテーション太郎";
```

TypeScript では、`:TypeAnnotation`構文を使い、型アノテーションを書けます。
上記のコードでは、変数`name`が`string`型であることを意味します。

---

## プリミティブ型

TypeScript のプリミティブ型には、以下が存在します。

- `boolean`型
- `string`型
- `number`型
- `bigint`型
- `symbol`型
- `undefined`
- `null`

---

## `boolean`

`true`/`false`を値として持つ真偽値の型

```typescript
const isDone: boolean = true;
const isDone: boolean = false;
```

---

## `number`

整数だけでなく実数も含む数値を扱います。

2 進数・8 進数・16 進数も使用可能です。

```typescript
const decimal: number = 6;
const hex: number = 0xf00d; // 16進数
const binary: number = 0b1010; // 2進数
const octal: number = 0o744; // 8進数
const big: bigint = 100n;
```

### `豆知識`

整数の限界値は、`Number.MAX_SAFE_INTEGER`と`Number.MIN_SAFE_INTEGER`によって決まります。

```typescript
console.log({ max: Number.MAX_SAFE_INTEGER, min: Number.MIN_SAFE_INTEGER });
// {max: 9007199254740991, min: -9007199254740991}
```

安全をチェックするには ES6 の`Number.isSafeInteger`を使用します。
安全でない値は、安全な値から`+1`もしくは`-1`離れた値であり、加算減算の寮に関わらず結果が丸められてしまいます。

```typescript
// 安全な値
console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER)); // true

// 危険な値
console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1)); // false
```

---

## `string`

文字列を扱います。
`""(ダブルクオート)`もしくは`''(シングルクオート)`を使い、変数を定義することができます。
また``(バッククオート)`で囲むと、テンプレートリテラル記法が使うことができ、改行や変数展開が可能です。

```typescript
const textA = "テキスト";
const textB = "テキスト";
```

```typescript
const textA = `テキストを
改行できます。`;

const name: string = "たかし";
const text: string = `私の名前は${name}です。`;
console.log(text); // 私の名前はたかしです。
```

---

## `bigint`

`number`型よりも大きな整数を扱います。

---

## `symbol`

symbol 値は、Symbol コンストラクタを呼び出す事で定義できます。
シンボルは普遍で一意になります。
※ ECMAScript 2015 から導入されたため、コンパイラーオプションの lib に「lib.es2015.iterable」の設定などが必要

```typescript
const sym1: symbol = Symbol("シンボル");
const sym2: symbol = Symbol("シンボル");
console.log(sym1 === sym2); // false 一意であるため、引数に同じ文字列を入れても等価にはならない。
```

---

## `undefined`

未定義や値が代入されていない値

### `undefined`な変数を参照するとコンパイルエラーとなります。(※strictNullChecks: true の場合)

```typescript
let value: string;
console.log(value); // Variable 'value' is used before being assigned.
```

### 存在しないプロパティにアクセスした際に、`undefined`が返却されます。

```typescript
let numArray: number[] = [1, 2, 3];
console.log(numArray[100]); // undefined
```

---

## `null`

明示的に無効な値を示します。
`undefine`と`null`は別物のため`null`型の変数に`undefined`を入れることも、またその逆もエラーとなります。

```typescript
const sample: null = undefined; //Type 'undefined' is not assignable to type 'null'.
const sample2: undefined = null; //Type 'null' is not assignable to type 'undefined'.
```

---

## リテラル型

リテラル型では、特定の値のみ許容する型を作ることができます。

```typescript
// 文字列リテラル
const stringFoo: "foo" = "foo";
const stringBar: "bar" = "foo"; // Type '"foo"' is not assignable to type '"bar"'.
```

リテラル型単体ではあまり使い所はありませんが、ユニオン型(Union types)で結合して便利な型を作成する時に相性が良いです。

### Literal Narrowing

変数を`var`や`let`で定義した時と、`const`で定義した時では型推論が変わります。

```typescript
const Hellow = "Hellow"; // stringではなく、"Hellow"型として推論される
let hellow = "hellow"; // "hellow"型ではなく、string型として推論される
```

これは、`const`と`var`や`let`の役割によるものです。`const`は JavaScript において、一度変数が定義されると他の値の再代入を許容しないため
特定の文字列型として推論されます。一方で、`var`や`let`は再代入を可能とするため、特定の文字列型となると意図に反します。そのため`string`型(プリミティブ型)として推論
されます。

```typescript
let sample = "Hello"; // string型として推論される
const sample2: "Hellow" = sample; // "Hellow"型として推論されるため、Type 'string' is not assignable to type '"Hellow"'.とエラーになる。
```

---

## 配列型

TypeScript にて配列の型を定義する`[]`を用いる方法とジェネリクスを用いる方法の 2 通り存在します。

```typescript
const list: number[] = [1, 2, 3];
const list: Array<number> = [1, 2, 3];
```

---

## Object 型

`Object`型には、`Object`型と`object`型が存在します。
そして、それらは同一のものではありません。

```typescript
const obj: object = {};
const anotherObj: Object = {};
console.log(obj === anotherObj); // false
```

`Object`型: プリミティブ型の`boolean`,`number`,`string`,`symbol`を含みます。

`object`型: プリミティブ型の`boolean`,`number`,`string`,`symbol`, `bigint`, `null`, `undefined`を含みません。

詳細はこちらの記事が参考になります。

[TypeScript の Object 型と object 型は同じ……と思うじゃん?](https://qiita.com/suin/items/928642e48959e864a74e)

### 独自のオブジェクト型を定義

TypeScript では、独自のオブジェクト型を定義することができます。

```typescript
const obj: {
  name: string;
  age: number;
} = {
  name: "Takashi",
  age: 22,
};
```

しかし、上記の定義方法では毎回インラインで書く必要があり非効率です。
そこで TypeScript では、`Interface`や`Type aliases`によって独自の型に名前を定義することが可能です。
`Interface`や`Type aliases`の詳細は各項目の説明にて行います。

```typescript
// Interface
interface Person {
  name: string;
  age: number;
}

// Person型をInterfaceで定義することで、型指定が可能となる。
const person: Person = {
  name: "Takashi",
  age: 22,
};
console.log(person); // { "name": "Takashi", "age": 22 }

// Type aliases
type Person = {
  name: string;
  age: number;
};

// Person型をtypeで定義することで、型指定が可能となる。
const person: Person = {
  name: "Takashi",
  age: 22,
};
console.log(person); // { "name": "Takashi", "age": 22 }
```

型に合わない値を代入しようとしたり、型とは異なる形式で代入を行おうとするとエラーになります。

```typescript
interface Person {
  name: string;
  age: number;
}

// number型のageにstring型を代入
const person: Person = {
  name: "Takashi",
  age: "22", // Type 'string' is not assignable to type 'number'.
};

// ageプロパティが無い
const person: Person = {
  name: "Takashi", // Property 'age' is missing in type '{ name: string; }' but required in type 'Person'.
};
```

---

## `Tuple(タプル)型`

`Tuple`型を使うことで、それぞれの要素の型と、順番や要素数に制約を設ける配列の型を表現できます。
書き方は単純で、`[]`の中に型を定義するだけです。

タプルで定義した範囲外の要素に対してアクセスするとエラーになります。
またタプルで定義した型と異なる型の値を代入したり、順番が異なるとエラーになります。

```typescript
const foo: [string, number] = ["foo", 1];
foo[100]; // Tuple type '[string, number]' of length '2' has no element at index '100'.

let bar: [string, number];
bar = ["bar", 1]; // ok
bar = [1, "bar"];
// Type 'number' is not assignable to type 'string'.
// Type 'string' is not assignable to type 'number'.
```

タプルで定義された変数は、指定された型が持つメソッド使用できます。
型が持つメソッド以外にアクセスしようとするとエラーになります。

```typescript
const foo: [string, number] = ["foo", 1];
console.log(foo[0].substring(1)); // string型が持つメソッドsubstring
console.log(foo[1].valueOf()); // number型が持つメソッドvalueOf()
console.log(foo[1].substring(1)); // Property 'substring' does not exist on type 'number'.
```

---
