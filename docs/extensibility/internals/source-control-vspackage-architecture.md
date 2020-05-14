---
title: ソース管理 VSPackage アーキテクチャ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d6e62aa9e2d725e982f0605e2721f0bfeb3cc5ee
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705080"
---
# <a name="source-control-vspackage-architecture"></a>ソース管理 VSPackage アーキテクチャ
ソース管理パッケージは、IDE が提供するサービスを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用する VSPackage です。 その代わりに、ソース管理パッケージはソース管理サービスとして機能を提供します。 また、ソース管理パッケージは、ソース管理を に統合するためのソース管理プラグインよりも汎用性の高い代替手段です[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

 ソース管理プラグイン API を実装するソース管理プラグインは、厳密なコントラクトを遵守します。 たとえば、プラグインは既定[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のユーザー インターフェイス (UI) を置き換えることはできません。 さらに、ソース管理プラグイン API では、プラグインが独自のソース管理モデルを実装することはできません。 ただし、ソース管理パッケージは、これらの制限の両方を克服します。 ソース管理パッケージは、ユーザーのソース管理エクスペリエンスを完全に制御します[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 また、ソース管理パッケージは、独自のソース管理モデルとロジックを使用でき、すべてのソース管理関連のユーザー インターフェイスを定義できます。

## <a name="source-control-package-components"></a>ソース管理パッケージ コンポーネント
 アーキテクチャ図に示すように、ソース管理[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]スタブという名前のコンポーネントは、ソース管理パッケージをと統合する VSPackage です[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

 ソース管理スタブは、次のタスクを処理します。

- ソース管理パッケージの登録に必要な共通の UI を提供します。

- ソース管理パッケージを読み込みます。

- ソース管理パッケージをアクティブ/非アクティブとして設定します。

  ソース管理スタブは、ソース管理パッケージのアクティブなサービスを検索し、IDE からそのパッケージに受信するすべてのサービス呼び出しをルーティングします。

  ソース管理アダプター パッケージは、提供する特別なソース管理[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]パッケージです。 このパッケージは、ソース管理プラグイン API に基づくソース管理プラグインをサポートするための中心的なコンポーネントです。 ソース管理プラグインがアクティブなプラグインである場合、ソース管理スタブは、ソース管理アダプター パッケージにイベントを送信します。 次に、ソース管理アダプター パッケージは、ソース管理プラグイン API を使用してソース管理プラグインと通信し、すべてのソース管理プラグインに共通の既定の UI を提供します。

  ソース管理パッケージがアクティブなパッケージである場合、ソース管理スタブは、ソース管理パッケージ インターフェイスを[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]使用して直接パッケージと通信します。 ソース管理パッケージは、独自のソース管理 UI をホストします。

  ![ソース管理アーキテクチャのグラフィック](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  ソース管理パッケージの場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理コードや API を統合用に提供しません。 これは、ソース管理プラグインが厳密な関数とコールバックのセットを実装する必要がある[ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)で説明されているアプローチとは対照的です。

  他の VSPackage と同様に、ソース管理パッケージは を使用`CoCreateInstance`して作成できる COM オブジェクトです。 VSPackage は、 を実装[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>することで、それ自体を IDE で使用できるようにします。 インスタンスが作成されると、VSPackage はサイト ポインターと、IDE で<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>使用可能なサービスおよびインターフェイスへの VSPackage アクセスを提供するインターフェイスを受信します。

  VSPackage ベースのソース管理パッケージを作成するには、ソース管理プラグイン API ベースのプラグインを作成するよりも、より高度なプログラミングの専門知識が必要です。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [作業の開始](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
