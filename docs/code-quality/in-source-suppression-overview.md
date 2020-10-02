---
title: コード分析の違反を抑制する
ms.date: 08/27/2020
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: 4ef64528d8686267677020458374ef96143f6e34
ms.sourcegitcommit: c025a5e2013c4955ca685092b13e887ce64aaf64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91658517"
---
# <a name="suppress-code-analysis-violations"></a>コード分析の違反を抑制する

多くの場合、警告が適用されないことを示すと便利です。 これは、コードがレビューされたことと、警告を抑制できることをチームメンバーに示します。 ソース内抑制 (ISS) では、属性を使用して <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 警告を抑制します。 属性は、警告を生成したコードセグメントの近くに配置できます。 属性を入力し <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> てソースファイルに追加することも、 **エラー一覧** の警告のショートカットメニューを使用して自動的に追加することもできます。

属性は、 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> コンパイル時に CODE_ANALYSIS コンパイルシンボルが定義されている場合にのみ、マネージコードアセンブリの IL メタデータに含まれる条件付き属性です。

C++/CLI では、マクロ CA を使用して \_ \_ ヘッダーファイル内のメッセージまたは ca グローバル SUPPRESS_MESSAGE を抑制し、 \_ \_ 属性を追加します。

> [!NOTE]
> ソース内の抑制メタデータが誤って配布されるのを防ぐために、リリースビルドでは、ソース内の抑制を使用しないでください。 また、ソース内抑制の処理コストが原因で、アプリケーションのパフォーマンスが低下する可能性があります。

::: moniker range="vs-2017"

> [!NOTE]
> プロジェクトを Visual Studio 2017 に移行すると、コード分析の警告が多数発生する可能性があります。 警告を修正する準備ができていない場合は、[実行コード分析の**分析**] を選択し、[  >  **アクティブな問題を抑制**する] を選択して、すべての警告を非表示にできます。
>
> ![Visual Studio でコード分析を実行し、問題を抑制する](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> プロジェクトを Visual Studio 2019 に移行すると、コード分析の警告が多数発生する可能性があります。 警告を修正する準備ができていない場合は、[ビルドの**分析**] を選択し、  >  **アクティブな問題を非**表示にして、すべての警告を非表示にすることができます。

::: moniker-end

## <a name="suppressmessage-attribute"></a>SuppressMessage 属性

**エラー一覧**でコード分析の警告のコンテキストまたは右クリックメニューから [**抑制**] を選択すると、 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性がコードまたはプロジェクトのグローバル抑制ファイルのいずれかに追加されます。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>属性の形式は次のとおりです。

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

属性のプロパティは次のとおりです。

- [**カテゴリ]** -ルールが定義されているカテゴリ。 コード分析規則のカテゴリの詳細については、「 [マネージコードの警告](/dotnet/fundamentals/code-analysis/quality-rules/index)」を参照してください。

- **Checkid** -ルールの識別子。 サポートには、規則識別子の短い名前と長い名前の両方が含まれます。 短い名前は CAXXXX です。長い名前は CAXXXX: FriendlyTypeName です。

- **理由** -メッセージを抑制する理由を文書化するために使用されるテキストです。

- **MessageId** -各メッセージの問題の一意の識別子。

- **スコープ** -警告が抑制されている対象。 ターゲットが指定されていない場合は、属性のターゲットに設定されます。 サポートされる [スコープ](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope) は次のとおりです。

  - [`module`](#module-suppression-scope) -このスコープは、アセンブリに対する警告を抑制します。 これは、プロジェクト全体に適用されるグローバルな抑制です。

  - `resource` -([レガシ FxCop](../code-quality/static-code-analysis-for-managed-code-overview.md) のみ) このスコープでは、モジュール (アセンブリ) の一部であるリソースファイルに書き込まれた診断情報の警告が抑制されます。 このスコープは、ソースファイルを分析するだけで、Roslyn アナライザー診断用の C#/VB コンパイラでは読み取られません。

  - `type` -このスコープは、型に対して警告を抑制します。

  - `member` -このスコープは、メンバーに対して警告を抑制します。

  - `namespace` -このスコープでは、名前空間自体に対する警告が抑制されます。 名前空間内の型に対する警告は抑制されません。

  - `namespaceanddescendants` -(コンパイラバージョン3.x 以降と Visual Studio 2019 が必要) このスコープでは、名前空間とそのすべての子孫シンボルで警告が抑制されます。 この `namespaceanddescendants` 値は、レガシ分析では無視されます。

- **Target** -警告が抑制されるターゲットを指定するために使用される識別子。 完全修飾項目名が含まれている必要があります。

Visual Studio で警告が表示された場合は、 `SuppressMessage` [グローバル抑制ファイルに抑制を追加](../code-quality/use-roslyn-analyzers.md#suppress-violations)することで、の例を確認できます。 抑制属性とその必須プロパティは、プレビューウィンドウに表示されます。

## <a name="suppressmessage-usage"></a>SuppressMessage の使用法

コード分析の警告は、属性が適用されるレベルでは抑制され <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> ます。 たとえば、属性は、アセンブリ、モジュール、型、メンバー、またはパラメーターレベルで適用できます。 この目的は、違反が発生したコードに対して抑制情報を密に結合することです。

抑制の一般的な形式には、ルールカテゴリとルール識別子が含まれます。このルールには、ユーザーが判読できる規則名の表現が含まれています。 次に例を示します。

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

ソース内の抑制メタデータを最小限に抑えるためにパフォーマンス上の厳密な理由がある場合は、規則名を省略できます。 ルールカテゴリとそのルール ID が一緒に、十分に一意なルール識別子が構成されます。 次に例を示します。

`[SuppressMessage("Microsoft.Design", "CA1039")]`

保守容易性のために、規則名を省略することは推奨されません。

## <a name="suppress-selective-violations-within-a-method-body"></a>メソッド本体内の選択的違反を抑制する

抑制属性はメソッドに適用できますが、メソッド本体内に埋め込むことはできません。 これは、属性をメソッドに追加した場合に、特定の規則のすべての違反が抑制されることを意味 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> します。

場合によっては、将来のコードがコード分析ルールから自動的に除外されるように、違反の特定のインスタンスを抑制することが必要になることがあります。 特定のコード分析規則を使用すると、属性のプロパティを使用してこれを行うことができ `MessageId` <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> ます。 一般に、特定のシンボル (ローカル変数またはパラメーター) に対する違反に関する従来のルールでは、プロパティが尊重され `MessageId` ます。 [CA1500: VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) は、このようなルールの一例です。 ただし、実行可能コード (非シンボル) での違反に関する従来の規則では、プロパティは考慮されません `MessageId` 。 また、.NET Compiler Platform ("Roslyn") アナライザーでは、プロパティは考慮されません `MessageId` 。

規則の特定のシンボル違反を抑制するには、属性のプロパティのシンボル名を指定し `MessageId` <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> ます。 次の例は、2つの CA1500 の違反を含むコードを示しています。変数の場合は[VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md)、変数の場合は &mdash; `name` 1 `age` です。 シンボルの違反のみ `age` が抑制されます。

```vb
Public Class Animal
    Dim age As Integer
    Dim name As String

    <CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId:="age")>
    Sub PrintInfo()
        Dim age As Integer = 5
        Dim name As String = "Charlie"

        Console.WriteLine("Age {0}, Name {1}", age, name)
    End Sub

End Class
```

```csharp
public class Animal
{
    int age;
    string name;

    [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId = "age")]
    private void PrintInfo()
    {
        int age = 5;
        string name = "Charlie";

        Console.WriteLine($"Age {age}, Name {name}");
    }
}
```

## <a name="global-level-suppressions"></a>グローバルレベルの抑制

マネージコード分析ツールは、 `SuppressMessage` アセンブリ、モジュール、型、メンバー、またはパラメーターレベルで適用される属性を調べます。 また、リソースと名前空間に対する違反も発生します。 これらの違反はグローバルレベルで適用される必要があり、スコープが設定され、対象となります。 たとえば、次のメッセージでは、名前空間違反が抑制されます。

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> スコープで警告を非表示にすると、 `namespace` 名前空間自体に対して警告が抑制されます。 名前空間内の型に対して警告が抑制されることはありません。

明示的なスコープを指定することで、任意の抑制を表現できます。 これらの抑制はグローバルレベルで有効である必要があります。 型を修飾することによって、メンバーレベルの抑制を指定することはできません。

明示的に指定されたユーザーソースにマップされないコンパイラで生成されたコードを参照するメッセージを抑制する唯一の方法は、グローバルレベルの抑制です。 たとえば、次のコードは、コンパイラによって生成されたコンストラクターに対する違反を抑制します。

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` 常に、完全修飾された項目名を含みます。

### <a name="global-suppression-file"></a>グローバル抑制ファイル

グローバル抑制ファイルは、グローバルレベルの抑制またはターゲットを指定しない抑制のいずれかである抑制を保持します。 たとえば、アセンブリレベルの違反の抑制は、このファイルに格納されます。 また、一部の ASP.NET 抑制は、フォームの分離コードではプロジェクトレベルの設定が使用できないため、このファイルに格納されます。 グローバル抑制ファイルが作成され、プロジェクトに追加されます。その際、[**エラー一覧**] ウィンドウで [**抑制**] コマンドの [**プロジェクトの抑制ファイルを**使用する] オプションを初めて選択します。

### <a name="module-suppression-scope"></a>モジュールの抑制スコープ

**モジュール**スコープを使用すると、アセンブリ全体のコード品質違反を抑制できます。

たとえば、 _globalsuppressions_ プロジェクトファイルの次の属性は、ASP.NET Core プロジェクトの ConfigureAwait 違反を抑制します。

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

## <a name="generated-code"></a>生成されたコード

マネージコードコンパイラと一部のサードパーティツールでは、コードの迅速な開発を容易にするコードが生成されます。 ソースファイルに表示されるコンパイラで生成されたコードは、通常、属性でマークされ `GeneratedCodeAttribute` ます。

ソースコード分析では、生成されたコード内のメッセージをファイル内で抑制でき `.editorconfig` ます。 詳細については、「 [生成されたコードを除外](/dotnet/fundamentals/code-analysis/configuration-options#exclude-generated-code)する」を参照してください。

レガシコード分析では、生成されたコードのコード分析の警告とエラーを非表示にするかどうかを選択できます。 このような警告やエラーを抑制する方法の詳細については、「 [方法: 生成されたコードの警告を非](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)表示にする」を参照してください。

> [!NOTE]
> コード分析 `GeneratedCodeAttribute` は、アセンブリ全体または単一のパラメーターのいずれかに適用されるときに無視されます。

## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [コードアナライザーを使用する](../code-quality/use-roslyn-analyzers.md)
