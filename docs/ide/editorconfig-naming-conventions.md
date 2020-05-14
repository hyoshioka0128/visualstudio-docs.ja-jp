---
title: EditorConfig ファイルでの .NET の名前付け規則
ms.date: 03/31/2020
ms.topic: reference
helpviewer_keywords:
- naming conventions [EditorConfig]
- EditorConfig naming conventions
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d4864cc20813bc57b35e315a3b415cb6902e6361
ms.sourcegitcommit: 054815dc9821c3ea219ae6f31ebd9cd2dc8f6af5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2020
ms.locfileid: "80544005"
---
# <a name="net-naming-conventions-for-editorconfig"></a>EditorConfig での .NET の名前付け規則

名前付け規則は、クラス、プロパティ、およびメソッドなどのコード要素の名前付けに関するものです。 たとえば、パブリック メンバーは大文字表記とする必要があること、またはプライベート フィールドは `_` で始まる必要があることを指定できます。 これらの規則を適用するには、[.editorconfig ファイル](../ide/create-portable-custom-editor-options.md)にそれらを含めます。 名前付け規則違反は、規則に対して選択した重大度に応じて、**エラー一覧**内に表示されるか、または名前の下に修正候補として表示されます。 違反を確認するためにプロジェクトをビルドする必要はありません。

それぞれの名前付け規則については、名前付け規則を適用するシンボル、名前付けのスタイル、および規則を適用する上での重大度を、以下に示すプロパティを使用して指定する必要があります。 プロパティの順序は重要ではありません。

まずは、名前付け規則を完全に記述するために必要なプロパティの各々で使用する名前付け規則のタイトルを選択します。 たとえば、`public_members_must_be_capitalized` は、名前付け規則の名前としてわかりやすく適切です。 以下のセクションでは、選択したタイトルを **<namingRuleTitle\>** として参照します。

## <a name="symbols"></a>シンボル

最初に、名前付けルールを適用するシンボルのグループを識別します。 このプロパティの形式は次のとおりです。

`dotnet_naming_rule.<namingRuleTitle>.symbols = <symbolTitle>`

**<symbolTitle\>** の値を、`public_symbols` などのわかりやすいタイトルに置き換えて、シンボルのグループに名前を付けます。 規則が適用されるシンボルを記述する 3 つのプロパティ名 (シンボルの種類、アクセシビリティ レベル、修飾子) の中で **<symbolTitle\>** を使用します。

### <a name="kinds-of-symbols"></a>シンボルの種類

名前付け規則を適用するシンボルの種類を記述するには、次の形式でプロパティを指定します。

`dotnet_naming_symbols.<symbolTitle>.applicable_kinds = <values>`

許容される値を次のリストに示します。個々の値をコンマで区切ることで複数の値を指定できます。

- \*(この値を使用すると、すべてのシンボルが指定されます)
- namespace
- class
- struct
- interface
- enum
- property
- メソッド
- フィールド
- event
- delegate
- パラメーター
- type_parameter
- local
- local_function

> [!NOTE] 
> タプル メンバーは現時点ではサポートされていません。

### <a name="accessibility-levels-of-symbols"></a>シンボルのアクセシビリティ レベル

名前付け規則を適用するシンボルのアクセシビリティ レベルを記述するには、次の形式でプロパティ名を指定します。

`dotnet_naming_symbols.<symbolTitle>.applicable_accessibilities = <values>`

許容される値を次のリストに示します。個々の値をコンマで区切ることで複数の値を指定できます。

- \*(この値を使用すると、すべてのアクセシビリティ レベルが指定されます)
- public
- internal または friend
- private
- protected
- protected\_internal または protected_friend
- private\_protected
- local

   `local` アクセシビリティ レベルは、メソッド内で定義された記号に適用されます。 コード内でアクセシビリティを指定できない記号には、名前規則を定義すると便利です。 たとえば、定数 (`required_modifiers = const`) の名前規則に `applicable_accessibilities = local` を指定した場合、規則はメソッド内で定義された定数のみに適用され、型の中で定義されたものには適用されません。

   ```csharp
   class TypeName
   {
     // Constant defined in a type.
     const int X = 3;

     void Method()
     {
       // Constant defined in a method with "local" accessibility.
       const int Y = 4;
     }
   }
   ```

### <a name="symbol-modifiers-optional"></a>シンボルの修飾子 (省略可能)

名前付け規則を適用するシンボルの修飾子を記述するには、次の形式でプロパティ名を指定します。

`dotnet_naming_symbols.<symbolTitle>.required_modifiers = <values>`

許容される値を次のリストに示します (複数の値はコンマで区切ります)。

- `abstract` または `must_inherit`
- `async`
- `const`
- `readonly`
- `static` または `shared`

   > [!NOTE]
   > `static` または `shared` シンボルに対する名前付け規則がある場合、それは暗黙的に静的である `const` シンボルにも適用されます。 `static` 名前付け規則を `const` シンボルに適用しない場合は、`const` シンボルに対する別の名前付け規則を作成します。

名前付け規則は、`required_modifiers` で指定されている "*すべて*" の修飾子が含まれるシグネチャのみと一致します。 このプロパティを省略した場合は、既定値である空のリストが使用されます。すなわち、一致のために特定の修飾子は必要ありません。 このことは、この規則が適用されるかどうかに、シンボルの修飾子が影響を及ぼさないことを意味します。

> [!TIP]
> `required_modifiers` に対しては値 `*` を指定しないでください。 代わりに、`required_modifiers` プロパティをそっくり省略すると、すべての種類の修飾子に名前付け規則が適用されます。

## <a name="style"></a>スタイル

名前付け規則を適用するシンボルのグループを識別したので、名前付けのスタイルを記述できます。 名前が特定のプレフィックスまたは特定のサフィックスを持つスタイルを指定したり、名前に含まれている個々の単語が特定の文字で区切られるスタイルにしたりすることができます。 また、大文字/小文字のスタイルを指定することもできます。 スタイル プロパティの形式は次のようになります。

`dotnet_naming_rule.<namingRuleTitle>.style = <styleTitle>`

**<styleTitle\>** の値を、`first_word_upper_case_style` のようにわかりやすいタイトルに置き換えることで、スタイルに名前を付けます。 名前付けのスタイル (プレフィックス、サフィックス、単語区切り文字、大文字/小文字) を記述するプロパティ名の中で **<styleTitle\>** を使用します。 これらのプロパティを 1 つまたは複数使用して、目的のスタイルを記述します。

### <a name="require-a-prefix"></a>プレフィックスが必要

シンボル名が特定の文字で始まる必要があることを指定するには、次のプロパティを使用します。

`dotnet_naming_style.<styleTitle>.required_prefix = <prefix>`

### <a name="require-a-suffix"></a>サフィックスが必要

シンボル名が特定の文字で終わる必要があることを指定するには、次のプロパティを使用します。

`dotnet_naming_style.<styleTitle>.required_suffix = <suffix>`

### <a name="require-a-certain-word-separator"></a>特定の単語区切り記号が必要

シンボル名の中の個々の単語を特定の文字で区切る必要があることを指定するには、次のプロパティを使用します。

`dotnet_naming_style.<styleTitle>.word_separator = <separator character>`

### <a name="require-a-capitalization-style"></a>大文字/小文字のスタイルが必要

シンボル名に対して特定の大文字/小文字のスタイルを指定するには、次のプロパティを使用します。

`dotnet_naming_style.<styleTitle>.capitalization = <value>`

このプロパティに設定できる値は次のとおりです。

- pascal_case
- camel_case
- first\_word_upper
- all\_upper
- all_lower

> [!NOTE]
> 名前付けスタイルの一部として大文字/小文字スタイルを指定する必要があります。そうしないと、名前付けスタイルは無視される可能性があります。

## <a name="severity"></a>重要度

名前付け規則違反の重大度を記述するには、次の形式でプロパティを指定します。

`dotnet_naming_rule.<namingRuleTitle>.severity = <value>`

次の表に、許容される重大度の値と、その意味を示します。

重要度 | 効果
------------ | -------------
none | 規則は完全に抑制されます。
refactoring または silent | このスタイルに準拠していないときは、ユーザーには何も表示されません。ただし、自動生成コードは、このスタイルに従います。
修正候補 | このスタイルに準拠していないとき、修正候補としてユーザーに表示されます (最初の 2 文字の下に点線が付きます)。 コンパイル時には影響しません。
warning | このスタイルに準拠していないとき、**エラー一覧**にコンパイラの警告が表示されます。
error | このスタイルに準拠していないとき、**エラー一覧**にコンパイラ エラーが表示されます。

> [!NOTE]
> 名前付け規則違反を確認するために、プロジェクトをビルドする必要はありません。 名前付け規則違反は、コードの編集時に、**エラー一覧**に表示されるか、または修正候補として表示されます。

## <a name="rule-order"></a>ルールの順序

::: moniker range="vs-2017"

名前付け規則は、EditorConfig ファイル内に固有度の高いものから低いものの順に並べる必要があります。 適用可能な最初に検出されたルールのみが適用されます。 ただし、同じ名前のルールの "*プロパティ*" が複数ある場合は、その名前の最も最近見つかったプロパティが優先されます。 詳細については、「[File hierarchy and precedence (ファイルの階層と優先順位)](create-portable-custom-editor-options.md#file-hierarchy-and-precedence)」を参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio 2019 バージョン 16.2 以降では、EditorConfig ファイルで名前付け規則が定義されている順序は関係ありません。 代わりに、Visual Studio で、規則自体の定義に従って、名前付け規則が自動的に並べ替えられます。 [EditorConfig 言語サービス拡張機能](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig)では、EditorConfig ファイルを分析して、ファイルでの規則の順序が実行時にコンパイラで使用される順序と異なる場合に報告できます。

以前のバージョンの Visual Studio を使っている場合、名前付け規則は、EditorConfig ファイル内で固有度の高いものから低いものの順に並べる必要があります。 適用可能な最初に検出されたルールのみが適用されます。 ただし、同じ名前のルールの "*プロパティ*" が複数ある場合は、その名前の最も最近見つかったプロパティが優先されます。 詳細については、「[File hierarchy and precedence (ファイルの階層と優先順位)](create-portable-custom-editor-options.md#file-hierarchy-and-precedence)」を参照してください。

::: moniker-end

## <a name="default-naming-styles"></a>既定の名前付けスタイル

カスタム名前付け規則を何も指定しないと、Visual Studio では次の既定のスタイルが使われます。

- アクセシビリティが `public`、`private`、`internal`、`protected`、または `protected_internal` であるクラス、構造体、列挙型、プロパティ、およびイベントでは、既定の名前付けスタイルはパスカル ケースです。

- アクセシビリティが `public`、`private`、`internal`、`protected`、または `protected_internal` であるインターフェイスでは、既定の名前付けスタイルはパスカル ケースであり、プレフィックス **I** を付ける必要があります。

## <a name="example"></a>例

次の *.editorconfig* ファイルには、パブリック プロパティ、メソッド、フィールド、イベント、デリゲートを大文字で入力する必要があることを指定した名前付け規則が含まれています。 この名前付け規則では、コンマを使用して個々のシンボル値を区切ることにより、規則を適用する複数の種類のシンボルを指定しています。

```ini
# Public members must be capitalized (public_members_must_be_capitalized)
[*.{cs,vb}]
dotnet_naming_rule.public_members_must_be_capitalized.symbols   = public_symbols
dotnet_naming_symbols.public_symbols.applicable_kinds           = property,method,field,event,delegate
dotnet_naming_symbols.public_symbols.applicable_accessibilities = public
dotnet_naming_symbols.public_symbols.required_modifiers         = readonly

dotnet_naming_rule.public_members_must_be_capitalized.style    = first_word_upper_case_style
dotnet_naming_style.first_word_upper_case_style.capitalization = first_word_upper

dotnet_naming_rule.public_members_must_be_capitalized.severity = suggestion
```

次のスクリーンショットでは、この名前付け規則の結果がエディターに表示されています。 2 つのパブリック変数に付けられた名前は、最初の文字が大文字になっていません。 1 つは `const`、もう 1 つは `readonly` です。 名前付け規則は `readonly` シンボルのみに適用されるので、`readonly` 変数のみに、名前付け規則の修正候補が表示されています。

![名前付け規則の修正候補](media/editorconfig-naming-rule-suggestion.png)

これで、違反の重大度を `warning` に変更してみましょう。

```ini
dotnet_naming_rule.public_members_must_be_capitalized.severity = warning
```

コード ファイルを閉じてから再度開いた場合、名前違反の下には修正候補が表示されるのではなく、緑色の波線が表示され、さらにエラー一覧に警告が表示されます。

![名前付け規則の警告](media/editorconfig-naming-rule-warning.png)

## <a name="see-also"></a>関連項目

- [言語規則](editorconfig-language-conventions.md)
- [書式規則](editorconfig-formatting-conventions.md)
- [Roslyn 名前付け規則](https://github.com/dotnet/roslyn/blob/master/.editorconfig#L63)
- [移植可能なカスタム エディター オプションを作成する](../ide/create-portable-custom-editor-options.md)
- [EditorConfig の .NET コーディング規則の設定](editorconfig-code-style-settings-reference.md)
