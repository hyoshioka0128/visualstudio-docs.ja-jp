---
title: ソース管理プラグインを使用したはじめに |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 85aa5727f252ad75c45064d7b885e3d282da36a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538162"
---
# <a name="getting-started-with-source-control-plug-ins"></a>ソース管理プラグイン入門
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理プラグインを作成するには、ソース管理プラグイン API で定義されている関数を実装する DLL を作成し、その DLL をに登録して、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ソースコードのバージョン管理で使用できるようにする必要があります。  
  
 ソース管理プラグイン API の3つのバージョン (バージョン1.1、1.2、および 1.3) をソース管理プラグインで使用できます。ここに記載されているソース管理プラグイン API はバージョン1.3 です。 バージョン1.1 および1.2 をサポートするソース管理プラグインと完全に互換性があるように設計されています。 「 [ソース管理プラグイン Api バージョン1.3 の新](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md) 機能」セクションでは、ソース管理プラグイン api の最新バージョンでサポートされている新機能について詳しく説明しています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: ソース管理プラグインのインストール](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)  
 ソース管理 DLL をプラグインするために必要なレジストリエントリを作成する方法について説明します。  
  
 [ソース管理プラグイン API バージョン 1.3 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)  
 バージョン1.3 のソース管理プラグイン API に加えられた変更の簡単な概要を示します。  
  
 [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)  
 バージョン1.2 のソース管理プラグイン API に加えられた変更の簡単な概要を示します。  
  
## <a name="related-sections"></a>関連項目  
 [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)  
 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。  
  
 [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 ソース管理プラグイン SDK を定義し、含まれているリソースについて説明します。
