---
title: Editorconfig を使用して .NET コード品質アナライザーを構成する
ms.date: 09/23/2019
ms.topic: conceptual
helpviewer_keywords:
- .NET analyzers
- FxCop analyzers, configuring
- code quality
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fbd30859c5ee3dbbea80c6d88d68c0211da62c88
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88706582"
---
# <a name="configure-net-code-quality-analyzers"></a>.NET コード品質アナライザーの構成

特定の .NET コード品質アナライザー (規則 Id がから始まるもの) については `CA` 、 [構成可能なオプション](fxcop-analyzer-options.md)を使用して、コードベースのどの部分を適用するかを調整できます。 各オプションは、キーと値のペアを [Editorconfig](https://editorconfig.org) ファイルに追加することによって指定します。 構成ファイルは、ファイル、プロジェクト、ソリューション、またはリポジトリ全体に固有のものにすることができます。

> [!TIP]
> **ソリューションエクスプローラー**でプロジェクトを右クリックし、[ **Add**  >  **新しい項目**の追加] を選択して、プロジェクトに editorconfig ファイルを追加します。 [ **新しい項目の追加** ] ウィンドウで、検索ボックスに「 **editorconfig** 」と入力します。 [ **Editorconfig ファイル (既定)** ] テンプレートを選択し、[ **追加**] を選択します。
>
> ![Visual Studio で editorconfig ファイルをプロジェクトに追加する](media/add-editorconfig-file.png)

::: moniker range=">=vs-2019"

規則の重要度の構成 (エラーや警告など) については、「 [EditorConfig ファイルで規則の重要度を設定](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)する」を参照してください。 または、組み込みの [Editorconfig ファイルまたはルールセット](analyzer-rule-sets.md) の1つを選択して、ルールのカテゴリをすばやく有効または無効にすることができます。

::: moniker-end

この記事の残りの部分では、.NET コード品質アナライザーが適用される場所を [調整するオプション](fxcop-analyzer-options.md) の一般的な構文について説明します。

## <a name="option-scopes"></a>オプションスコープ

各 [調整] オプションは、ルールのカテゴリ (名前付けや設計など)、または特定のルールに対して、すべてのルールに対して構成できます。

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

## <a name="enabling-editorconfig-based-configuration"></a>Editorconfig ベースの構成を有効にする

EditorConfig ベースのアナライザーの構成は、次のスコープに対して有効にすることができます。

- 特定のドキュメント
- 特定のフォルダー
- 特定のプロジェクト
- 特定のソリューション
- リポジトリ全体

構成を有効にするには、対応するディレクトリのオプションを使用して、 *editorconfig* ファイルを追加します。 このファイルには、EditorConfig ベースの診断重大度構成エントリも含まれます。 詳細については、[こちら](use-roslyn-analyzers.md#rule-severity)を参照してください。

## <a name="see-also"></a>関連項目

- [.NET コード品質アナライザーの規則スコープオプション](fxcop-analyzer-options.md)
- [アナライザーの構成](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [EditorConfig の .NET コーディング規則](../ide/editorconfig-code-style-settings-reference.md)
