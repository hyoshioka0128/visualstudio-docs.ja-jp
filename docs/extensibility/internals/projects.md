---
title: Projects |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bfe172d0255a6874d65fb940afd0f6f0beb1657a
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848801"
---
# <a name="projects"></a>Projects
Visual Studio では、プロジェクトは、**ソリューションエクスプローラー**に表示されるソースコードファイルやその他のリソースを整理するために開発者が使用するコンテナーです。 通常、プロジェクトは、ソースコードファイルと、ビットマップファイルなどのリソースC#への参照を格納するファイル (たとえば、プロジェクトの .csproj ファイル) です。 プロジェクトを使用すると、ソースコード、Web サービスおよびデータベースへの参照、およびその他のリソースを整理、ビルド、デバッグ、および配置できます。 Vspackage は、*プロジェクトの種類*、*プロジェクトのサブタイプ*、および*カスタムツール*という3つの主な方法で Visual Studio プロジェクトシステムを拡張できます。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクト タイプ](../../extensibility/internals/project-types.md)

 *プロジェクトの種類*では、プログラミング言語など、新しい種類のプロジェクトのサポートが追加されます。 たとえば、Visual Studio がサポートする各言語には独自のプロジェクトの種類があり、IronPython 統合サンプルには IronPython 言語のプロジェクトの種類が含まれています。 項目のビルド、デバッグ、配置、**ソリューションエクスプローラー**でC#の表示方法をカスタマイズするには、または Visual Basic 以外の言語のプロジェクトの種類を作成する必要があります。 詳細については、「[プロジェクトの種類](../../extensibility/internals/project-types.md)」を参照してください。

- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)

 プロジェクトの*サブタイプ*はプロジェクトの種類に基づいており、プロジェクトのビルド、デバッグ、および配置の方法をカスタマイズするために使用できます。 Visual Studio は、スマートデバイスプロジェクトでプロジェクトのサブタイプを使用します。開発用コンピューターからターゲットデバイスに新しくビルドされたプログラムをコピーすることによって、展開をカスタマイズします。 C#および Visual Basic プロジェクトの種類は、プロジェクトのサブタイプの基礎として使用できます。C++プロジェクトの種類はできません。 プロジェクトのサブタイプの基礎として、独自のプロジェクトの種類を使用することもできます。 詳細については、「[プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

- [Web プロジェクト](../../extensibility/internals/web-projects.md)

 Web アプリケーションを作成する Web プロジェクトについて説明します。

- [新しいプロジェクトの生成: 内部、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) 、[新しいプロジェクトの生成: 内部、パート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 新しいプロジェクトを作成するときに実際に行われることについて説明します。

- [Vssdk のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)プロジェクトとソリューションを処理する VSSDK のサンプルが含まれています。

## <a name="related-sections"></a>関連セクション
- [Visual Studio SDK の内部](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 Visual Studio の機能拡張のさまざまな側面について説明します。
