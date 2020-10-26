---
title: レガシ API | のテキストバッファーイベントMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text buffer events
ms.assetid: 9be49e9f-1864-41c2-8a3c-f66895881341
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e82fa31ca435d0c850a4d9e75e927cff9613b046
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186412"
---
# <a name="text-buffer-events-in-the-legacy-api"></a>レガシ API のテキスト バッファー イベント
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストバッファーオブジェクトは、さまざまな状況に対応できるように、いくつかの異なるイベントを出力します。  
  
 レガシ API を使用している場合は、テキストバッファーに対する変更の通知を受信するために、次のインターフェイスを実装する必要があります。 テキストバッファーのインターフェイスを使用してテキストバッファーにインターフェイスを公開し、 `IConnectionPointContainer` バッファーからの行変更の通知を受信します。 詳細については、「 [方法: 従来の API を使用してテキストバッファーイベントに登録する](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)」を参照してください。 `IVsTextStreamEvents`インターフェイスまたはインターフェイスの場合は、 `IVsTextLinesEvents` それぞれ1次元座標または2次元座標で変更が返されます。  
  
## <a name="text-buffer-interfaces"></a>テキストバッファーインターフェイス  
 テキストバッファーオブジェクトによって実装されるインターフェイスを次に示します。  
  
|インターフェイス|説明|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (つまり、1つの元に戻す/やり直し単位でグループ化されたアクション) の作成を有効にします。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|テキストバッファーによって管理されるドキュメントデータの永続化を有効にします。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|基本的なサービスを提供します。多くのクライアントで使用されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|2次元座標を使用して読み取りおよび書き込みの機能を提供します。 `IVsTextBuffer` から継承されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|バッファー内のテキストへの高速でストリーム指向のシーケンシャルアクセスを提供します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|1次元座標を使用して読み取りおよび書き込みの機能を提供します。 `IVsTextBuffer` から継承されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|プロパティのジェネリックコレクションへのアクセスを提供します。 最も重要なプロパティは、バッファーの名前 (モニカー) です。 このインターフェイスを使用して独自のランダムデータをバッファーに格納するには、GUID を作成し、それをキーとして使用します。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|イベントの接続ポイントをサポートします。|  
  
## <a name="text-buffer-event-interfaces"></a>テキストバッファーのイベントインターフェイス  
 次に、テキストバッファーイベント通知のインターフェイスを示します。  
  
|インターフェイス|説明|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferEvents>|新しい言語サービスがテキストバッファーに関連付けられている場合に、クライアントに通知します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferDataEvents>|テキストバッファーが初期化されたときと、テキストバッファー内のデータに変更が加えられたときに、クライアントに通知します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamEvents>|基になるテキストバッファーに対する変更をクライアントに1次元座標で通知します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents>|基になるテキストバッファーに対する変更をクライアントに2次元座標で通知します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserDataEvents>|ユーザーデータへの変更をクライアントに通知します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>|最後のコミットジェスチャをクライアントに通知し、イベントをトリガーし、変更されたテキストの範囲を提供します。 この `IVsPreliminaryTextChangeCommitEvents` インターフェイスは、Undo または Redo コマンドへの応答としては起動されません。 イベントは、元に戻すマネージャーがあるバッファーに対してのみ発生します。 `IVsPreliminaryTextChangeCommitEvents` は、他のイベントが発生する前に発生します。これは、他のイベントによって、変更がコミットされる前に、他のイベントによってテキストが変更されないようにするためです。 VSPackage はインターフェイスまたはインターフェイスのいずれかを監視する必要があり `IVsPreliminaryTextChangeCommitEvents` `IVsFinalTextChangeCommitEvents` ますが、両方を監視することはできません。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>|最後のコミットジェスチャをクライアントに通知し、イベントをトリガーし、変更されたテキストの範囲を提供します。 この `IVsFinalTextChangeCommitEvents` インターフェイスは、Undo または Redo コマンドへの応答としては起動されません。 イベントは、元に戻すマネージャーがあるバッファーに対してのみ発生します。 `IVsFinalTextChangeCommitEvents` は、言語サービスや、編集を完全に制御できるその他のオブジェクトによってのみ使用されることを意図しています。 VSPackage はインターフェイスまたはインターフェイスのいずれかを監視する必要があり `IVsPreliminaryTextChangeCommitEvents` `IVsFinalTextChangeCommitEvents` ますが、両方を監視することはできません。|  
  
## <a name="see-also"></a>参照  
 [レガシ API を使用したテキストバッファーへのアクセス](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)   
 [方法: レガシ API でテキスト バッファー イベントを登録する](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)
