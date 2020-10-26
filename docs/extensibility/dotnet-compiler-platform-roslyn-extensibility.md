---
title: .NET Compiler Platform ( &quot; roslyn &quot; ) 拡張 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62ceac6e2be8a0a84d82f6b86b685c7c8b20a182
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712073"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET Compiler Platform ( &quot; roslyn &quot; ) 拡張性
.NET Compiler Platform ("Roslyn") の中核となる任務は、C# および Visual Basic コンパイラを起動し、ツールや開発者が豊富な情報コンパイラについての情報を共有できるようにすることです。 コード分析ツールを利用すると、コードの品質を向上させることができ、コードジェネレーターはアプリケーションの構築に役立ちます。 ツールがよりスマートになるにつれて、コンパイラだけが持っている深いコードの詳細にアクセスする必要があります。 Roslyn コンパイラは、非透過的なトランスレーター (およびオブジェクトコード内のソースコード) ではなく、ツールとアプリケーションのコード関連タスクに使用できる Api を提供します。

 ベストパートは、Roslyn コンパイラ、Api、サンプル、チュートリアル、およびこれらの Api の上に構築された実際のツールはすべて、 [github.com/dotnet/roslyn](https://github.com/dotnet/Roslyn)で完全にオープンソースであることです。 詳細については、OSS サイトにアクセスして、Roslyn の使用を開始してください。 エンドユーザーとして使用できる最新の C# および Visual Basic 機能を入手するためのリンクと、Roslyn Api を活用したツールビルダーとして開始するためのリンクを紹介します。

## <a name="see-also"></a>関連項目
- [Roslyn アナライザーを使ってみる](../extensibility/getting-started-with-roslyn-analyzers.md)
