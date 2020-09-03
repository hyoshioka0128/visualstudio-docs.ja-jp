---
title: Roslyn アナライザーを使用したはじめにMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a712697bafefcf115ce10d110c0ef3a4270c6acd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "81444983"
---
# <a name="getting-started-with-roslyn-analyzers"></a>Roslyn アナライザーの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のプロジェクトベースのコードアナライザーを使用すると、API の作成者は、NuGet パッケージの一部としてドメイン固有のコード分析を行うことができます。  これらのアナライザーは .NET Compiler Platform (コードネーム "Roslyn") を備えているので、行を完了する前に入力したコードに警告を生成することができます (問題を検出するためのコードのビルドを待機する必要はありません)。  また、アナライザーは、Visual Studio 電球のプロンプトで自動的にコードを修正することもできます。これにより、コードをすぐにクリーンアップできるようになります。

## <a name="getting-started"></a>作業の開始
[Roslyn ライブコードアナライザーの概要とチュートリアル](https://msdn.microsoft.com/magazine/dn879356.aspx)

[コード修正の追加チュートリアル: アナライザーの問題に対するユーザー修正の提供](https://msdn.microsoft.com/magazine/dn904670.aspx)

[実際のアナライザーの概要とチュートリアル](https://channel9.msdn.com/events/Build/2015/3-725)

[リアルワールド Roslyn アナライザー](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md) 。[話す](https://channel9.msdn.com/events/Build/2015/3-725)こともできます。

[3種類のアナライザーにグループ化された GitHub のいくつかの例](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

[いくつかのアナライザーの概要とツアー](https://channel9.msdn.com/Events/dotnetConf/2015/NET-Compiler-Platform-Roslyn-Analyzers-and-the-Rise-of-Code-Aware-Libraries)

## <a name="other-resources"></a>その他の参照情報
[GitHub OSS サイトに関するその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)

[GitHub で Roslyn アナライザーを使用して実装された FxCop 規則](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
