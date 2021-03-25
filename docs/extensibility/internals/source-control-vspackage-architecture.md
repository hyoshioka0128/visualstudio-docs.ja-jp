---
title: ソース管理 VSPackage Architecture |Microsoft Docs
description: ソース管理パッケージのアーキテクチャについて説明します。これは、ソース管理サービスとして Visual Studio に機能を提供する VSPackage です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4e9f19506c58f65f80900c08fe339c7478144546
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064229"
---
# <a name="source-control-vspackage-architecture"></a>ソース管理 VSPackage アーキテクチャ
ソース管理パッケージは、IDE によって提供されるサービスを使用する VSPackage です [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 戻り値として、ソース管理パッケージの機能がソース管理サービスとして提供されます。 また、ソース管理パッケージは、ソース管理をに統合するためのソース管理プラグインよりも汎用性の高い方法です [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 ソース管理プラグイン API を実装するソース管理プラグインは、厳密なコントラクトに準拠しています。 たとえば、既定の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザーインターフェイス (UI) をプラグインで置き換えることはできません。 さらに、ソース管理プラグイン API では、プラグインが独自のソース管理モデルを実装することはできません。 ただし、ソース管理パッケージでは、これらの両方の制限が解消します。 ソース管理パッケージは、ユーザーのソース管理エクスペリエンスを完全に制御 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] できます。 さらに、ソース管理パッケージは、独自のソース管理モデルとロジックを使用して、ソース管理に関連するすべてのユーザーインターフェイスを定義できます。

## <a name="source-control-package-components"></a>パッケージコンポーネントの Source-Control
 アーキテクチャ図に示されているように、ソース管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] スタブという名前のコンポーネントは、ソース管理パッケージとを統合する VSPackage です [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 ソース管理スタブは、次のタスクを処理します。

- ソース管理のパッケージ登録に必要な共通の UI を提供します。

- ソース管理パッケージを読み込みます。

- ソース管理パッケージをアクティブ/非アクティブとして設定します。

  ソース管理スタブは、ソース管理パッケージのアクティブなサービスを検索し、IDE からのすべての受信サービス呼び出しをそのパッケージにルーティングします。

  ソース管理アダプターパッケージは、に用意されている特殊なソース管理パッケージです [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 このパッケージは、ソース管理プラグイン API に基づいたソース管理プラグインをサポートするための中心的なコンポーネントです。 ソース管理プラグインがアクティブプラグインの場合、ソース管理スタブはそのイベントをソース管理アダプターパッケージに送信します。 さらに、ソース管理アダプターパッケージは、ソース管理プラグイン API を使用してソース管理プラグインと通信します。また、すべてのソース管理プラグインに共通の既定の UI も提供します。

  一方、ソース管理パッケージがアクティブパッケージの場合、ソース管理スタブは、Source-Control パッケージインターフェイスを使用して、パッケージと直接通信し [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。 ソース管理パッケージは、独自のソース管理 UI をホストします。

  ![ソース管理アーキテクチャのグラフィック](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  ソース管理パッケージの場合、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、ソース管理コードまたは統合用の API を提供しません。 これは、「ソース管理プラグインの [作成](../../extensibility/internals/creating-a-source-control-plug-in.md) 」で説明されている方法と同じです。ソース管理プラグインは、厳密な一連の関数とコールバックを実装する必要があります。

  VSPackage と同様に、ソース管理パッケージは、を使用して作成できる COM オブジェクトです `CoCreateInstance` 。 VSPackage を実装することにより、IDE でそれ自体を使用できるようになり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> ます。 インスタンスが作成されると、VSPackage は、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> IDE で使用可能なサービスとインターフェイスへの VSPackage アクセスを提供するサイトポインターとインターフェイスを受け取ります。

  VSPackage ベースのソース管理パッケージを作成するには、ソース管理プラグイン API ベースのプラグインを記述するよりも高度なプログラミングの専門知識が必要です。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [はじめに](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
