---
title: Roslyn アナライザーを使用したはじめにMicrosoft Docs
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc975ff4f142b85297c20f16ac399fce588c093b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80711275"
---
# <a name="get-started-with-roslyn-analyzers"></a>Roslyn アナライザーを使ってみる

Visual Studio のプロジェクトベースのコードアナライザーを使用すると、API の作成者は、NuGet パッケージの一部としてドメイン固有のコード分析を行うことができます。 これらのアナライザーは .NET Compiler Platform (コードネーム "Roslyn") を備えているので、行を完了する前に入力したコードに警告を生成することができます (問題を検出するためのコードのビルドを待機する必要はありません)。 また、アナライザーは、Visual Studio 電球のプロンプトを使用してコードを自動的に修正することもできます。これにより、コードをすぐにクリーンアップできます。

## <a name="get-started"></a>はじめに

[Roslyn アナライザーの概要](../code-quality/roslyn-analyzers-overview.md)

[チュートリアル: 最初のアナライザーとコード修正を作成する](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[コード修正の追加チュートリアル: アナライザーの問題についてユーザーに修正プログラムを提供する](https://msdn.microsoft.com/magazine/dn904670.aspx)

[リアルワールド Roslyn アナライザー](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md) 。[話す](https://channel9.msdn.com/events/Build/2015/3-725)こともできます。

[3種類のアナライザーにグループ化された GitHub のいくつかの例](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>関連項目

- [.NET compiler platform パッケージバージョンリファレンス](roslyn-version-support.md)
- [GitHub OSS サイトに関するその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [Roslyn アナライザーで実装された FxCop 規則](../code-quality/fxcop-rule-port-status.md)
