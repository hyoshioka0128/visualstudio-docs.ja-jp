---
title: プロジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b7a9299321d2aa80eebb564bf9b926f07ab0108
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706213"
---
# <a name="projects"></a>プロジェクト
Visual Studio では、プロジェクトは、**開発者がソリューション エクスプローラー**に表示されるソース コード ファイルやその他のリソースを整理するために使用するコンテナーです。 通常、プロジェクトは、ソース コード ファイルやビットマップ ファイルなどのリソースへの参照を格納するファイル (たとえば、C# プロジェクトの .csproj ファイル) です。 プロジェクトを使用すると、ソース コード、Web サービスやデータベース、およびその他のリソースを整理、ビルド、デバッグ、および配置できます。 VSPackages は、Visual Studio プロジェクト システムを、*プロジェクトの種類*、*プロジェクト サブタイプ*、および*カスタム ツール*の 3 つの主要な方法で拡張できます。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 *プロジェクトの種類*は、プログラミング言語などの新しい種類のプロジェクトのサポートを追加します。 たとえば、Visual Studio がサポートする各言語には独自のプロジェクトの種類があり、IronPython 統合サンプルには IronPython 言語用のプロジェクト の種類が含まれています。 **C#** または Visual Basic 以外の言語用のプロジェクトの種類を作成して、ソリューション エクスプローラでの項目のビルド、デバッグ、配置、および表示方法をカスタマイズする必要があります。 詳細については、「[プロジェクトの種類](../../extensibility/internals/project-types.md)」を参照してください。

- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)

 *プロジェクトのサブタイプ*はプロジェクトの種類に基づいており、プロジェクトのビルド、デバッグ、および配置方法をカスタマイズするために使用できます。 Visual Studio では、スマート デバイス プロジェクトでプロジェクト サブタイプが使用されます。開発用コンピューターからターゲット デバイスに新しく構築されたプログラムをコピーして、展開をカスタマイズします。 C# および Visual Basic プロジェクトの種類は、プロジェクトのサブタイプの基礎として使用できます。C++ プロジェクトの種類はできません。 独自のプロジェクト タイプは、プロジェクト のサブタイプの基礎として使用することもできます。 詳細については、「[プロジェクト のサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

- [Web プロジェクト](../../extensibility/internals/web-projects.md)

 Web プロジェクトについて説明します。

- [新しいプロジェクト生成:ボンネットの下で、パート1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)と[新しいプロジェクト生成:ボンネットの下で、パート2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 新しいプロジェクトを作成するときに実際に発生する現象について説明します。

- [VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)プロジェクトとソリューションを扱う VSSDK のサンプルが含まれています。

## <a name="related-sections"></a>関連項目
- [Visual Studio SDK の内部](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 Visual Studio の機能拡張のさまざまな側面について説明する。
