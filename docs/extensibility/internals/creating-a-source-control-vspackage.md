---
title: ソース管理を作成する VSPackage |Microsoft Docs
description: Visual Studio と統合するソース管理の詳細な統合パスを作成するソース管理 VSPackage を作成する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 69e526cea292544c725abc7ffb54d0b29ad88403
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305582"
---
# <a name="create-a-source-control-vspackage"></a>ソース管理 VSPackage を作成する
このドキュメントには、に統合されているソース管理パッケージのアーキテクチャの概要、実装するインターフェイスによって定義されている API、および使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] されるサービスと、単純なソース管理パッケージの実装を示すサンプルへのリンクが含まれています。

 ソース管理 VSPackage を使用すると、と統合するソース管理の詳細な統合パスを作成でき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 これにより、パッケージは、でホストされている既定のソース管理 UI をバイパスし、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトシステムからのソース管理要求に応答して、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **ソリューションエクスプローラー** などのコンポーネントと対話できます。 は [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サービスモデルを使用してと統合できる VSPackage を作成するメカニズムをパートナーに提供します。

## <a name="in-this-section"></a>このセクションの内容
- [開始するには](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 ソース管理パッケージについて説明します。これは、のソース管理機能を実装するためのソース管理プラグインに代わる、より高度な代替手段です [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [アーキテクチャ](../../extensibility/internals/source-control-vspackage-architecture.md)

 図を紹介し、ソース管理パッケージのコンポーネントについて説明します。

- [機能](../../extensibility/internals/source-control-vspackage-features.md)

 ソース管理パッケージのさまざまな機能について説明します。

- [要素のデザイン](../../extensibility/internals/source-control-vspackage-design-elements.md)

 ソース管理パッケージがディープインテグレーションのために実装する必要がある VSPackage の構造について説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインを作成する](../../extensibility/internals/creating-a-source-control-plug-in.md)

 ソース管理の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザーインターフェイス (UI) でソース管理機能を提供するソース管理プラグインを作成する方法について説明します。

- [ソース管理](../../extensibility/internals/source-control.md)

 の統合機能としてソース管理を実装するためのオプションについて説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。
