---
title: Roslyn アナライザーの使用開始 |マイクロソフトドキュメント
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc975ff4f142b85297c20f16ac399fce588c093b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711275"
---
# <a name="get-started-with-roslyn-analyzers"></a>Roslyn アナライザーの使用を開始する

Visual Studio のプロジェクト ベースのライブ コード アナライザーを使用すると、API の作成者は、NuGet パッケージの一部としてドメイン固有のコード分析を出荷できます。 これらのアナライザーは .NET コンパイラ プラットフォーム (コード名 "Roslyn") によって供給されるため、行を終了する前に入力するとコードに警告が出力されます (問題を検出するためにコードのビルドを待つ必要はありません)。 アナライザーは、Visual Studio 電球プロンプトを使用して自動コード修正を表示して、コードをすぐにクリーンアップすることもできます。

## <a name="get-started"></a>はじめに

[ロスリンアナライザの概要](../code-quality/roslyn-analyzers-overview.md)

[チュートリアル: 最初のアナライザーとコード修正を作成する](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[コード修正の追加 チュートリアル: アナライザーの問題に対するユーザーの修正を提供する](https://msdn.microsoft.com/magazine/dn904670.aspx)

あなたも[トーク](https://channel9.msdn.com/events/Build/2015/3-725)として見ることができる[現実世界のロスリンアナライザ](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)

[GitHub のいくつかの例は、3 種類のアナライザーにグループ化されています。](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>関連項目

- [.NET コンパイラ プラットフォーム パッケージのバージョン リファレンス](roslyn-version-support.md)
- [GitHub OSS サイトのその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [ロスリン アナライザーで実装された FxCop ルール](../code-quality/fxcop-rule-port-status.md)
