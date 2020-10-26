---
title: '方法: 従来の API を使用してテキストバッファーイベントに登録する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - register for text buffer events
ms.assetid: 5fc00ced-882c-4b48-b46c-1fa5a2469f94
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f36e8dd780788d241e3c286b1bbbe581311b143
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204089"
---
# <a name="how-to-register-for-text-buffer-events-with-the-legacy-api"></a>方法: レガシ API でテキスト バッファー イベントを登録する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

レガシ API を使用してテキストバッファーにアクセスする場合は、次の手順に示すように、テキストバッファーイベントに登録する必要があります。  
  
### <a name="to-advise-text-buffer-events"></a>テキストバッファーイベントをアドバイズするには  
  
1. のインターフェイスのいずれかへのポインターから <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 、 `QueryInterface` へのポインターに対してを呼び出し <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> ます。  
  
2. <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer.FindConnectionPoint%2A>メソッドを呼び出して、登録するイベントのインターフェイス ID を渡します。  
  
     たとえば、に登録する場合は、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents> IID_IVsTextLinesEvents のインターフェイス ID を渡します。  
  
     テキストバッファーは、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 適切な接続ポイントオブジェクトのインターフェイスへのポインターを返します。  
  
3. このポインターを使用して、メソッドを呼び出します。これには、インターフェイスなど、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> 登録するイベントインターフェイスの実装へのポインターを渡し `IVsTextLinesEvents` ます。  
  
     この環境では、メソッドを呼び出すことによって、イベントのリッスンを停止するために使用できる cookie が返され <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Unadvise%2A> ます。  
  
## <a name="see-also"></a>参照  
 [レガシ API のテキスト バッファー イベント](../extensibility/text-buffer-events-in-the-legacy-api.md)
