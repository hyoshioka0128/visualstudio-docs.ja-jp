---
title: 提供されるサービス (ソース管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 750710cdc381573f8aa6fd064e1fc980030cf359
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202710"
---
# <a name="services-provided-source-control-vspackage"></a>提供されるサービス (ソース管理 VSPackage)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

サービスは、Vspackage 間、および Visual Studio 統合開発環境 (IDE) とインストールされている Vspackage の間で機能を共有するための主要なメカニズムです。 Visual Studio IDE におけるサービスとその重要度の詳細については、「[サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。  
  
## <a name="the-source-control-service"></a>ソース管理サービス  
 Visual Studio には、IDE レベルのサービスとパッケージレベルのサービスの2つの層が用意されています。 IDE レベルのサービスは、Visual Studio IDE によってネイティブに提供されます。 ソース管理パッケージは、これらのサービスの一部を消費します。 VSPackage としてのソース管理パッケージは、独自のソース管理サービスを提供することによって、ソース管理機能を共有します。 ソース管理パッケージは、Visual Studio IDE で使用できるコントラクトの形式で、このによって実装されたソース管理関連のインターフェイスのセットをカプセル化します。  
  
## <a name="see-also"></a>参照  
 [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
