---
title: Projects |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
caps.latest.revision: 44
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a251af12ccf4be5f0f48f789ac59fedaed3299b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183948"
---
# <a name="projects"></a>プロジェクト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio では、プロジェクトは、 **ソリューションエクスプローラー**に表示されるソースコードファイルやその他のリソースを整理するために開発者が使用するコンテナーです。 通常、プロジェクトは、ソースコードファイルと、ビットマップファイルなどのリソースへの参照を格納するファイル (C# プロジェクトの .csproj ファイルなど) です。 プロジェクトを使用すると、ソースコード、Web サービスおよびデータベースへの参照、およびその他のリソースを整理、ビルド、デバッグ、および配置できます。 Vspackage は、 *プロジェクトの種類*、 *プロジェクトのサブタイプ*、および *カスタムツール*という3つの主な方法で Visual Studio プロジェクトシステムを拡張できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [プロジェクトの種類](../../extensibility/internals/project-types.md)  
 *プロジェクトの種類* では、プログラミング言語など、新しい種類のプロジェクトのサポートが追加されます。 たとえば、Visual Studio がサポートする各言語には独自のプロジェクトの種類があり、IronPython 統合サンプルには IronPython 言語のプロジェクトの種類が含まれています。 項目のビルド、デバッグ、配置、 **ソリューションエクスプローラー**での表示方法をカスタマイズするには、C# または Visual Basic 以外の言語のプロジェクトの種類を作成する必要があります。 詳細については、「 [プロジェクトの種類](../../extensibility/internals/project-types.md)」を参照してください。  
  
 [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)  
 プロジェクトの*サブタイプ*はプロジェクトの種類に基づいており、プロジェクトのビルド、デバッグ、および配置の方法をカスタマイズするために使用できます。 Visual Studio は、スマートデバイスプロジェクトでプロジェクトのサブタイプを使用します。開発用コンピューターからターゲットデバイスに新しくビルドされたプログラムをコピーすることによって、展開をカスタマイズします。 C# および Visual Basic プロジェクトの種類は、プロジェクトのサブタイプの基礎として使用できます。C++ プロジェクトの種類はできません。 プロジェクトのサブタイプの基礎として、独自のプロジェクトの種類を使用することもできます。 詳細については、「 [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。  
  
 [Web プロジェクト](../../extensibility/internals/web-projects.md)  
 Web アプリケーションを作成する Web プロジェクトについて説明します。  
  
 [新しいプロジェクトの生成: 内部、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) 、 [新しいプロジェクトの生成: 内部、パート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)  
 新しいプロジェクトを作成するときに実際に行われることについて説明します。  
  
 [VSSDK のサンプル](../../misc/vssdk-samples.md)  
 プロジェクトとソリューションを処理する VSSDK のサンプルについて説明します。  
  
## <a name="related-sections"></a>関連項目  
 [Visual Studio SDK の内部](../../extensibility/internals/inside-the-visual-studio-sdk.md)  
 Visual Studio の機能拡張のさまざまな側面について説明します。
