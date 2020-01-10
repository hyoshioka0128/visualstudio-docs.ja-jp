---
title: デザイン時のアセンブリの解決 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild
ms.assetid: 20dae076-733e-49c1-a2e9-b336757ae21d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d46b2042755df9f9f0e1abcb43c07a5318c92593
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595151"
---
# <a name="resolve-assemblies-at-design-time"></a>デザイン時のアセンブリの解決
**[参照の追加]** ダイアログの **[.NET]** タブを使用してアセンブリへの参照を追加する場合、その参照は中間参照アセンブリを指します。つまり、すべての型情報と署名情報を含んでいるが、コードを必ずしも含まないアセンブリを指します。 **[.NET]** タブには、.NET Framework のランタイム アセンブリに対応する参照アセンブリの一覧が表示されます。 さらに、サードパーティによって使用される、登録済みの AssemblyFoldersEx フォルダーのランタイム アセンブリに対応する参照アセンブリの一覧も表示されます。

## <a name="multi-targeting"></a>マルチターゲット
 [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] では、共通言語ランタイム (CLR: Common Language Runtime) Version 2.0 または Version 4 で実行される複数のバージョンの .NET Framework を対象にすることができます。 これらのバージョンには、.NET Framework Version 2.0、3.0、3.5、4、4.5、4.5.1 および Silverlight Version 1.0、2.0、3.0 が含まれます。 CLR Version 2.0 または Version 4 に基づいた新しいバージョンの .NET Framework がリリースされた場合、この Framework はターゲット パックを使用してインストールでき、Visual Studio でターゲットとして自動的に表示されます。

## <a name="how-type-resolution-works"></a>型解決のしくみ
 CLR は、実行時に GAC、*bin* ディレクトリ、およびすべてのプローブ パスを調べることで、アセンブリ内の型を解決します。 これは、フュージョン ローダーによって処理されます。 では、フュージョン ローダーはどうやって調査対象を認識するのでしょうか。 これは、デザイン時、アプリケーションのビルド中に行われた解決によって異なります。

 ビルド中、コンパイラは参照アセンブリを使用してアプリケーションの型を解決します。 .NET Framework Version 2.0、3.0、3.5、4、4.5、4.5.1 では、参照アセンブリは .NET Framework のインストール時にインストールされます。

 参照アセンブリは、対応するバージョンの .NET Framework SDK に付属するターゲット パックによって提供されます。 Framework 自体が提供するのは、ランタイム アセンブリだけです。 アプリケーションをビルドするには、.NET Framework と、対応する .NET Framework SDK の両方をインストールする必要があります。

 特定の .NET Framework を対象とする場合、ビルド システムは、ターゲット パックの参照アセンブリを使用してすべての型を解決します。 実行時には、フュージョン ローダーにより、これらの型が通常は GAC 内にあるランタイム アセンブリに解決されます。

 参照アセンブリを使用できない場合、ビルド システムはランタイム アセンブリを使用してアセンブリの型を解決します。 GAC のランタイム アセンブリは、マイナー バージョン番号では区別されないため、間違ったアセンブリに解決される可能性があります。 この現象は、たとえば、.NET Framework Version 3.0 を対象としているのに、Version 3.5 で導入された新しいメソッドが参照されている場合に発生することがあります。 ビルドは成功し、アプリケーションはビルド コンピューターで動作しますが、Version 3.5 がインストールされていないコンピューターに配置すると正常に動作しなくなります。

 .NET Framework SDK に現在付属しているターゲット パックには、そのバージョンの Framework のすべてのランタイム アセンブリのリストが含まれています。これは再配布 (Redist) リストと呼ばれます。このリストによって、ビルド システムがアセンブリの間違ったバージョンに型を解決することはできなくなります。

## <a name="see-also"></a>関連項目
- [詳細な概念](../msbuild/msbuild-advanced-concepts.md)
