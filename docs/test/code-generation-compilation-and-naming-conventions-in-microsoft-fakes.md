---
title: Microsoft Fakes:コードの生成とコンパイル、名前付け規則
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 9a1ba469f460e966be581b87226f2a89faac8186
ms.sourcegitcommit: f2bb3286028546cbd7f54863b3156bd3d65c55c4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2020
ms.locfileid: "93325933"
---
# <a name="code-generation-compilation-and-naming-conventions-in-microsoft-fakes"></a>Microsoft Fakes におけるコード生成、コンパイル、および名前付け規則

この記事では、Fakes のコード生成とコンパイルのオプションと問題について説明し、Fakes で生成される型、メンバー、およびパラメーターの名前付け規則について説明します。

**必要条件**

- Visual Studio Enterprise
- .NET Framework プロジェクト
::: moniker range=">=vs-2019"
- Visual Studio 2019 Update 6 でプレビューされた .NET Core と SDK スタイルのプロジェクトのサポートは、Update 8 で既定で有効になっています。 詳細については、「[.NET Core および SDK スタイルのプロジェクトのための Microsoft Fakes](/visualstudio/releases/2019/release-notes#microsoft-fakes-for-net-core-and-sdk-style-projects)」を参照してください。
::: moniker-end

## <a name="code-generation-and-compilation"></a>コードの生成とコンパイル

### <a name="configure-code-generation-of-stubs"></a>スタブのコード生成を構成する

スタブ型の生成は、 *.fakes* ファイル拡張子を持つ XML ファイルで構成されます。 Fakes フレームワークは、カスタム MSBuild タスクによってビルド処理で統合され、ビルド時にそれらのファイルを検出します。 Fakes コード ジェネレーターは、スタブ型をアセンブリにコンパイルし、参照をプロジェクトに追加します。

次の例に、 *FileSystem.dll* で定義されたスタブ型を示します。

```xml
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">
    <Assembly Name="FileSystem"/>
</Fakes>
```

### <a name="type-filtering"></a>型のフィルター処理

*.fakes* ファイルでフィルターを設定して、スタブされる型を制限できます。 StubGeneration 要素の下に Clear、Add、Remove 要素を無制限に追加して、選択された型の一覧を作成できます。

たとえば、次の *.fakes* ファイルは、System 名前空間と System.IO 名前空間の下に型のスタブを生成しますが、System では "Handle" が含まれる型は除外します。

```xml
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">
  <Assembly Name="mscorlib" />
  <!-- user code -->
  <StubGeneration>
    <Clear />
    <Add Namespace="System!" />
    <Add Namespace="System.IO!"/>
    <Remove TypeName="Handle" />
  </StubGeneration>
  <!-- /user code -->
</Fakes>
```

フィルター文字列では、単純な文法を使用して一致の照合方法を定義します。

- 既定では、フィルターは大文字と小文字を区別しません。フィルターは部分文字列の一致を照合します。

     `el` は "hello" に一致します

- フィルターの末尾に `!` を追加すると、正確な大文字小文字を区別する照合が行われます。

     `el!` は "hello" に一致しません

     `hello!` は "hello" に一致します

- フィルターの末尾に `*` を追加すると、文字列のプレフィックスとの一致が照合されます。

     `el*` は "hello" に一致しません

     `he*` は "hello" に一致します

- セミコロン区切りのリストに複数のフィルターを記述すると、フィルターは論理和として組み合わされます。

     `el;wo` は "hello" と "world" に一致します。

### <a name="stub-concrete-classes-and-virtual-methods"></a>具象クラスと仮想メソッドをスタブする

既定では、スタブ型はすべての非シール クラスに対して生成されます。 *.fakes* 構成ファイルで指定して、スタブ型を抽象クラスに制限することができます。

```xml
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">
  <Assembly Name="mscorlib" />
  <!-- user code -->
  <StubGeneration>
    <Types>
      <Clear />
      <Add AbstractClasses="true"/>
    </Types>
  </StubGeneration>
  <!-- /user code -->
</Fakes>
```

### <a name="internal-types"></a>内部型

Fakes コード ジェネレーターは、生成された Fakes アセンブリから見える型の shim 型と stub 型を生成します。 shim が適用されたアセンブリの内部型を Fakes アセンブリおよびテスト アセンブリから見えるようにするには、生成された Fakes アセンブリとテスト アセンブリに可視性を与える、shim が適用されたアセンブリ コードに <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性を追加します。 次に例を示します。

```csharp
// FileSystem\AssemblyInfo.cs
[assembly: InternalsVisibleTo("FileSystem.Fakes")]
[assembly: InternalsVisibleTo("FileSystem.Tests")]
```

**厳密な名前を持つアセンブリの内部型**

shim が適用されたアセンブリが厳密な名前を持つ場合に、アセンブリの内部型にアクセスするには:

- テスト アセンブリと Fakes アセンブリの両方に、厳密な名前を付ける必要があります。

- テスト アセンブリと Fakes アセンブリの公開キーを、shim が適用されたアセンブリの **InternalsVisibleToAttribute** 属性に追加します。 以下に、shim が適用されたアセンブリが厳密な名前を持つとき、shim が適用されたアセンブリ コード内のサンプル属性がどのように表示されるかを示します。

    ```csharp
    // FileSystem\AssemblyInfo.cs
    [assembly: InternalsVisibleTo("FileSystem.Fakes",
        PublicKey=<Fakes_assembly_public_key>)]
    [assembly: InternalsVisibleTo("FileSystem.Tests",
        PublicKey=<Test_assembly_public_key>)]
    ```

shim が適用されたアセンブリが厳密な名前を持つ場合、Fakes フレームワークは生成された Fakes アセンブリに自動的に厳密な名前で署名します。 テスト アセンブリに厳密な名前で署名する必要があります。 「[厳密な名前付きアセンブリ](/dotnet/framework/app-domains/strong-named-assemblies)」を参照してください。

Fakes フレームワークは、生成されるすべてのアセンブリに同じキーを使って署名するため、このスニペットを開始点として使って Fakes アセンブリの **InternalsVisibleTo** 属性を shim が適用されたアセンブリ コードに追加することができます。

```csharp
[assembly: InternalsVisibleTo("FileSystem.Fakes, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e92decb949446f688ab9f6973436c535bf50acd1fd580495aae3f875aa4e4f663ca77908c63b7f0996977cb98fcfdb35e05aa2c842002703cad835473caac5ef14107e3a7fae01120a96558785f48319f66daabc862872b2c53f5ac11fa335c0165e202b4c011334c7bc8f4c4e570cf255190f4e3e2cbc9137ca57cb687947bc")]
```

*.fakes* ファイルの `Fakes`\\`Compilation` 要素に、`KeyFile` 属性値として代替キーを含む *.snk* ファイルへの完全パスを指定して、shim が適用されたアセンブリ用に作成したキーなどの別の公開キーを Fakes アセンブリに指定することができます。 次に例を示します。

```xml
<-- FileSystem.Fakes.fakes -->
<Fakes ...>
  <Compilation KeyFile="full_path_to_the_alternate_snk_file" />
</Fakes>
```

shim が適用されたアセンブリ コード内の Fakes アセンブリの InternalVisibleTo 属性の 2 番目のパラメーターとして、代替 *.snk* ファイルの公開キーを使う必要があります。

```csharp
// FileSystem\AssemblyInfo.cs
[assembly: InternalsVisibleTo("FileSystem.Fakes",
    PublicKey=<Alternate_public_key>)]
[assembly: InternalsVisibleTo("FileSystem.Tests",
    PublicKey=<Test_assembly_public_key>)]
```

上の例で、値 `Alternate_public_key` と `Test_assembly_public_key` は同じでもかまいません。

### <a name="optimize-build-times"></a>ビルド時間を最適化する

Fakes アセンブリのコンパイルで、ビルド時間が非常に長くなることがあります。 別の一元化されたプロジェクトで .NET System のアセンブリとサードパーティのアセンブリの Fakes アセンブリを生成することで、ビルド時間を最小限に抑えることができます。 こういうアセンブリはコンピューターでほとんど変更されないため、生成された Fakes アセンブリを他のプロジェクトで再利用できます。

単体テスト プロジェクトから、プロジェクト フォルダーの FakesAssemblies の下に置かれたコンパイル済みの Fakes アセンブリに参照を追加します。

1. テスト プロジェクトに一致する .NET ランタイム バージョンを含む新しいクラス ライブラリを作成します。 これに Fakes.Prebuild という名前を付けます。 プロジェクトから不要な *class1.cs* ファイルを削除します。

2. Fakes が必要なすべてのシステムおよびサードパーティのアセンブリへの参照を追加します。

3. アセンブリごとに *.fakes* ファイルを追加し、ビルドします。

4. テスト プロジェクトから

    - Fakes ランタイム DLL への参照があることを確認します。

         *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\PublicAssemblies\Microsoft.QualityTools.Testing.Fakes.dll*

    - Fakes を作成したアセンブリごとに、プロジェクトの *Fakes.Prebuild\FakesAssemblies* フォルダーの対応する DLL ファイルへの参照を追加します。

### <a name="avoid-assembly-name-clashing"></a>アセンブリ名の競合を回避する

チーム ビルド環境では、すべてのビルド出力が 1 つのディレクトリにマージされます。 複数のプロジェクトが Fakes を使用している場合は、異なるバージョンの Fakes アセンブリが互いにオーバーライドすることがあります。 たとえば、.NET Framework 2.0 からの TestProject1 による *mscorlib.dll* の Fakes 処理と .NET Framework 4 の TestProject2 による *mscorlib.dll* の Fakes 処理は、いずれも *mscorlib.Fakes.dll* Fakes アセンブリを生成します。

この問題を回避するには、 *.fakes* ファイルを追加するとき、Fakes 処理で非プロジェクト参照用にバージョンで修飾された Fakes アセンブリ名を自動的に作成する必要があります。 バージョンで修飾された Fakes アセンブリ名の場合は、Fakes アセンブリ名を作成するときにバージョン番号が埋め込まれます。

アセンブリ MyAssembly とバージョン 1.2.3.4 の場合、Fakes アセンブリ名は MyAssembly.1.2.3.4.Fakes です。

*.fakes* の Assembly 要素の Version 属性を編集して、このバージョンを変更または削除できます。

```xml
attribute of the Assembly element in the .fakes:
<Fakes ...>
  <Assembly Name="MyAssembly" Version="1.2.3.4" />
  ...
</Fakes>
```

## <a name="fakes-naming-conventions"></a>Fakes 名前付け規則

### <a name="shim-type-and-stub-type-naming-conventions"></a>Shim 型とスタブ型の名前付け規則

**名前空間**

- .Fakes サフィックスは名前空間に追加されます。

   たとえば、`System.Fakes` 名前空間には System 名前空間の shim 型が含まれています。

- Global.Fakes には、空の名前空間の shim 型が含まれています。

  **型名**

- Shim プレフィックスが型名に追加されて、shim 型名が作成されます。

   たとえば、ShimExample は Example 型の shim 型です。

- Stub プレフィックスが型名に追加されて、stub 型名が作成されます。

   たとえば、StubIExample は IExample 型の stub 型です。

  **型引数および入れ子にされた型の構造体**

- ジェネリック型の引数がコピーされます。

- shim 型の場合、入れ子にされた型の構造体がコピーされます。

### <a name="shim-delegate-property-or-stub-delegate-field-naming-conventions"></a>Shim デリゲート プロパティまたはスタブ デリゲート フィールドの名前付け規則

空の名前から始まるフィールド名の付け方の **基本的な規則** は次のとおりです。

- メソッド名が追加されます。

- メソッド名が明示的なインターフェイスの実装の場合、ドットは削除されます。

- メソッドがジェネリックの場合、`Of`*n* が追加されます。ここで、 *n* はジェネリック メソッドの引数の数です。

  プロパティの get/set アクセス操作子などの **特殊なメソッド名** は、次の表に示すように処理されます。

|メソッドの種類|例|追加されるメソッド名|
|-|-|-|
|**コンストラクター**|`.ctor`|`Constructor`|
|静的 **コンストラクター**|`.cctor`|`StaticConstructor`|
|"_" で区切られた 2 つの部分で構成されるメソッド名を持つ **アクセサー** (プロパティの get アクセス操作子など)|*kind_name* (一般的なケース。ただし ECMA で強制されていない)|*NameKind* 。両方のパーツが大文字になり、前後が逆になっています|
||プロパティの get アクセス操作子 `Prop`|`PropGet`|
||プロパティの set アクセス操作子 `Prop`|`PropSet`|
||イベントを追加する操作子|`Add`|
||イベントを削除する操作子|`Remove`|
|2 つの部分で構成される **演算子**|`op_name`|`NameOp`|
|例: + 演算子|`op_Add`|`AddOp`|
|**変換演算子** の場合は、戻り値の型が追加されます。|`T op_Implicit`|`ImplicitOpT`|

> [!NOTE]
> - **インデクサーの get および set アクセス操作子** は、プロパティと同様に扱われます。 インデクサーの既定の名前は `Item` です。
> - **パラメーターの型** の名前は変換され、連結されます。
> - **戻り値の型** は、オーバーロードのあいまいさがない場合は無視されます。 あいまいさがある場合は、戻り値の型が名前の末尾に追加されます。

### <a name="parameter-type-naming-conventions"></a>パラメーターの型の名前付け規則

|種類|追加される文字列|
|-|-|
|**型**`T`|T<br /><br /> 名前空間、入れ子になった構造体、およびジェネリック チックは削除されます。|
|**out パラメーター**`out T`|`TOut`|
|**ref パラメーター** `ref T`|`TRef`|
|**配列型**`T[]`|`TArray`|
|**多次元配列** 型 `T[ , , ]`|`T3`|
|**ポインター** 型 `T*`|`TPtr`|
|**ジェネリック型**`T<R1, ...>`|`TOfR1`|
|型 `C<TType>` の **ジェネリック型引数**`!i`|`Ti`|
|メソッド `M<MMethod>` の **ジェネリック メソッド引数**`!!i`|`Mi`|
|**入れ子にされた型**`N.T`|`N` が追加され、その後に `T`|

### <a name="recursive-rules"></a>再帰的な規則

次の規則は再帰的に適用されます。

- Fakes は C# を使用して Fakes アセンブリを生成するため、無効な C# トークンを生成する文字は "_" (アンダースコア) にエスケープされます。

- 結果の名前が宣言する型のいずれかのメンバーと競合する場合は、01 から始まる 2 桁のカウンターの追加して番号付けスキーマが使用されます。

## <a name="see-also"></a>関連項目

- [Microsoft Fakes を使用したテストでのコードの分離](../test/isolating-code-under-test-with-microsoft-fakes.md)
