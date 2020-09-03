---
title: ソース管理 VSPackage Architecture |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3cca9e39714f87024b01ab2c925189aacbe22785
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183404"
---
# <a name="source-control-vspackage-architecture"></a>ソース管理 VSPackage アーキテクチャ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理パッケージは、IDE によって提供されるサービスを使用する VSPackage です [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 戻り値として、ソース管理パッケージの機能がソース管理サービスとして提供されます。 また、ソース管理パッケージは、ソース管理をに統合するためのソース管理プラグインよりも汎用性の高い方法です [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 ソース管理プラグイン API を実装するソース管理プラグインは、厳密なコントラクトに準拠しています。 たとえば、既定の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ユーザーインターフェイス (UI) をプラグインで置き換えることはできません。 さらに、ソース管理プラグイン API では、プラグインが独自のソース管理モデルを実装することはできません。 ただし、ソース管理パッケージでは、これらの両方の制限が解消します。 ソース管理パッケージは、ユーザーのソース管理エクスペリエンスを完全に制御 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] できます。 さらに、ソース管理パッケージは、独自のソース管理モデルとロジックを使用して、ソース管理に関連するすべてのユーザーインターフェイスを定義できます。  
  
## <a name="source-control-package-components"></a>ソース管理パッケージのコンポーネント  
 アーキテクチャ図に示されているように、ソース管理 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] スタブという名前のコンポーネントは、ソース管理パッケージとを統合する VSPackage です [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 ソース管理スタブは、次のタスクを処理します。  
  
- ソース管理のパッケージ登録に必要な共通の UI を提供します。  
  
- ソース管理パッケージを読み込みます。  
  
- ソース管理パッケージをアクティブ/非アクティブとして設定します。  
  
  ソース管理スタブは、ソース管理パッケージのアクティブなサービスを検索し、IDE からのすべての受信サービス呼び出しをそのパッケージにルーティングします。  
  
  ソース管理アダプターパッケージは、に用意されている特殊なソース管理パッケージです [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 このパッケージは、ソース管理プラグイン API に基づいたソース管理プラグインをサポートするための中心的なコンポーネントです。 ソース管理プラグインがアクティブプラグインの場合、ソース管理スタブはそのイベントをソース管理アダプターパッケージに送信します。 さらに、ソース管理アダプターパッケージは、ソース管理プラグイン API を使用してソース管理プラグインと通信します。また、すべてのソース管理プラグインに共通の既定の UI も提供します。  
  
  一方、ソース管理パッケージがアクティブパッケージの場合、ソース管理スタブは、ソース管理のパッケージインターフェイスを使用して、パッケージと直接通信し [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] ます。 ソース管理パッケージは、独自のソース管理 UI をホストします。  
  
  ![ソース管理アーキテクチャのグラフィック](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")  
  
  ソース管理パッケージの場合、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、ソース管理コードまたは統合用の API を提供しません。 これは、「ソース管理プラグインの [作成](../../extensibility/internals/creating-a-source-control-plug-in.md) 」で説明されている方法と同じです。ソース管理プラグインは、厳密な一連の関数とコールバックを実装する必要があります。  
  
  VSPackage と同様に、ソース管理パッケージは、を使用して作成できる COM オブジェクトです `CoCreateInstance` 。 VSPackage を実装することにより、IDE でそれ自体を使用できるようになり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> ます。 インスタンスが作成されると、VSPackage は、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> IDE で使用可能なサービスとインターフェイスへの VSPackage アクセスを提供するサイトポインターとインターフェイスを受け取ります。  
  
  VSPackage ベースのソース管理パッケージを作成するには、ソース管理プラグイン API ベースのプラグインを記述するよりも高度なプログラミングの専門知識が必要です。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>   
 [はじめに](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
