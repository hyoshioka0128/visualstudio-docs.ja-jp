---
title: ソース管理を作成する VSPackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2b1516cf358a4488ff02e650f6c703a1761a94a2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196955"
---
# <a name="creating-a-source-control-vspackage"></a>ソース管理 VSPackage の作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このドキュメントには、に統合されているソース管理パッケージのアーキテクチャの概要、実装するインターフェイスによって定義されている API、および使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] されるサービスと、単純なソース管理パッケージの実装を示すサンプルへのリンクが含まれています。  
  
 ソース管理 VSPackage を使用すると、と統合するソース管理の詳細な統合パスを作成でき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 これにより、パッケージは、でホストされている既定のソース管理 UI をバイパスし、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロジェクトシステムからのソース管理要求に応答して、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **ソリューションエクスプローラー**などのコンポーネントと対話できます。 は [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] サービスモデルを使用してと統合できる VSPackage を作成するメカニズムをパートナーに提供します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](../../extensibility/internals/getting-started-with-source-control-vspackages.md)  
 ソース管理パッケージについて説明します。これは、のソース管理機能を実装するためのソース管理プラグインに代わる、より高度な代替手段です [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [アーキテクチャ](../../extensibility/internals/source-control-vspackage-architecture.md)  
 図を紹介し、ソース管理パッケージのコンポーネントについて説明します。  
  
 [機能](../../extensibility/internals/source-control-vspackage-features.md)  
 ソース管理パッケージのさまざまな機能について説明します。  
  
 [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)  
 ソース管理パッケージがディープインテグレーションのために実装する必要がある VSPackage の構造について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 ソース管理の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ユーザーインターフェイス (UI) でソース管理機能を提供するソース管理プラグインを作成する方法について説明します。  
  
 [ソース管理](../../extensibility/internals/source-control.md)  
 の統合機能としてソース管理を実装するためのオプションについて説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。
