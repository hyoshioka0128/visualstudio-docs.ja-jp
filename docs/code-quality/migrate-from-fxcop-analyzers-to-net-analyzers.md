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
manager: jmartens
ms.openlocfilehash: e435502587e65bd694567f4100516a91fa97cc0a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867868"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>FxCop アナライザーから .NET アナライザーへの移行

.NET Compiler Platform によるソース分析 ("Roslyn") アナライザーは、マネージコードの [従来の分析](code-analysis-for-managed-code-overview.md) に代わるものです。 従来の分析 (FxCop) ルールの多くは、既にソースアナライザーとして書き換えられています。

Visual Studio 2019 16.8 と .NET 5.0 より前のリリースでは、これらのアナライザーは NuGet パッケージとして出荷さ `Microsoft.CodeAnalysis.FxCopAnalyzers` [](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)れています。

Visual Studio 2019 16.8 と .NET 5.0 以降、これらのアナライザーは [.NET SDK に含まれて](/dotnet/fundamentals/code-analysis/overview)います。 .NET 5 + SDK に移行しない場合、または NuGet パッケージベースのモデルを使用する場合は、nuget パッケージでアナライザーを使用することもでき `Microsoft.CodeAnalysis.NetAnalyzers` [](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)ます。 オンデマンドバージョン更新には、パッケージベースのモデルを使用することをお勧めします。

> [!NOTE]
> ファーストパーティの .NET アナライザーは、ターゲットプラットフォームに依存しません。 つまり、プロジェクトは特定の .NET プラットフォームを対象にする必要がありません。 アナライザーは、、、など、以前のバージョンの .NET を対象とするプロジェクトに対して機能し `net5.0` `netcoreapp` `netstandard` `net472` ます。

## <a name="migration-steps"></a>移行の手順

バージョン以降 `3.3.2` で `Microsoft.CodeAnalysis.FxCopAnalyzers` は、NuGet パッケージは非推奨となりました。 次の手順に従って、プロジェクトまたはソリューションをから .NET アナライザーに移行してください `Microsoft.CodeAnalysis.FxCopAnalyzers` 。

1. `Microsoft.CodeAnalysis.FxCopAnalyzers`NuGet パッケージのアンインストール

2. [.Net アナライザーを有効またはインストール](install-net-analyzers.md)します。 プロジェクトのターゲットプラットフォームを変更する必要はないことに注意してください。

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
