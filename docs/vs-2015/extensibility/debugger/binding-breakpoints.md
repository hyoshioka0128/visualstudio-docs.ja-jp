---
title: ブレークポイントのバインド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc7f68093432c96d496921ea593b6e936bad8302
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68147970"
---
# <a name="binding-breakpoints"></a>ブレークポイントのバインド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザーが F9 キーを押してブレークポイントを設定した場合、IDE は要求を使用しし、ブレークポイントを作成するようにデバッグセッションに指示します。  
  
## <a name="setting-a-breakpoint"></a>ブレークポイントの設定  
 ブレークポイントの設定は、ブレークポイントの影響を受けるコードまたはデータがまだ使用できない場合があるため、2段階のプロセスです。 まず、ブレークポイントが記述されている必要があります。次に、コードまたはデータが使用可能になったら、次のようにそのコードまたはデータにバインドする必要があります。  
  
1. ブレークポイントが関連するデバッグエンジン (DEs) から要求され、ブレークポイントは使用可能になるとコードまたはデータにバインドされます。  
  
2. ブレークポイント要求は、関連するすべての DEs に送信されるデバッグセッションに送信されます。 ブレークポイントを処理するように選択すると、対応する保留中のブレークポイントが作成されます。  
  
3. デバッグセッションでは、保留中のブレークポイントが収集され、デバッグパッケージ (Visual Studio のデバッグコンポーネント) に送信されます。  
  
4. デバッグパッケージは、保留中のブレークポイントをコードまたはデータにバインドするようにデバッグセッションに要求します。 デバッグセッションは、関連するすべての DEs にこの要求を送信します。  
  
5. DE がブレークポイントをバインドできる場合は、ブレークポイントにバインドされたイベントをデバッグセッションに送り返します。 そうでない場合は、代わりにブレークポイントエラーイベントが送信されます。  
  
## <a name="pending-breakpoints"></a>保留中のブレークポイント  
 保留中のブレークポイントは、複数のコードの場所にバインドできます。 たとえば、C++ テンプレートのソースコードの行は、テンプレートから生成されたすべてのコードシーケンスにバインドできます。 デバッグセッションでは、ブレークポイントバインドイベントを使用して、イベントの送信時にブレークポイントにバインドされたコードコンテキストを列挙できます。 後でより多くのコードコンテキストをバインドできるため、DE は各バインド要求に対して複数のブレークポイントバインドイベントを送信できます。 ただし、DE は、バインド要求ごとに1つのブレークポイントエラーイベントのみを送信する必要があります。  
  
## <a name="implementation"></a>実装  
 プログラムによってデバッグパッケージは、セッションデバッグマネージャー (SDM) を呼び出し、設定するブレークポイントを記述する[BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md)構造体をラップする[IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md)インターフェイスを提供します。 ブレークポイントは多くの形式にすることができますが、最終的にはコードまたはデータコンテキストに解決されます。  
  
 SDM は、 [Creatependingbreakpoint ポイント](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) メソッドを呼び出すことによって、関連する各 DE にこの呼び出しを渡します。 逆に、ブレークポイントを処理するように選択すると、 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスが作成されて返されます。 SDM はこれらのインターフェイスを収集し、1つのインターフェイスとしてデバッグパッケージに戻し `IDebugPendingBreakpoint2` ます。  
  
 これまでは、イベントは生成されませんでした。  
  
 次に、デバッグパッケージは、DE によって実装される [bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)を呼び出して、保留中のブレークポイントをコードまたはデータにバインドしようとします。  
  
 ブレークポイントがバインドされている場合、DE は [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) イベントインターフェイスをデバッグパッケージに送信します。 デバッグパッケージは、このインターフェイスを使用して、1つ以上の[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)インターフェイスを返す[enumboundbreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)ポイントを呼び出すことによって、ブレークポイントにバインドされているすべてのコードコンテキスト (または単一のデータコンテキスト) を列挙します。 [Getbreakpointresolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)インターフェイスは[IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)インターフェイスを返し、 [getresolution INFO](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)はコードまたはデータコンテキストを含む[BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md)の共用体を返します。  
  
 DE がブレークポイントをバインドできない場合は、単一の [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) イベントインターフェイスをデバッグパッケージに送信します。 デバッグパッケージは、 [GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)を呼び出してエラーの種類 (エラーまたは警告) と情報メッセージを取得し、その後に [Getbreakpointresolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) と [getresolution info](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)を呼び出します。 これにより、エラーの種類とメッセージを含む [BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md) 構造体が返されます。  
  
 DE がブレークポイントを処理するが、バインドできない場合は、型のエラーが返さ `BPET_TYPE_ERROR` れます。 デバッグパッケージはエラーダイアログボックスを表示することによって応答し、IDE はソースコード行の左側のブレークポイントグリフの内側に感嘆符を配置します。  
  
 DE がブレークポイントを処理する場合、バインドできませんが、他の DE によってバインドされる場合は、警告が返されます。 IDE は、ブレークポイントのグリフの内側に、ソースコード行の左側に疑問符を配置することで応答します。  
  
## <a name="see-also"></a>参照  
 [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
