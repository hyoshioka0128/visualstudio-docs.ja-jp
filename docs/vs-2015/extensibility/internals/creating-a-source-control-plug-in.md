---
title: ソース管理プラグインを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 37cb4cfc71b2574600bf7ca886c693b888ec821a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196969"
---
# <a name="creating-a-source-control-plug-in"></a>ソース管理プラグインの作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio SDK には、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 統合開発環境 (IDE: integrated development environment) にソース管理機能を追加できるリソースが用意されています。 このドキュメントに記載されているソース管理プラグイン API に準拠している任意のプラグイン DLL を使用できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)  
 ソース管理プラグインをインストールする方法について説明し、現在使用可能なソース管理プラグイン API バージョンについて説明します。  
  
 [アーキテクチャ](../../extensibility/internals/source-control-plug-in-architecture.md)  
 アーキテクチャ図を使用して、ソース管理プラグインと IDE との統合について説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 [ソース管理プラグイン向けのテスト ガイド](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 ソース管理プラグインのインストールと操作のテスト方法に関するガイダンスを提供します。  
  
## <a name="related-sections"></a>関連項目  
 [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)  
 ソース管理機能を提供するだけでなく、ソース管理 UI を置き換えるソース管理 VSPackage を作成する方法について説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)  
 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。  
  
 [ソース管理](../../extensibility/internals/source-control.md)  
 の統合機能としてソース管理を実装するためのオプションについて説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。
