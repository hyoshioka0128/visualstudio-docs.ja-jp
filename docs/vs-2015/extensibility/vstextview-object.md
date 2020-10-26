---
title: VSTextView オブジェクト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSTextView
helpviewer_keywords:
- VSTextView object, reference
- views [Visual Studio SDK], reference
ms.assetid: 78272ddc-9718-4c65-a94e-a44a2e8d54f4
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 22e4d4cdf1e5ca610dbdb067f8195fb730139c3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690697"
---
# <a name="vstextview-object"></a>VSTextView オブジェクト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストビューは、ユーザーがテキストバッファーの Unicode テキストを表示および編集できるウィンドウです。 基本的に、ビューは、ほとんどのユーザーがエディターとして参照します。 ビューは、さまざまなテキストレイヤー (右端での折り返し、アウトラインテキストなど) によってバッファーから分離されているため、ビューはバッファー内のテキストを正確に表現するとは限りません。 テキストビューの詳細については、「[従来の API を使用したテキストビューへのアクセス](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)」を参照してください。  
  
 次の表は、オブジェクト内のインターフェイスを示して <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> います。  
  
|インターフェイス|説明|  
|---------------|-----------------|  
|[IDropSource](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|標準 OLE インターフェイス。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|標準 OLE インターフェイス。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|標準 OLE インターフェイス。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|標準 OLE インターフェイス。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (つまり、1つの元に戻す/やり直し単位でグループ化されたアクション) の作成を有効にします。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|ビューを管理およびアクセスするための基本的なメソッドを提供します。 `IVsTextView` はスレッド セーフではありません。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウペインを作成および管理します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|テキストレイヤーと対話します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|別のスレッドからビューに対して操作を実行します。|  
  
## <a name="see-also"></a>参照  
 [図形の編集](https://msdn.microsoft.com/f08872bd-fd9c-4e36-8cf2-a2a2622ef986)   
 [VSTextBuffer オブジェクト](../extensibility/vstextbuffer-object.md)   
 [レガシ API を使用するテキスト ビューへのアクセス](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)
