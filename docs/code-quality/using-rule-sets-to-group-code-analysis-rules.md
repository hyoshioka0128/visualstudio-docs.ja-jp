---
title: コード分析規則セット
ms.date: 04/02/2018
description: Visual Studio code の分析における組み込みのルールセットとカスタマイズされたルールセットについて説明します。 「ファイルで規則セットを指定する方法」および「プロジェクトで規則セットを構成する方法」を参照してください。
ms.custom: SEO-VS-2020
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 49d17e8321aa6567a6ae0936291a73d5cb854b5c
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436889"
---
# <a name="use-rule-sets-to-group-code-analysis-rules"></a>規則セットを使用したコード分析規則のグループ化

Visual Studio でコード分析を構成するときに、組み込みの *規則セット* の一覧から選択できます。 ルールセットは、対象となる問題とそのプロジェクトの特定の条件を識別するコード分析ルールをグループ化したものです。 たとえば、公開されている Api のコードをスキャンするように設計された規則セットを適用できます。 また、使用可能なすべての規則を含む規則セットを適用することもできます。

ルールセットをカスタマイズするには、ルールを追加または削除するか、ルールの重大度を変更して **エラー一覧** で警告またはエラーとして表示されるようにします。 カスタマイズした規則セットで、特定の開発環境の要件を満たすことができます。 規則セットをカスタマイズすると、そのプロセスに役立つ検索とフィルター処理のツールがルールセットエディターに表示されます。

規則セットは、 [マネージコード分析](/dotnet/fundamentals/code-analysis/code-quality-rule-options)、 [マネージコードのレガシ分析](how-to-configure-code-analysis-for-a-managed-code-project.md)、および [C++ コード分析](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)に使用できます。

## <a name="rule-set-format"></a>規則セットの形式

ルールセットは、規則 *セットファイルで* XML 形式で指定されます。 ID と *アクション* で構成されるルールは、アナライザーの id とファイル内の名前空間によってグループ化されます。

規則セットファイルの内容は、次の XML のように *なり* ます。

```xml
<RuleSet Name="Rules for Hello World project" Description="These rules focus on critical issues for the Hello World app." ToolsVersion="10.0">
  <Localization ResourceAssembly="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.dll" ResourceBaseName="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.Localized">
    <Name Resource="HelloWorldRules_Name" />
    <Description Resource="HelloWorldRules_Description" />
  </Localization>
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1009" Action="Warning" />
    <Rule Id="CA1016" Action="Warning" />
    <Rule Id="CA1033" Action="Warning" />
  </Rules>
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1802" Action="Error" />
    <Rule Id="CA1814" Action="Info" />
    <Rule Id="CA1823" Action="None" />
    <Rule Id="CA2217" Action="Warning" />
  </Rules>
</RuleSet>
```

> [!TIP]
> グラフィカルな **ルールセットエディター** では、手動で [はなくルールセットを編集](../code-quality/working-in-the-code-analysis-rule-set-editor.md)する方が簡単です。

## <a name="specify-a-rule-set-for-a-project"></a>プロジェクトの規則セットを指定する

プロジェクトの規則セットは、Visual Studio プロジェクトファイルの **CodeAnalysisRuleSet** プロパティによって指定されます。 次に例を示します。

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

## <a name="see-also"></a>関連項目

- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)