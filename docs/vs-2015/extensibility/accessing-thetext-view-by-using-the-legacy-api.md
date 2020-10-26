---
title: 従来の API を使用したテキストビューへのアクセス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text view
ms.assetid: 8f751f72-c972-4be3-84ee-19c281e02e25
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f9396e4523e38e7313efb5668c4680f551558ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184947"
---
# <a name="accessing-thetext-view-by-using-the-legacy-api"></a>レガシ API を使用するテキスト ビューへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストビューは、テキストバッファーに格納されているテキストを表現したものです。 次のセクションに示すように、従来の API を使用してテキストビューにアクセスできます。  
  
## <a name="text-view-object"></a>テキストビューオブジェクト  
 各ビューは独自のテキストバッファーに関連付けられており、ビューはバッファー内のデータのウィンドウです。 次の図は、で表されるテキストビューオブジェクトの主要なインターフェイスを示して <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> います。  
  
 ![Visual Studio テキスト ビュー オブジェクト](../extensibility/media/vstextview.gif "vstextview")  
テキストビューオブジェクト  
  
 ビューは、バッファー内のテキストを表示する方法です。 これには、右端での折り返しやアウトラインのような機能が含まれているため、ビューに表示される内容は、バッファー内のテキストを正確に表現するものではありません。  
  
 ビューでは、ビューが動作する前に、他のサービスまたはプロセスが受信コマンドをインターセプトして操作できるようにします。 これを行う最も一般的なサービスは、言語サービスです。 たとえば、言語サービスでは、カスタムのインデント動作やツールヒントを提供するために、ENTER キーのコマンドをインターセプトすることが必要になる場合があります。  
  
## <a name="adding-functionality-to-the-text-view"></a>テキストビューへの機能の追加  
 特定のキー入力を処理することによって、テキストビューの動作をカスタマイズできます。 キーストロークをインターセプトするには、を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> オブジェクトに実装し、コマンドターゲット () を指定して <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンドを監視およびインターセプトします。  
  
 テキストビューでは、コマンドフィルターにシーケンシャルアーキテクチャを使用します。 新しいコマンドフィルター ( <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> オブジェクト) は、メソッドを呼び出すことによって、シーケンスに追加され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> ます。  
  
 テキストビューのイベント通知は、インターフェイスを使用して提供され `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents` ます。 テキストビューへの変更の通知を受信するには、クライアントオブジェクトにこのインターフェイスを実装します。 このインターフェイスをテキストビューに公開するには、テキストビューのインターフェイスを使用して <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 、ビューからの変更の通知を受け取ります。  
  
## <a name="see-also"></a>参照  
 [レガシ API を使用した表示設定の変更](../extensibility/changing-view-settings-by-using-the-legacy-api.md)   
 [グローバル設定を監視するためのテキスト マネージャーの使用](../extensibility/using-the-text-manager-to-monitor-global-settings.md)
