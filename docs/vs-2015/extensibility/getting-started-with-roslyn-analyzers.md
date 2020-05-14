---
title: Roslyn アナライザーの使用開始 |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a712697bafefcf115ce10d110c0ef3a4270c6acd
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444983"
---
# <a name="getting-started-with-roslyn-analyzers"></a>Roslyn アナライザーの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のプロジェクト ベースのライブ コード アナライザーを使用すると、API の作成者は、NuGet パッケージの一部としてドメイン固有のコード分析を出荷できます。  これらのアナライザーは .NET コンパイラ プラットフォーム (コード名 "Roslyn") によって供給されるため、行を終了する前に入力するとコードに警告が出力されます (問題を検出するためにコードのビルドを待つ必要はありません)。  アナライザーは、Visual Studio 電球プロンプトを使用して自動コード修正を表示して、コードをすぐにクリーンアップすることもできます。

## <a name="getting-started"></a>作業の開始
[Roslyn ライブ コード アナライザーの概要とチュートリアル](https://msdn.microsoft.com/magazine/dn879356.aspx)

[コード修正の追加 チュートリアル: アナライザーの問題に対するユーザーの修正プログラムの提供](https://msdn.microsoft.com/magazine/dn904670.aspx)

[実世界アナライザートークの紹介とチュートリアル](https://channel9.msdn.com/events/Build/2015/3-725)

あなたも[トーク](https://channel9.msdn.com/events/Build/2015/3-725)として見ることができる[リアルワールドロスリンアナライザ](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md)

[GitHub のいくつかの例は、3 種類のアナライザーにグループ化されています。](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

[いくつかのアナライザーの概要とツアー](https://channel9.msdn.com/Events/dotnetConf/2015/NET-Compiler-Platform-Roslyn-Analyzers-and-the-Rise-of-Code-Aware-Libraries)

## <a name="other-resources"></a>その他のリソース
[GitHub OSS サイトのその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)

[GitHub のロズリン アナライザーで実装された FxCop ルール](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
