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
