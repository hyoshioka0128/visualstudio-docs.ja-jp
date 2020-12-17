---
title: ファーストパーティの .NET アナライザーを有効またはインストールする
ms.date: 08/03/2018
description: .NET SDK からファーストパーティの .NET analyzer を有効にする方法、または NuGet パッケージとしてこれらのアナライザーをインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ea13fde64f6214cf3c219de45c79458b75e1caf8
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97615526"
---
# <a name="enable-or-install-first-party-net-analyzers"></a>ファーストパーティの .NET アナライザーを有効またはインストールする

## <a name="overview"></a>概要

.NET のコンパイラ プラットフォーム (Roslyn) アナライザーでは、お使いの C# または Visual Basic コードについて、コード品質やコード スタイルに関する問題を検査できます。 ファーストパーティの .NET アナライザーは、 **ターゲットプラットフォームに依存** しません。 つまり、プロジェクトは特定の .NET プラットフォームを対象にする必要がありません。 アナライザーは、、、など、以前のバージョンの .NET を対象とするプロジェクトに対して機能し `net5.0` `netcoreapp` `netstandard` `net472` ます。

ファーストパーティの .NET analyzer は、次のいずれかの方法で有効にしたりインストールしたりできます。

- **.NET sdk からの有効化**: Visual Studio 2019 16.8 と .Net 5.0 以降では、これらのアナライザーは [.net sdk に含まれて](/dotnet/fundamentals/code-analysis/overview)います。 .NET 5.0 以降を対象とするプロジェクトでは、既定で分析が有効になっています。 以前のバージョンの .NET を対象とするプロジェクトでコード分析を有効にするには、 `EnableNETAnalyzers` プロパティをに設定し `true` ます。 をに設定することにより、プロジェクトのコード分析を無効にすることもでき `EnableNETAnalyzers` `false` ます。

- **Nuget パッケージとしてインストール** する: .net 5 + SDK に移行しない場合、または nuget パッケージベースのモデルを希望する場合は、 `Microsoft.CodeAnalysis.NetAnalyzers` Visual Studio 2019 の [nuget パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers) でアナライザーを使用することもできます。  オンデマンドバージョン更新には、パッケージベースのモデルを使用することをお勧めします。 Visual Studio 2017 を使用している場合は、 `2.9.x` 代わりに最新バージョンの `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) をインストールしてください。

> [!NOTE]
> `Microsoft.CodeAnalysis.NetAnalyzers`可能な場合は、 [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)をインストールするのではなく、.net SDK からアナライザーを有効にすることをお勧めします。 .NET SDK からアナライザーを有効にすると、SDK を更新するとすぐにアナライザーのバグ修正と新しいアナライザーが自動的に取得されるようになります。 NuGet モデルでは、最新のバグ修正が必要になるたびに NuGet パッケージを更新する必要があります。 NuGet パッケージがより頻繁に更新されます。

## <a name="see-also"></a>関連項目

- [Visual Studio のコードアナライザーの概要](roslyn-analyzers-overview.md)
- [Visual Studio でコード アナライザーを使用する](use-roslyn-analyzers.md)
- [レガシ分析から .NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)
