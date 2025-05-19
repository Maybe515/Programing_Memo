## コーディングルール
- 処理するコードの最後には`;`をつける
- メソッドの処理内容は`{`と`}`で囲む
- リビルドする際はプリプロセス命令を記載する
<br>

## 型宣言
### 変数
`<型名> <変数名> = <value>;`<br>

型名は、一般的に値型であれば`int`,`long`,`float`,`double`,`bool`、参照型であれば`string`がよく使われる。<br>
宣言する型の代わりに`var`(variant)を入れると、コンパイル時に自動で型を判定してくれる。<br>

```C#
public static void Main()
{
  string x = "Hello, World!";
  Console.WriteLine(x);    // コンソールに「Hello, World!」と表示される
}
```
<br>

### 定数
`const <型名> <定数名> = <value>;`<br>

定数は`const`を型名の前につけて、宣言する。<br>
```C#
static void Main()
{
  const string x = "Hello, World!";
  Console.WriteLine(x);    // コンソールに「Hello, World!」と表示される
}
```
定数は宣言時に代入した値から変更できなくなる（値を代入するとエラーとなる）<br>
<br>

#### バージョニング問題
`private`で定数を宣言している場合には定数に変更があったとしても影響範囲が狭く、修正も容易なため問題ないが、`public`で宣言している場合、定数の変更があった際に別ファイルやプロジェクトで参照している箇所の再コンパイルが必要になる。<br>
publicで使用したい場合は`readonly`というキーワードを用いて宣言することが望ましい。また整数型の定数を宣言したい時には`enum`(列挙型)と呼ばれるデータ型を使うのが良い。<br>
<br>

> [!NOTE]
> Microsoftは宣言時の基本的な命名規則を以下としている。<br>
> - 宣言するにあたり、フィールド名はPascal形式を使用する。<br>
> - フィールド名にはプリフィックスを使用しない。
<br>

### 配列
一次元配列：`<型名> <配列名> = new <型名>[<int>];`<br>
多次元配列：`<型名> <配列名> = new <型名>[<int1>,<int2>];`<br>

型名の後ろに`[]`をつけることで配列として宣言できる（`var`で宣言する場合は不要）<br>
多次元配列の場合、`int1`は行数（縦）、`int2`は列数（横）として考えると分かりやすい。<br>
```C#
// 一次元配列
var arr1 = new int[1];      // varで宣言
int[] arr2 = new int[1];    // intで宣言

// 多次元配列
var arr3 = new int[3, 4];      // varで宣言
int[] arr4 = new int[5, 6];    // intで宣言
```
<br>


## 関数まとめ
### 分岐処理
- `if`, `elseif`, `else`
- `switch-case`, `default`

### ループ処理
- `for`
- `while`
- `do-while`
- `foreach`

### その他
- `split`：指定した区切り文字から文字列を分割できる。
- `containts`：文字列・配列・Listから指定した対象が含まれるかを確認できる。
- `Regex.IsMatch`：正規表現を用いて、指定した対象が含まれるかを確認できる。
- `tostring`
<br>

## 演算子
### 単項演算子
|演算子|内容|使用例|
|:-:|:-:|:-:|
|+x|そのまま|x = 5　⇒　+x = 5|
|-x|符号反転|x = 5　⇒　-x=-5|
|x++|x=x+1 (後置インクリメント)|x = 5　⇒　x++ = 6|
|++x|x=x+1 (前置インクリメント)|x = 5　⇒　++x = 6|
|x--|x=x-1 (後置デクリメント)|x = 5　⇒　x-- = 4|
|--x|x=x-1 (後置インクリメント)|x = 5　⇒　--x = 4|
|!x|否定|x = true　⇒　!x = false|
|~x|補数 (ビット反転)|int x = 5　⇒　~x = -6|
<br>

### 二項演算子
|演算子|内容|使用例|
|:-:|:-:|:-:|
|x + y|和||
|x - y|差||
|x * y|積||
|x / y|商||
|x % y|余剰||
|x & y|論理積||
|`x | y`|論理和||
|x ^ y|排他的論理和||
|x << y|左シフト||
|x >> y|右シフト||
|x = y|代入||
|x == y|等しい||
|x != y|等しくない||
|x < y|大なり||
|x <= y|以上||
|x > y|小なり||
|x >= y|以下||
|x && y|AND演算||
|`x || y`|OR演算||
|x + y (string)|文字列結合|"abc" + "def" = "abcdef"|
|x += y|和（複合代入演算子）||
|x -= y|差（複合代入演算子）||
|x *= y|積（複合代入演算子）||
|x /= y|商（複合代入演算子）||
|x %= y|余剰（複合代入演算子）||
|x &= y|論理積（複合代入演算子）||
|x |= y|論理和（複合代入演算子）||
|x ^= y|排他的論理和（複合代入演算子）||
|x <<= y|左シフト（複合代入演算子）||
|x >>= y|右シフト（複合代入演算子）||




<br>

## プリプロセッサ（プリプロセス命令）
C#では、コーディングしたプログラムをコンパイルして実行ファイルに変換する。<br>
このコンパイルの直前に行なう特殊な処理のことを指す。<br>
プログラムの動作には直接影響しないが、利用することで生産性を向上させることができる。<br>
<details><summary>プリプロセス命令一覧</summary><ul><li>define</li><li>if</li><li>elif</li><li>else</li><li>endif</li><li>error</li><li>line</li><li>nullable</li><li>pragma</li><li>pragma checksum</li><li>pragma warning</li><li>region</li><li>end region</li><li>undef</li><li>warning</li></ul></details>
<br>

### シンボルの定義
上記の命令で使用するための定数のようなもの。定義するには`#define`を使用する。<br>
この命令はコードの先頭で定義する必要がある。<br>
```C#
#define <symbol name>

using System;
using System.Collections.Generic;
```
<br>

### undef命令
`#define`命令で定義したシンボルを未定義にする。<br>
この命令も`#define`と同様にコードの先頭で定義する必要があり、<br>
コンパイラオプションで設定したシンボルを、そのソースコード上で無効にすることができる。<br>
```C#
#undef <symbol name>

using System;
using System.Collections.Generic;
```
<br>

### 条件付きコンパイル（if, elif, else, endif）
定義したシンボルに従って、コンパイル対象となるコードを切り替えることができる。<br>
デバッグビルドとリリースビルドの切り替えでよく使用される。<br>
`if文`と同じ動作で実行される。<br>
```C#
#define <symbol name1>
#define <symbol name2>

using System;
using System.Collections.Generic;

#if <symbol name1>
    // 処理
#elif <symbol name2>
    // 処理
#else
    // 処理
#endif
```
<br>

## コメントアウト
- 一行コメントは`//`を使用する。<br>
- 複数行コメントは`/*`と`*/`で囲む。<br>

上記とは別にドキュメントコメントと呼ばれる特殊なコメントがある。ドキュメントコメントは`///`を使用する。<br>
ドキュメントコメントを記述しておくと、Visual Studioなどの開発環境や、専用のツールを使って、APIドキュメント（クラスやメソッドの説明書）を自動的に生成できるため、コードの可読性を向上させることができる。
