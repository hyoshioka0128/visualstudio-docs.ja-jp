---
title: ソース管理 VS パッケージを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8608aae718ff9f8bdf2e40c0ab648c1d22c38257
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709191"
---
# <a name="create-a-source-control-vspackage"></a>ソース管理の作成 VS パッケージ
このドキュメントには[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、 と統合されたソース管理パッケージのアーキテクチャの概要へのリンクが含まれています実装するインターフェイスと使用するサービスによって定義される API、および単純なソース管理パッケージの実装を示すサンプル。

 ソース管理 VSPackage を使用すると、ソース管理を使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]して統合するための深い統合パスを作成できます。 パッケージがホストする既定のソース管理 UI をバイパスし[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、プロジェクト システムからのソース管理要求に応答し、ソリューション[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**エクスプローラー**などのコンポーネントと対話できます。 サービス[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]モデル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を使用して統合できる VSPackage を作成するメカニズム[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]をパートナーに与えます。

## <a name="in-this-section"></a>このセクションの内容
- [はじめに](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 ソース管理プラグインの代わりに、ソース管理プラグインを実装するためのより高度な方法であるソース管理パッケージについて説明[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

- [Architecture](../../extensibility/internals/source-control-vspackage-architecture.md)

 図を示し、ソース管理パッケージのコンポーネントについて説明します。

- [機能](../../extensibility/internals/source-control-vspackage-features.md)

 ソース管理パッケージのさまざまな機能について説明します。

- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)

 深い統合のためにソース管理パッケージが実装する必要がある VSPackage の構造について説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインを作成する](../../extensibility/internals/creating-a-source-control-plug-in.md)

 ソース管理ユーザー インターフェイス (UI) でソース管理機能を提供する[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理プラグインを作成する方法について説明します。

- [ソース管理](../../extensibility/internals/source-control.md)

 の統合機能としてソース管理を実装するためのオプションについて説明[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。
