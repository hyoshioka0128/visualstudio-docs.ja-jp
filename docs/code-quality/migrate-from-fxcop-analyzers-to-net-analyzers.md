---
title: FxCop アナライザーから .NET アナライザーへの移行
ms.custom: SEO-VS-2020
description: FxCop アナライザーから .NET analyzer に移行する方法について説明します
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
manager: jillfra
ms.openlocfilehash: b62f99b296c0f9624079423d850029f804e5ebe4
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96112181"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>FxCop アナライザーから .NET アナライザーへの移行

.NET Compiler Platform によるソース分析 ("Roslyn") アナライザーは、マネージコードの [従来の分析](code-analysis-for-managed-code-overview.md) に代わるものです。 従来の分析 (FxCop) ルールの多くは、既にソースアナライザーとして書き換えられています。

Visual Studio 2019 16.8 と .NET 5.0 より前のリリースでは、これらのアナライザーは NuGet パッケージとして出荷さ `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)れています。

Visual Studio 2019 16.8 と .NET 5.0 以降、これらのアナライザーは [.NET SDK に含まれて](/dotnet/fundamentals/code-analysis/overview)います。 また、NuGet パッケージとして入手することもでき `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)ます。 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet パッケージはまもなく非推奨とされる予定です。

## <a name="migration-steps"></a>移行の手順

次の手順に従って、プロジェクトまたはソリューションをから .NET アナライザーに移行してください `Microsoft.CodeAnalysis.FxCopAnalyzers` 。

1. `Microsoft.CodeAnalysis.FxCopAnalyzers`NuGet パッケージのアンインストール

2. [.NET アナライザーの有効化またはインストール](install-net-analyzers.md)

3. 追加のルールを有効に `Microsoft.CodeAnalysis.NetAnalyzers` する: よりもはるかに控えめです `Microsoft.CodeAnalysis.FxCopAnalyzers` 。 FxCopAnalyzers パッケージとは異なり、 [既定ではビルド警告として有効になっ](/dotnet/fundamentals/code-analysis/overview#enabled-rules)ているいくつかの正確性規則があります。 [AnalysisMode](/dotnet/core/project-sdk/msbuild-props#analysismode) MSBuild プロパティをカスタマイズすることで、[追加のルールを有効に](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules)することができます。 たとえば、プロパティをに設定すると、 `AllEnabledByDefault` 既定では、適用可能なすべての CA 規則がビルド警告として有効になります。

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>関連項目

- [ソース コード分析と従来の分析](net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)
- [レガシ分析から .NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [.NET アナライザーの有効化またはインストール](install-net-analyzers.md)
- [.NET アナライザーに関する FAQ](net-analyzers-faq.md)
- [.NET アナライザーの構成](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
