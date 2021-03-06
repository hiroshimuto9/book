# ジェネリクスが使われている標準ライブラリ

ジェネリクスは標準ライブラリの中でも多くの箇所で利用されています。ジェネリクスを利用する代表的なものとしては、

* Arrayオブジェクト
* Promiseオブジェクト
* Mapオブジェクト

などがあります。

これらのオブジェクトでジェネリクスがどう使われているのかを見てきましょう。

### なぜジェネリクスが使われているか

Arrayオブジェクトは `string` や `number` など状況に応じて色々な型の要素を保持する必要があります。この時、配列の要素の型はどんなプログラムを実装するかで変わってきます。つまり、要素の型を抽象化してプログラマーが実装時に型を指定できる必要があります。

この型を抽象化する方法としてジェネリクスが利用されています。

```typescript
const numbers: Array<number> = [1, 2, 3, 4];
```

### 標準ライブラリを使ってみる

実際にジェネリクスが使われる標準ライブラリを利用した実装をみてみましょう。

#### Array.protoype.map&lt;T&gt;\(\)

Arrayオブジェクトの `map<T>()` メソッドは引数で渡された関数を全ての配列の要素に適用することで、新しい配列を返す関数です。サンプルコードでは、新しく生成されるs数値配列の要素の型を指定する `map<number>` でジェネリクスが使われています。

```typescript
const textNumbers = ["1", "2", "3", "4"];
const numbers = textNumbers.map<number>(function(text: string) {
    return Number(text);
});
```

#### Map&lt;K, V&gt;

`Map<K, V>` オブジェクトでは、`K` にキーの型を指定し`V` にキーに紐づく値の型を指定します。先ほどの `map<T>()` メソッドは、ジェネリクスの型定義が1つだけでしたが、`Map<K, V>` は型定義が2つあります。このようにジェネリクスの型定義は1つである必要はなく、複数の型定義を持つことも可能です。

```typescript
type Address = {
    country: string,
    postalCode: string,
    address1: string,
};

const addresses = new Map<string, Address>();
addresses.set("太郎", {
    country: "日本",
    postalCode: "8256405",
    address1: "東京都",
});

console.log(addresses.get("太郎"));
```

#### Promise&lt;T&gt;

Promiseオブジェクトについての説明は本書にてより詳細な記載がありますので、そちらをご参照ください。

{% page-ref page="promise-async-await.md" %}

#### 標準ライブラリの型定義の参照方法

標準ライブラリの型定義ファイルはTypeScriptの公式リポジトリのlibディレクトリで確認する事ができます。  
[https://github.com/microsoft/TypeScript/tree/master/lib](https://github.com/microsoft/TypeScript/tree/master/lib)

`Array.prototype.map()` の型は [lib/lib.es5.d.ts](https://github.com/microsoft/TypeScript/blob/master/lib/lib.es5.d.ts#L1170) のファイルで確認できます。

