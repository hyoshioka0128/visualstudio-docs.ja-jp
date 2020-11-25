---
title: .NET アナライザーの有効化またはインストール
ms.date: 08/03/2018
description: .Net SDK から .NET アナライザーを有効にする方法、または NuGet パッケージとしてこれらのアナライザーをインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a14d89caba498a07c2447f9df1109e4da9f6a466
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96112173"
---
# <a name="enable-or-install-net-analyzers"></a>.NET アナライザーの有効化またはインストール

## <a name="overview"></a>概要

.NET のコンパイラ プラットフォーム (Roslyn) アナライザーでは、お使いの C# または Visual Basic コードについて、コード品質やコード スタイルに関する問題を検査できます。 これらのアナライザーは、次のいずれかの方法で有効またはインストールできます。

- **.NET sdk からの有効化**: Visual Studio 2019 16.8 と .Net 5.0 以降では、これらのアナライザーは [.net sdk に含まれて](/dotnet/fundamentals/code-analysis/overview)います。 .NET 5.0 以降を対象とするプロジェクトでは、既定で分析が有効になっています。 以前のバージョンの .NET を対象とするプロジェクトでコード分析を有効にするには、 `EnableNETAnalyzers` プロパティをに設定し `true` ます。 をに設定することにより、プロジェクトのコード分析を無効にすることもでき `EnableNETAnalyzers` `false` ます。

- **Nuget パッケージとしてインストール** する: または、 `Microsoft.CodeAnalysis.NetAnalyzers` Visual Studio 2019 に [nuget パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers) をインストールして、これらのアナライザーをインストールすることもできます。 Visual Studio 2017 を使用している場合は、最新 `2.9.x` バージョンの `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/)をインストールします。

> [!NOTE]
> `Microsoft.CodeAnalysis.NetAnalyzers`可能な場合は、 [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)をインストールするのではなく、.net SDK からアナライザーを有効にすることをお勧めします。 .NET SDK からアナライザーを有効にすると、SDK を更新するとすぐにアナライザーのバグ修正と新しいアナライザーが自動的に取得されるようになります。

## <a name="see-also"></a>関連項目

- [Visual Studio のコードアナライザーの概要](roslyn-analyzers-overview.md)
- [Visual Studio でコード アナライザーを使用する](use-roslyn-analyzers.md)
- [レガシ分析から .NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)
