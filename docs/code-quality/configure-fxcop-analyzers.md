---
title: Editorconfig を使用した .NET コード品質アナライザーの構成
ms.date: 09/01/2020
ms.topic: conceptual
helpviewer_keywords:
- .NET analyzers
- FxCop analyzers, configuring
- code quality
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: bc237082ec1188d71241facead975db1df2cf3af
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90035431"
---
# <a name="configure-net-code-quality-analysis-with-editorconfig"></a>EditorConfig を使用した .NET コード品質分析の構成

各コード品質アナライザー (規則 Id がで始まるもの `CA` ) は、構成可能なオプションを使用して、コードベースの部分に適用するように調整できます。 各オプションは、キーと値のペアを [Editorconfig](https://editorconfig.org) ファイルに追加することによって指定します。 構成ファイルは、ファイル、プロジェクト、ソリューション、またはリポジトリ全体に固有のものにすることができます。

> [!TIP]
> **ソリューションエクスプローラー**でプロジェクトを右クリックし、[ **Add**  >  **新しい項目**の追加] を選択して、プロジェクトに editorconfig ファイルを追加します。 [ **新しい項目の追加** ] ウィンドウで、検索ボックスに「 **editorconfig** 」と入力します。 [ **Editorconfig ファイル (既定)** ] テンプレートを選択し、[ **追加**] を選択します。
>
> ![Visual Studio で EditorConfig ファイルをプロジェクトに追加する](media/add-editorconfig-file.png)

::: moniker range=">=vs-2019"

規則の重要度の構成 (エラーや警告など) については、「 [EditorConfig ファイルで規則の重要度を設定](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)する」を参照してください。 または、組み込みの [Editorconfig ファイルまたはルールセット](analyzer-rule-sets.md) の1つを選択して、ルールのカテゴリをすばやく有効または無効にすることができます。

::: moniker-end

この記事の残りの部分では、.NET コード品質アナライザーが適用される場所を調整するオプションの一般的な構文について説明します。

## <a name="option-scopes"></a>オプションスコープ

各 [調整] オプションは、ルールのカテゴリ (セキュリティや設計など)、または特定のルールに対して、すべてのルールに対して構成できます。

### <a name="all-rules"></a>すべてのルール

*すべて*のルールのオプションを構成するための構文は次のとおりです。

|構文|例|
|-|-|
| dotnet_code_quality。OptionName = OptionValue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>ルールのカテゴリ

ルールの *カテゴリ* (名前付け、設計、パフォーマンスなど) のオプションを構成するための構文は次のとおりです。

|構文|例|
|-|-|
| dotnet_code_quality。RuleCategory OptionName = OptionValue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>特定のルール

*特定*のルールのオプションを構成するための構文は次のとおりです。

|構文|例|
|-|-|
| dotnet_code_quality。RuleId OptionName = OptionValue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="enabling-editorconfig-based-configuration"></a>EditorConfig ベースの構成を有効にする

EditorConfig ベースのアナライザーの構成は、次のスコープに対して有効にすることができます。

- 特定のドキュメント
- 特定のフォルダー
- 特定のプロジェクト
- 特定のソリューション
- リポジトリ全体

構成を有効にするには、対応するディレクトリのオプションを使用して、 *editorconfig* ファイルを追加します。 このファイルには、EditorConfig ベースの診断重大度構成エントリも含まれます。 詳細については、[こちら](use-roslyn-analyzers.md#configure-severity-levels)を参照してください。

## <a name="enable-a-category-of-rules"></a>ルールのカテゴリを有効にする

Analyzer パッケージには、定義済みの [Editorconfig](use-roslyn-analyzers.md#configure-severity-levels) ファイルや [ルールセット](using-rule-sets-to-group-code-analysis-rules.md) ファイルが含まれている場合があります。これにより、セキュリティや設計ルールなどのルールのカテゴリをすばやく簡単に有効にすることができます。 この [パッケージには](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) 、editorconfig ファイルとルールセットの両方が含まれています。 特定のカテゴリのルールを有効にすることで、対象となる問題と特定の条件を特定できます。

> [!NOTE]
> アナライザーの規則を有効にし、EditorConfig ファイルを使用して重要度を設定することは、Visual Studio 2019 バージョン16.3 以降でサポートされています。

NetAnalyzers NuGet パッケージには、次のルールカテゴリの定義済みの EditorConfig ファイルとルールセットが含まれています。

- すべてのルール
- データフロー
- デザイン
- ドキュメント
- グローバリゼーション
- 相互運用性
- 保守容易性
- 名前を付ける
- パフォーマンス
- FxCop からの移植
- [信頼性]
- セキュリティ
- 使用法

これらの規則の各カテゴリには、次のように EditorConfig ファイルまたは規則セットファイルがあります。

- カテゴリ内のすべてのルールを有効にします (他のすべてのルールを無効にします)。
- 各ルールの既定の重要度を使用し、既定の設定で有効にします (他のすべてのルールを無効にします)。

> [!TIP]
> [すべてのルール] カテゴリには、すべてのルールを無効にするための追加の EditorConfig ファイルまたはルールセットファイルがあります。 このファイルを使用すると、プロジェクト内のアナライザーの警告またはエラーがすぐに除去されます。

> [!TIP]
> 従来の "FxCop" 分析から .NET Compiler Platform ベースのコード分析に移行している場合は、EditorConfig ファイルとルールセットファイルを使用して、 [以前に使用したもの](rule-set-reference.md)と同様の規則の構成を引き続き使用することができます。

## <a name="predefined-editorconfig-files"></a>定義済みの EditorConfig ファイル

Nuget\packages\microsoft.codeanalysis.netanalyzers アナライザーパッケージの定義済みの EditorConfig ファイルは、 *% USERPROFILE% \\ . \\ \<version\> \ editorconfig*ディレクトリにあります。 たとえば、すべてのセキュリティ規則を有効にするための EditorConfig ファイルは、 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> \\ *にあります。

選択した editorconfig ファイルをプロジェクトのルートディレクトリにコピーします。

## <a name="predefined-rule-sets"></a>定義済みの規則セット

% USERPROFILE アナライザーパッケージの定義済みの規則セットファイルは、 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> *ディレクトリに格納されています。 たとえば、すべてのセキュリティ規則を有効にするための規則セットファイルは *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> *にあります。

1つ以上の規則セットをコピーし、Visual Studio プロジェクトが格納されているディレクトリまたは **ソリューションエクスプローラー**に直接貼り付けます。

また、 [定義済みの規則セット](how-to-create-a-custom-rule-set.md) を自分の好みに合わせてカスタマイズすることもできます。 たとえば、1つまたは複数のルールの重要度を変更して、 **エラー一覧**に違反がエラーまたは警告として表示されるようにすることができます。


## <a name="rule-scope-options-for-net-code-quality-analyzers"></a>.NET コード品質アナライザーの規則スコープオプション

[Editorconfig ファイル](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)でオプションを指定できます。 たとえば、次のオプションを指定できます。

> [!TIP]
> 使用可能なオプションの完全な一覧については、この [Analyzer Configuration.md ファイル](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)を参照してください。 次に、 *Analyzer Configuration.md* ファイルでオプションを記述する方法の例を示します。
>
> オプション名: `sufficient_IterationCount_for_weak_KDF_algorithm`\
> オプション値: 整数値 \
> 既定値: 構成可能な各規則に固有 (ほとんどの規則に対して既定では ' 10万 ') \
> 例: `dotnet_code_quality.CA5387.sufficient_IterationCount_for_weak_KDF_algorithm = 100000`

## <a name="api_surface"></a>api_surface

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 分析する API サーフェイスの部分 | `public`<br/>`internal` または `friend`<br/>`private`<br/>`all`<br/><br/>複数の値はコンマ (,) で区切ります | `public` | [CA1000](ca1000.md) [CA1003](ca1003.md) [CA1008](ca1008.md) [CA1010](ca1010.md)<br/>[CA1012](ca1012.md) [CA1024](ca1024.md) [CA1027](ca1027.md) [CA1028](ca1028.md)<br/>[CA1030](ca1030.md) [CA1036](ca1036.md) [CA1040](ca1040.md) [CA1041](ca1041.md)<br/>[CA1043](ca1043.md) [CA1044](ca1044.md) [CA1051](ca1051.md) [CA1052](ca1052.md)<br/>[CA1054](ca1054.md) [CA1055](ca1055.md) [CA1056](ca1056.md) [CA1058](ca1058.md)<br/>[CA1063](ca1063.md) [CA1708](ca1708.md) [CA1710](ca1710.md) [CA1711](ca1711.md)<br/>[CA1714](ca1714.md) [CA1715](ca1715.md) [CA1716](ca1716.md) [CA1717](ca1717.md)<br/>[CA1720](ca1720.md) [CA1721](ca1721.md) [CA1725](ca1725.md) [CA1801](ca1801.md)<br/>[CA1802](ca1802.md) [CA1815](ca1815.md) [CA1819](ca1819.md) [CA2217](ca2217.md)<br/>[CA2225](ca2225.md) [CA2226](ca2226.md) [CA2231](ca2231.md) [CA2234](ca2234.md)<br/>|

## <a name="exclude_async_void_methods"></a>exclude_async_void_methods

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 値を返さない非同期メソッドを無視するかどうか | `true`<br/>`false` | `false` | [CA2007](ca2007.md) |

> [!NOTE]
> バージョン2.6.3 以前のアナライザーパッケージでは、このオプションの名前は `skip_async_void_methods` です。

## <a name="exclude_single_letter_type_parameters"></a>exclude_single_letter_type_parameters

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 1文字の [型パラメーター](/dotnet/csharp/programming-guide/generics/generic-type-parameters) をルールから除外するかどうか (例 `S` :) `Collection<S>` | `true`<br/>`false` | `false` | [CA1715](ca1715.md) |

> [!NOTE]
> バージョン2.6.3 以前のアナライザーパッケージでは、このオプションの名前は `allow_single_letter_type_parameters` です。

## <a name="output_kind"></a>output_kind

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| この型のアセンブリを生成するプロジェクト内のコードを分析する必要があることを指定します。 | 列挙体の1つまたは複数のフィールド <xref:Microsoft.CodeAnalysis.OutputKind><br/><br/>複数の値はコンマ (,) で区切ります | すべての出力の種類 | [CA2007](ca2007.md) |

## <a name="required_modifiers"></a>required_modifiers

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 分析する必要がある Api の必須の修飾子を指定します | 以下の許可された修飾子テーブルの1つ以上の値<br/><br/>複数の値はコンマ (,) で区切ります | 各規則に依存 | [CA1802](ca1802.md) |

| 許可される修飾子 | まとめ |
| --- | --- |
| `none` | 修飾子の要件はありません |
| `static` または `Shared` | ' Static ' (Visual Basic では ' Shared ') として宣言されなければなりません |
| `const` | ' Const ' として宣言されなければなりません |
| `readonly` | ' Readonly ' として宣言されなければなりません |
| `abstract` | ' Abstract ' として宣言されなければなりません |
| `virtual` | ' Virtual ' として宣言されなければなりません |
| `override` | ' Override ' として宣言されなければなりません |
| `sealed` | ' Sealed ' として宣言されなければなりません |
| `extern` | ' Extern ' として宣言されなければなりません。 |
| `async` | ' Async ' として宣言されなければなりません |

## <a name="exclude_extension_method_this_parameter"></a>exclude_extension_method_this_parameter

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 拡張メソッドのパラメーターの分析をスキップするかどうか `this` | `true`<br/>`false` | `false` | [CA1062](ca1062.md) |

## <a name="null_check_validation_methods"></a>null_check_validation_methods

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| メソッドに渡された引数を検証する null チェック検証メソッドの名前が null 以外である | 許可するメソッド名の形式 (で区切る `|` ):<br/> -メソッド名のみ (包含する型または名前空間に関係なく、という名前のすべてのメソッドが含まれます)<br/> -省略可能なプレフィックスを持つシンボルの[ドキュメント ID 形式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)の完全修飾名 `M:` | なし | [CA1062](ca1062.md) |

## <a name="additional_string_formatting_methods"></a>additional_string_formatting_methods

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 追加の文字列書式指定メソッドの名前 | 許可するメソッド名の形式 (で区切る `|` ):<br/> -メソッド名のみ (包含する型または名前空間に関係なく、という名前のすべてのメソッドが含まれます)<br/> -省略可能なプレフィックスを持つシンボルの[ドキュメント ID 形式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)の完全修飾名 `M:` | なし | [CA2241](ca2241.md) |

## <a name="excluded_type_names_with_derived_types"></a>excluded_type_names_with_derived_types

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 型の名前 (型とそのすべての派生型が分析に対して除外される) | 使用できるシンボル名の形式 (で区切る `|` ):<br/> -型名のみ (包含する型または名前空間に関係なく、名前を持つすべての型を含む)<br/> -省略可能なプレフィックスを持つシンボルの[ドキュメント ID 形式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)の完全修飾名 `T:` | なし | [CA1303](ca1303.md) |

## <a name="excluded_symbol_names"></a>excluded_symbol_names

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 分析に対して除外されるシンボルの名前 | 使用できるシンボル名の形式 (で区切る `|` ):<br/> -シンボル名のみ (包含する型または名前空間に関係なく、名前の付いたすべての記号が含まれます)<br/> -シンボルの [ドキュメント ID 形式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)の完全修飾名。 各シンボル名には、記号の種類のプレフィックスが必要です。たとえば、メソッドのプレフィックス "M:"、型のプレフィックス "T:"、名前空間のプレフィックス "N:" などです。<br/> - `.ctor` コンストラクターと `.cctor` 静的コンストラクターの場合 | なし | [CA1062](ca1062.md) [CA1303](ca1303.md) [CA2000](ca2000.md) [CA2100](ca2100.md) [CA2301](ca2301.md) [CA2302](ca2302.md)<br/>[CA2311](ca2311.md) [CA2312](ca2312.md) [CA2321](ca2321.md) [CA2322](ca2322.md) [CA2327](ca2327.md) [CA2328](ca2328.md)<br/>[CA2329](ca2329.md) [CA2330](ca2330.md) [CA3001](ca3001.md) [CA3002](ca3002.md) [CA3003](ca3003.md) [CA3004](ca3004.md)<br/>[CA3005](ca3005.md) [CA3006](ca3006.md) [CA3007](ca3007.md) [CA3008](ca3008.md) [CA3009](ca3009.md) [CA3010](ca3010.md)<br/>[CA3011](ca3011.md) [CA3012](ca3012.md) [CA5361](ca5361.md) CA5376 CA5377 [CA5378](ca5378.md)<br/>[CA5380](ca5380.md) [CA5381](ca5381.md) CA5382 CA5383 CA5384 CA5387<br/>CA5388 [CA5389](ca5389.md) CA5390 |

## <a name="disallowed_symbol_names"></a>disallowed_symbol_names

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 分析のコンテキストで禁止されているシンボルの名前 | 使用できるシンボル名の形式 (で区切る `|` ):<br/> -シンボル名のみ (包含する型または名前空間に関係なく、名前の付いたすべての記号が含まれます)<br/> -シンボルの [ドキュメント ID 形式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)の完全修飾名。 各シンボル名には、記号の種類のプレフィックスが必要です。たとえば、メソッドのプレフィックス "M:"、型のプレフィックス "T:"、名前空間のプレフィックス "N:" などです。<br/> - `.ctor` コンストラクターと `.cctor` 静的コンストラクターの場合 | なし | [CA1031](ca1031.md) |

## <a name="see-also"></a>参照

- [アナライザーの構成](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [EditorConfig の .NET コーディング規則](../ide/editorconfig-code-style-settings-reference.md)
