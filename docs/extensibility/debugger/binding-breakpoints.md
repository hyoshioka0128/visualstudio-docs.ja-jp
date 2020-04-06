---
title: ブレークポイントをバインドする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 680cff398a43d1ebe9ccf061ad42781500c7cf01
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739237"
---
# <a name="bind-breakpoints"></a>ブレークポイントをバインドする
ユーザーがブレークポイントを設定する場合は **、F9**キーを押すと、IDE によって要求が作成され、デバッグ セッションにブレークポイントを作成するように求められます。

## <a name="set-a-breakpoint"></a>ブレークポイントの設定
 ブレークポイントの設定は、ブレークポイントの影響を受けるコードまたはデータがまだ使用できない可能性があるため、2 段階のプロセスです。 まず、ブレークポイントを記述し、次に、コードまたはデータが使用可能になったら、次のように、そのコードまたはデータにバインドする必要があります。

1. ブレークポイントは、関連するデバッグ エンジン (DEs) から要求され、ブレークポイントは、コードまたはデータが使用可能になるとバインドされます。

2. ブレークポイント要求はデバッグ セッションに送信され、関連するすべての DEs に送信されます。 ブレークポイントを処理することを選択した DE は、対応する保留中のブレークポイントを作成します。

3. デバッグ セッションは、保留中のブレークポイントを収集し、デバッグ パッケージ (Visual Studio のデバッグ コンポーネント) に返します。

4. デバッグ パッケージは、保留中のブレークポイントをコードまたはデータにバインドするようにデバッグ セッションに要求します。 デバッグ セッションは、この要求を関連するすべての D に送信します。

5. DE がブレークポイントをバインドできる場合、ブレークポイントバインド イベントをデバッグ セッションに送り返します。 それでない場合は、代わりにブレークポイント エラー イベントを送信します。

## <a name="pending-breakpoints"></a>保留中のブレークポイント
 保留中のブレークポイントは、複数のコードの場所にバインドできます。 たとえば、C++ テンプレートのソース コードの行は、テンプレートから生成されるすべてのコード シーケンスにバインドできます。 デバッグ セッションでは、ブレークポイントバインド イベントを使用して、イベントの送信時にブレークポイントにバインドされたコード コンテキストを列挙できます。 後でコード コンテキストをバインドできるため、DE はバインド要求ごとに複数のブレークポイント バインド イベントを送信できます。 ただし、DE はバインド要求ごとに 1 つのブレークポイント エラー イベントのみを送信する必要があります。

## <a name="implementation"></a>実装
 プログラムによって、デバッグ パッケージは、セッション デバッグ マネージャー (SDM) を呼び出し、設定するブレークポイントを記述する[BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md)構造体をラップする[IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md)インターフェイスを提供します。 ブレークポイントは多くの形式で構成できますが、最終的にはコードまたはデータ コンテキストに解決されます。

 SDM は、この呼び出しを各関連する DE[に渡](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)します。 DE がブレークポイントを処理することを選択した場合は、作成し[、IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)インターフェイスを返します。 SDM はこれらのインターフェイスを収集し、デバッグ パッケージに単一`IDebugPendingBreakpoint2`のインターフェイスとして渡します。

 ここまでは、イベントは生成されていません。

 デバッグ パッケージは、DE によって実装されている[Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)を呼び出すことによって、保留中のブレークポイントをコードまたはデータにバインドしようとします。

 ブレークポイントがバインドされている場合、DE は、デバッグ パッケージに[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)イベント インターフェイスを送信します。 デバッグ パッケージでは、このインターフェイスを使用して、1 つ以上の[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)インターフェイスを返す[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)を呼び出すことによって、ブレークポイントにバインドされているすべてのコード コンテキスト (または単一のデータ コンテキスト) を列挙します。 インターフェイス[は](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)[、IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)インターフェイスを返し[、GetResolutionInfo は](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)、コードまたはデータ コンテキストを含む[BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md)共用体を返します。

 DE は、ブレークポイントをバインドできない場合は、デバッグ パッケージに 1 つの[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)イベント インターフェイスを送信します。 デバッグ パッケージは、エラーの種類 (エラーまたは警告) と情報メッセージを取得するには[、GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)を呼び出し、続いて[ブレークポイントの解像度と GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)を[呼](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)び出します。 エラーの種類とメッセージを含む[BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md)構造体を返します。

 DE がブレークポイントを処理してもバインドできない場合は、 型のエラーを`BPET_TYPE_ERROR`返します。 デバッグ パッケージはエラー ダイアログ ボックスを表示して応答し、IDE はソース コード行の左側にブレークポイント グリフ内に感嘆符グリフを配置します。

 DE がブレークポイントを処理し、バインドできないが、他の DE がバインドする可能性がある場合は、警告を返します。 IDE は、ソース コード行の左側にあるブレークポイント グリフの内側に質問グリフを配置して応答します。

## <a name="see-also"></a>関連項目
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
