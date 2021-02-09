---
title: FxCop からソース分析への移行 (.NET アナライザー)
ms.custom: SEO-VS-2020
description: コードを初めて分析する方法、またはバイナリ分析 (FxCop) から、ソース分析を使用してマネージコードを分析する新しい方法 (.NET アナライザー) に移行する方法について説明します。
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 96a0c0b7fa1f2c703cefde31070ed98c5edddcb6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859763"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-net-analyzers"></a>レガシ分析 (FxCop) からソース分析への移行 (.NET アナライザー)

.NET Compiler Platform によるソース分析 ("Roslyn") アナライザーは、マネージコードの [従来の分析](../code-quality/code-analysis-for-managed-code-overview.md) に代わるものです。 .NET Core や .NET Standard プロジェクトなどの新しいプロジェクトテンプレートでは、レガシ分析は使用できません。

従来の分析 (FxCop) 規則の多くは、.NET アナライザー (Roslyn コードアナライザーのセット) に対して既に書き直しられています。 Roslyn アナライザーは、コンパイラの実行中にソースコードに基づく分析を実行します。 アナライザーの結果は、コンパイラーの結果と共に報告されます。

レガシ分析とソース分析の相違点の詳細については、次を参照してください。

- [ソース コード分析と従来の分析](../code-quality/net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)

- [.NET アナライザーに関する FAQ](../code-quality/net-analyzers-faq.md)

## <a name="migration"></a>移行

ソース分析に移行するに [は、.net アナライザーを有効にするかインストール](install-net-analyzers.md)します。 従来の分析のルール違反と同様に、ソース コード分析の違反は Visual Studio の [エラー一覧] ウィンドウに表示されます。 さらに、ソース コード分析の違反は、コード エディターで問題のあるコードの下に "*波線*" としても示されます。 波線の色は、ルールの[重要度設定](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)によって異なります。 新しい .NET アナライザーに移植された規則の状態を確認するには、「移植された [規則およびアン移植](../code-quality/fxcop-rule-port-status.md)された規則」を参照してください。

> [!NOTE]
> Visual Studio 2019 16.8 と .NET 5.0 より前のリリースでは、これらのアナライザーは NuGet パッケージとして出荷さ `Microsoft.CodeAnalysis.FxCopAnalyzers` [](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)れています。 Visual Studio 2019 16.8 と .NET 5.0 以降、これらのアナライザーは [.NET SDK に含まれて](/dotnet/fundamentals/code-analysis/overview)います。 また、NuGet パッケージとして入手することもでき `Microsoft.CodeAnalysis.NetAnalyzers` [](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)ます。 詳細については、「 [FxCop アナライザーから .net アナライザーへの移行」を](migrate-from-fxcop-analyzers-to-net-analyzers.md)参照してください。

## <a name="configuration"></a>構成

.NET アナライザーの構成方法の詳細については、次を参照してください。

- .NET アナライザーを構成するには、「 [.net アナライザーの構成](/dotnet/fundamentals/code-analysis/code-quality-rule-options)」を参照してください。

- EditorConfig またはルールセットファイルで定義済みのルールを使用してアナライザーを構成する方法については、「 [ルールのカテゴリを有効に](/dotnet/fundamentals/code-analysis/code-quality-rule-options)する」を参照してください。

## <a name="see-also"></a>関連項目

- [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)
