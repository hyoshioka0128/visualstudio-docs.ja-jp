---
title: .NET コンパイラ&quot;プラットフォーム&quot;( Roslyn ) 拡張性 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62ceac6e2be8a0a84d82f6b86b685c7c8b20a182
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712073"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET コンパイラ&quot;プラットフォーム&quot;( Roslyn ) の拡張性
.NET コンパイラ プラットフォーム ("Roslyn") の中核的な使命は、C# と Visual Basic のコンパイラを開き、ツールと開発者がプログラムに関する豊富な情報を共有できるようにすることです。 コード分析ツールはコードの品質を向上させ、コード ジェネレーターはアプリケーションの構築に役立ちます。 ツールが賢くなるにつれて、コンパイラだけが持つより深いコード知識にアクセスする必要があります。 不透明なトランスレータ (ソース コードとオブジェクト コードアウト) ではなく、Roslyn コンパイラは、ツールやアプリケーションのコード関連タスクに使用できる API を提供します。

 最もよい部分は、Roslyn コンパイラ、その API、サンプル、およびチュートリアル、およびこれらの API の上に構築された実際のツールがすべて[github.com/dotnet/roslyn](https://github.com/dotnet/Roslyn)で完全にオープン ソースであるということです。 OSSサイトで詳細を確認し、Roslynを始めてください。 エンド ユーザーとして使用できる最新の C# 機能と Visual Basic 機能を入手するためのリンクと、Roslyn API を活用したツール ビルダーとしての開始リンクがあります。

## <a name="see-also"></a>関連項目
- [Roslyn アナライザーの使用を開始する](../extensibility/getting-started-with-roslyn-analyzers.md)
