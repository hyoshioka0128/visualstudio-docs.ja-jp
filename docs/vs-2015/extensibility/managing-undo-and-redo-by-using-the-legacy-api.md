---
title: 従来の API を使用して元に戻すとやり直しを管理する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 838c0ddf-fdf3-4df1-8d21-79610b8ba0b1
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7c2133c75b32e56c1a054740bd829bd04cac97cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194370"
---
# <a name="managing-undo-and-redo-by-using-the-legacy-api"></a>レガシ API を使用した元に戻すとやり直しの管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターは、ユーザーがコードを変更したときに最近の変更を元に戻すことができる undo 操作をサポートする必要があります。 およびで実装されているほとんどのエディターでは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 統合開発環境 (IDE) によって自動的に元に戻す機能を使用できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: 元に戻すの管理を実装する](../extensibility/how-to-implement-undo-management.md)  
 1つまたは複数のビューを持つエディターに対して、元に戻す機能を提供します。  
  
 [方法: 元に戻すスタックをクリアする](../extensibility/how-to-clear-the-undo-stack.md)  
 元に戻すスタックをクリアする方法について説明します。  
  
 [方法: リンクされた元に戻すの管理を使用する](../extensibility/how-to-use-linked-undo-management.md)  
 リンクされた元に戻す管理をエディターに組み込みます。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>  
 複数のビューをサポートするエディターの元に戻す管理機能を提供します。  
  
## <a name="related-sections"></a>関連項目
