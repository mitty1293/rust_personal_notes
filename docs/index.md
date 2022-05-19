# Cargoコマンド
[Rust の最初のステップ / Rust とは / Rust 固有の機能](https://docs.microsoft.com/ja-jp/learn/modules/rust-introduction/3-rust-features)
- `cargo new` コマンドを使用して、新しいプロジェクト テンプレートを作成する。
- `cargo build` コマンドを使用して、プロジェクトをビルドする。
- `cargo run` コマンドを使用して、プロジェクトをビルドして実行する。
- `cargo test` コマンドを使用して、プロジェクトをテストする。
- `cargo check` コマンドを使用して、プロジェクトの種類を確認する。
- `cargo doc` コマンドを使用して、プロジェクトのドキュメントをビルドする。
- `cargo publish` コマンドを使用して、crates.io にライブラリを発行する。
- Cargo.toml ファイルにクレート名を追加して、依存クレートをプロジェクトに追加する。Rustのマニフェストファイル。プロジェクトのメタデータとすべての依存関係をここに保存する。

# 式と文
[Rust の最初のステップ / Rust プログラムを初めて作成する / Rust プログラムの基本的な構造を理解する](https://docs.microsoft.com/ja-jp/learn/modules/rust-create-program/1-program-structure)
- 式(expression): 返り値を評価する。値を返す。
    - ex. `5+6`, `6`, 関数呼び出し, マクロ呼び出し, `{}`
    - 終端にセミコロンを含まない
- 文(statement): 処理を実行するが値を返さない。
    - 終端にセミコロンを含む
-  開始コード ステートメントは、左余白からスペース 4 つ分インデントされます。
- コードがセミコロンで終わっていない場合、開始ステートメントが完了する前に次のコード行を実行する必要があることが認識されます。実行する次のコード行は、さらにスペース 4 つ分インデントされます。

# todo! マクロ
[Rust の最初のステップ / Rust プログラムを初めて作成する / Rust プログラムの基本的な構造を理解する](https://docs.microsoft.com/ja-jp/learn/modules/rust-create-program/1-program-structure)
- Rust のマクロは、可変個の入力引数を受け取る関数のようなものです。
- `todo!` マクロは、Rust プログラムで未完了のコードを識別するために使用されます。
    - このマクロは、プロトタイプを作成するときや、完了していない動作を示す場合に便利です。

# println! マクロ
[Rust の最初のステップ / Rust プログラムを初めて作成する / Rust プログラムの基本的な構造を理解する](https://docs.microsoft.com/ja-jp/learn/modules/rust-create-program/1-program-structure)
- `println!` マクロには、画面または "`println!`" に表示される 1 つ以上の入力引数が必要です。
-  `println!` マクロにより、テキスト文字列内の中かっこ `{}` の各インスタンスが、リスト内の次の引数の値に置き換えられます。
```Rust
fn main() {
    // Call println! with three arguments: a string, a value, a value
    println!("The first letter of the English alphabet is {} and the last letter is {}.", 'A', 'Z');
}
```

# 定数
[Rust by exmaple](https://doc.rust-jp.rs/rust-by-example-ja/custom_types/constants.html)  
[Tour of rust](https://tourofrust.com/07_ja.html)
- Rustで定数は`const`, `static`で定義する。
    - const:
        - 不変の値（通常はこちらを使用する）。
        - 変更しようとするとエラー。`mut`も付けられない。
        - グローバルスコープを含む任意のスコープで宣言可能。
    - static: 
        - スタティックなライフタイムを持つミュータブル(mut)な値。グローバル変数。
        - ちょっと難しいのであまり使わなくても良いかも。
- 大文字のスネークケース `SCREAMING_SNAKE_CASE` を使うことが一般的。
```Rust
const PI: f32 = 3.14159;
```

# 変数のシャドウ処理
[Rust の最初のステップ / Rust プログラムを初めて作成する / Rust で変数を作成して使用する](https://docs.microsoft.com/ja-jp/learn/modules/rust-create-program/2-variables)
- 既存の変数の名前を使って新しい変数を宣言できる。
- 前の変数は引き続き存在するが、このスコープでは参照できなくなる。（シャドウされる）
- 以下ではまず`shadow_num`を宣言し、新しく`shadow_num`を宣言する際に前の変数バインドをシャドウしている。新しい`shadow_num`が作成されている。
```Rust
// Declare first variable binding with name "shadow_num"
let shadow_num = 5;

// Declare second variable binding, shadows existing variable "shadow_num" 
let shadow_num = shadow_num + 5; 

// Declare third variable binding, shadows second binding of variable "shadow_num"
let shadow_num = shadow_num * 2; 

println!("The number is {}.", shadow_num);
```
- 以下はシャドウ処理ではないが、同じ結果をエラー無く出力できる。
```Rust
fn main() {
    let mut shadow_num = 5;

    shadow_num = shadow_num + 5; 

    shadow_num = shadow_num * 2; 

    println!("The number is {}.", shadow_num);
}
```

# テキスト: 文字と文字列
[Rust の最初のステップ / Rust プログラムを初めて作成する / 数値、テキスト、true/false 値のデータ型を調べる](https://docs.microsoft.com/ja-jp/learn/modules/rust-create-program/3-basic-data-types)
https://zenn.dev/toga/books/rust-atcoder/viewer/23-string
- Rustでは、2つの基本的な文字列型と1つの文字型がサポートされている。
- 文字は 1 つの項目で、文字列は一連の文字である。

## 文字型
### `char`型
- 項目を単一引用符で囲んで指定する。
```Rust
let uppercase_s = 'S';
let lowercase_f = 'f';
let smiley_face = '😃';
```

## 文字列型
### `str`型(文字列リテラル)
- 文字列処理において，スライス `[T]` に相当する型
- 項目を二重引用符""で囲んで指定する。
- `&str`のような参照を用いることがほとんど。
- コンパイル時に中身が判明している必要があり、変更できない文字列データへのポインタと考えることができる。
- 簡単にいうと、プログラムの実行時に変更されないテキスト データの不変ビュー。

### Todo
[Tour of Rust 基本的な型](https://tourofrust.com/05_ja.html)
-  スライスは実行時に長さが決まるのでは？コンパイル時に中身が判明している必要あるのか？上の説明あってるか？

### `String`型
- 文字列処理において，ベクタ `Vec<T>` に相当する型
- ヒープに割り当てられる。
- コンパイル時に文字数を把握しておく必要がない。
- 簡単にいうと、プログラムの実行時に変更される可能性があるテキストデータ。

# デバッグステートメント
[Rust の最初のステップ / Rust プログラムを初めて作成する / 複合データに列挙型バリアントを使用する](https://docs.microsoft.com/ja-jp/learn/modules/rust-create-program/5-enum-variants)
- `#[derive(Debug)]` 構文を使用すると、コードの実行中に、標準出力では見ることのできない特定の値を確認できる。
- `println!` マクロでデバッグ データを表示するには、構文 `{:#?}` を使用して、読み取り可能な方法でデータを書式設定する。

# 関数
- Rustでの一般的な方法では、関数の最後のコード行を返す値と同じにすることで、関数の終了時に値を返す。
```Rust
fn divide_by_5(num: u32) -> u32 {
    num / 5
    // a = num/5
    // return a
    // とかしなくて良い。返す値を最終行にしておくだけで良い。
    // 式なのでセミコロンを付与してはいけない。付与すると値が評価されずに返らなくなってしまう。
}
fn main() {
    let num = 25;
    println!("{} divided by 5 = {}", num, divide_by_5(num));
}

fn car_factory(color: String, transmission: Transmission) -> Car {
    // 関数の最後のコード行を構造体インスタンス呼び出しにすると、インスタンスが呼び出し元に返る。
    Car {
        color: color,
        transmission: transmission
    }
}
```

# 構造体
- `struct`で定義
- フィールドの集合である。
```Rust
struct SeaCreature {
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}
fn main() {
    let a = SeaCreature {
        name: String::from("イルカ"),
        arms: 2,
        legs: 1,
        weapon: String::from("超音波"), 
    };
    println!("{}", a.weapon);
}
```

# メソッド
[Tour of Rust メソッドの定義](https://tourofrust.com/24_ja.html) 
- 関数と違い、メソッドは特定のデータ型と紐づく関数のこと。
    - スタティックメソッド ある型そのものに紐付き、演算子 :: で呼び出せます。
    - インスタンスメソッド ある型のインスタンスに紐付き、演算子 . で呼び出せます。
```Rust
fn main() {
    // スタティックメソッドでStringインスタンスを作成する。
    let s = String::from("Hello world!");
    // インスタンスを使ってメソッドを呼び出す。
    println!("{} is {} characters long.", s, s.len());
}
```

# メモリ
Rust のプログラムでは、データを保持するために次の3種類のメモリ空間を持っています。

## データメモリ
- 固定長もしくは スタティック (例: プログラムのライフサイクルで常に存在するもの)なデータ。
- プログラム内の文字列(例: ‘Hello World’), この文字列のキャラクタは読み取りにしか使えないため、この領域に入ります。
- コンパイラはこういったデータに対してチューニングをしており、メモリ上の位置はすでに知られていてかつ固定であるため、非常に速く使うことができます。

## スタックメモリ
- 関数内で宣言された変数。
- 関数が呼び出されている間は、メモリ上の位置は変更されることがないため、コンパイラからするとチューニングができるので、スタックメモリも非常に速くデータにアクセスできます。

## ヒープメモリ
- プログラムの実行時に作られるデータ。
- このメモリにあるデータは追加、移動、削除、サイズの調節などの操作が許されています。
- 動的であるため、遅いと思われがちですが、 これによりメモリの使い方に柔軟性を生み出すことができます。
- データをヒープメモリに入れることをアロケーション(allocation)といい、データをヒープメモリから削除することはディアロケーション(deallocation)と言います。

# 配列
[Tour of Rust 基本的な型](https://tourofrust.com/05_ja.html)  
[Tour of Rust 配列](https://tourofrust.com/08_ja.html)
メモリに連続して格納された同じ型のオブジェクトのコレクション  
コンパイル時に長さが決まる同じ型のコレクション

## 特徴
- すべての要素は同じデータ型。(タプルは異なる型でも良い)
- サイズは固定。長さが変更されることはない。コンパイル時に決まる。
- 要素の値だけが変更される可能性がある。

## 定義
`[T; N]`: `T`は要素の型、`N`は長さ
```Rust
// 値のコンマ区切りで定義可能
let days = ["Sunday", "Monday", "Tuesday"];

// [初期値; 長さ] で定義可能
let bytes = [0; 5];

// シグネチャ[T; size]で定義可能
let array: [i64; 5];
let nums: [i32; 3] = [1, 2, 3];
println!("{:?}", nums);
println!("{}", nums[1]);
```

## 参照
- array[0], array[1]のようにインデックス番号で要素に参照可能。
- 長さ以上のインデックスを指定するとコンパイルエラー

# ベクター
配列と同様に同じ型の複数の値を格納するコレクション

## 特徴
- すべての要素は同じデータ型。
- サイズはいつでも拡大縮小可能。

## 要素の追加削除
push(value), pop(value)メソッドで末尾の追加削除が可能。  
異なる型の要素を追加しようとするとエラー。
```Rust
// 末尾に追加
fruit.push("Apple");
// 末尾を削除
fruit.pop()
```

## 参照と要素の変更
- `vec[0]`, `vec[1]`のようにインデックス番号で要素に参照可能。
- `index_vec[1] = index_vec[1] + 5;` のようにインデックスでアクセスして値の変更が可能。
- 長さ以上のインデックスを指定するとコンパイルはできるが実行時にパニックする。

## 定義
一般的には`vec!`マクロを使用して定義する。
```Rust
// 値のコンマ区切りで定義可能
let three_nums = vec![15, 3, 46];
println!("Initial vector: {:?}", three_nums);  

// [初期値; 長さ] で定義可能
let zeroes = vec![0; 5];
println!("Zeroes: {:?}", zeroes); 

// 空ベクターの作成
let mut fruit: Vec<String> = Vec::new();
let mut car = Vec::<i32>::new()

// シグネチャVec<T>で定義可能
let v: Vec<u32>;
```

## 型
```Rust
// データ型が不明なときはジェネリック型Tを用いる
let v: Vec<T>;
// 型がわかるときには以下のようにTに既知の型を指定する。
Vec<u32>
Vec<String>
```

# Option と Result
[RustのOptionとResult](https://qiita.com/take4s5i/items/c890fa66db3f71f41ce7)

## Option
[Rust の最初のステップ / Rust でエラーを処理する / Option 型を使用して値がない場合に対処する](https://docs.microsoft.com/ja-jp/learn/modules/rust-error-handling/3-use-option-type-deal-with-absence)
- Option<T>型は 取得できないかもしれない値 を表現する列挙型。
- 値が無いことを示すNoneとあることを示すSome(T)のどちらかをとる。
    - Noneがエラーを表しているわけでは無いことに注意。
    - Noneは値がなかったことを示しているだけで、エラーとは限らない。
- エラーを表したい場合はResult<T,E>を使う方がふさわしい

## Result
[Rust の最初のステップ / Rust でエラーを処理する / Result 型を使用してエラーを処理する](https://docs.microsoft.com/ja-jp/learn/modules/rust-error-handling/5-use-result-type)
- Result<T,E>は失敗するかもしれない処理の結果を表現する列挙型。
- Resultはrustコンパイラから特別扱いされており、無視するとwarinigが出る。
- Resultは例外がないrustにおける標準のエラーハンドリング方法。
- エラーが発生する可能性がある場合は結果にResultを用いるようにすること。

## ?演算子
[TRPL エラー委譲のショートカット: ?演算子](https://doc.rust-jp.rs/book-ja/ch09-02-recoverable-errors-with-result.html#%E3%82%A8%E3%83%A9%E3%83%BC%E5%A7%94%E8%AD%B2%E3%81%AE%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88-%E6%BC%94%E7%AE%97%E5%AD%90)

### Todo
- ?演算子についてまとめること

# 所有権・借用・参照

## 有効期間に注釈を付ける
[ Rust の最初のステップ / Rust によるメモリ管理の方法を理解する / 有効期間を使用した参照の検証](https://docs.microsoft.com/ja-jp/learn/modules/rust-memory-management/3-validate-references-with-lifetimes)

### Todo
- 注釈の必要性と方法がいまいちよくわからない。。。
- ライフタイム、ライフタイムパラメータ
- 上記を含めてまとめなおすこと

# ジェネリクス
[ Rust の最初のステップ ジェネリック型と特性を実装する / ジェネリック データ型とは](https://docs.microsoft.com/ja-jp/learn/modules/rust-generic-types-traits/1-what-are-generic-data-types)
[Rust入門 Chapter09 ジェネリクス](https://zenn.dev/mebiusbox/books/22d4c1ed9b0003/viewer/8ccf20)
[RustCoder Chapter31 関数のジェネリクス](https://zenn.dev/toga/books/rust-atcoder/viewer/31-generic-function)
- 任意の型（定義時点で不明な型）を受け取れる関数、構造体、列挙型等を定義する仕組みをジェネリクスという。
- 任意の型のことをジェネリック型という。

# 特性（トレイト）
[Rust の最初のステップ / ジェネリック型と特性を実装する / 特性を使用して共有動作を定義する](https://docs.microsoft.com/ja-jp/learn/modules/rust-generic-types-traits/2-define-shared-behavior-with-traits?source=learn)
[TRPL トレイト: 共通の振る舞いを定義する](https://doc.rust-jp.rs/book-ja/ch10-02-traits.html)
[Rust by Example トレイト](https://doc.rust-jp.rs/rust-by-example-ja/trait.html)
- 特性 = トレイト のこと。
- 他の言語でいうインターフェースのようなもの。
- 任意の型となりうるSelfに対して定義されたメソッドの集合のこと。同じトレイト内で宣言されたメソッド同士はお互いにアクセスすることができる。
- 型の振る舞いは、その型に対して呼び出せるメソッドから構成されます。異なる型は、それらの型全てに対して同じメソッドを呼び出せるなら、 同じ振る舞いを共有することになります。トレイト定義は、メソッドシグニチャをあるグループにまとめ、なんらかの目的を達成するのに必要な一連の振る舞いを定義する手段です。
- 動作の観点から関数または構造体のパラメーターを指定する必要がある場合に役立つ。

## Todo
- トレイトについてまとめること。いまいち理解しているか怪しい。
- [演習 - ジェネリック型を実装する](https://docs.microsoft.com/ja-jp/learn/modules/rust-generic-types-traits/6-exercise-implement-generic-type)の回答がよくわからない。そんなことどこにも書いてない。

# derive特性
- 自身で定義した型（構造体、ジェネリック型）は`Debug`, `Display`, `PartialEq`特性を実装されていないため、同じ型同士での比較やターミナルへの表示がエラーとなる。
- `#[derive(Trait)]`属性を使用すると、`Trait`特性が自動で実装される。
    - `#[derive(Debug, PartialEq)]`であれば`Debug`, `PartialEq`特性が自動で実装される。

# 反復子（イテレータ）
[Tour of Rust for](https://tourofrust.com/17_ja.html)
- 値を1つずつ取り出して処理するためのもの
- 項目がなくなるまで「次の項目は何か？」と質問することができるオブジェクト。
- Range, スライスや配列やVecやHashMap等のコレクション型
- すべての反復子で Iterator という名前の特性が実装されており、標準ライブラリに定義されている。
    ```Rust
    trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
    }
    ```
- Iterator には next というメソッドがある。これを呼び出すと、Option<Item> が返される。next メソッドからは、要素がある限り、Some(Item) が返される。 すべての処理が完了すると、反復が終了したことを示す None が返される。

## Todo
- 以下の反復子関連メソッドについて調べてまとめる。  
  [演習 - 反復子を実装する](https://docs.microsoft.com/ja-jp/learn/modules/rust-generic-types-traits/7-exercise-implement-iterator)の回答がよくわからないため。
    - `drain`
    - `collect`

# パッケージ、クレート、モジュール
- パッケージ：1つ以上のクレートを持ち、ある機能を提供するための単位
    - 1つの `Cargo.toml` で管理する粒度
        - `Cargo.toml` にクレート達をビルドするための情報が含まれている
    - 0個か1個のライブラリクレートを持つ
    - バイナリクレートはいくらでも持って良い
    - ライブラリクレートとバイナリクレートをあわせて少なくとも1つのクレートを持っていないといけない
- クレート：ライブラリ(`lib.rs`)か実行可能ファイル(`main.rs`)を生成するモジュール群
    - Rustのコンパイル単位である
    - ライブラリクレート： `src/lib.rs`
    - バイナリクレート： `src/main.rs`
        - または `src/bin` ディレクトリにファイルを置くことで複数のバイナリクレートを持つことができる
- モジュール： mod や use でまとめる単位
```Shell
package
  ├ Cargo.toml
  └ src/
    ├ lib.rs     ... 0 or 1
    ├ main.rs    ... 0 or 1
    └ bin/       ... 0 or N (files)
      ├ bin_a.rs
      ├ bin_b.rs
      └ ...
```

# テスト
[Rust の最初のステップ / 自動テストを記述する](https://docs.microsoft.com/ja-jp/learn/modules/rust-automated-tests/)

## `assert!` マクロ
- `assert(条件, メッセージ)`
- 第一引数に指定された条件がtrueであることを表明する
- 条件がfalseの場合、省略可能なメッセージ引数を`panic!`に渡す
    - `panic!`: 回復不能なエラーとして、指定されたメッセージの出力とともにプログラムを終了する

## `assert_eq!` マクロ
- `assert_eq(a, b, メッセージ)`
- 式aと式bが等しいことを表明する
- 条件がfalseの場合、省略可能なメッセージ引数を`panic!`に渡す

## ドキュメンテーションコメント、ドキュメントテスト
[TRPL テストとしてのドキュメンテーションコメント](https://doc.rust-jp.rs/book-ja/ch14-02-publishing-to-crates-io.html#%E3%83%86%E3%82%B9%E3%83%88%E3%81%A8%E3%81%97%E3%81%A6%E3%81%AE%E3%83%89%E3%82%AD%E3%83%A5%E3%83%A1%E3%83%B3%E3%83%86%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%A1%E3%83%B3%E3%83%88)
- `//` でコメントアウトできるが、`///` でドキュメントを記載できる
    - Markdown記法をサポートしている
    - `cargo doc` でHTMLドキュメントを生成できる
        - HTMLドキュメントは`target/doc`ディレクトリに配置される
- ドキュメント内にコードブロックを追加すると、`cargo test`時にテストされる
    - サンプルコード等が動くことを保障できる
