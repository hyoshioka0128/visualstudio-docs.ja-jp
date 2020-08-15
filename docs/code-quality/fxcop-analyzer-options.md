---
title: FxCop analyzer の構成オプション
ms.date: 09/23/2019
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 7d6b56bec2174ca71cc66f5424b7bdc309330d95
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248800"
---
# <a name="rule-scope-options-for-fxcop-analyzers"></a>FxCop アナライザーの規則のスコープオプション

一部の FxCop analyzer ルールでは、コードベースのどの部分を適用すべきかを調整できます。 このページには、使用可能なスコープ構成オプション、許容される値、および適用できるルールが一覧表示されます。 これらのオプションを使用するには、 [Editorconfig ファイル](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)で指定します。

これらの構成オプションは、 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet パッケージのバージョン2.6.3 以降で使用できます。

> [!TIP]
> FxCopAnalyzers パッケージの特定のバージョンで使用できるすべてのオプションの一覧を表示するには、パッケージの*documentation*フォルダーにある*Analyzer Configuration.md*ファイルを参照してください。 ファイルは *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.fxcopanalyzers \ \\ \<version\> Configuration.md*にあります。 この構成ドキュメントファイルは、バージョン2.6.5 以降では、パッケージの各バージョンに含まれています。 次に、 *Analyzer Configuration.md* ファイルでオプションを記述する方法の例を示します。
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
