---
title: ブレークポイント関連メソッド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c72ec63e500ac86a4a5bd66a2956fe0fb06c8834
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739209"
---
# <a name="breakpoint-related-methods"></a>ブレークポイント関連のメソッド
デバッグ エンジン (DE) は、ブレークポイントの設定をサポートする必要があります。 Visual Studio のデバッグでは、次の種類のブレークポイントがサポートされます。

- Bound

     UI を介して要求され、指定したコードの場所に正常にバインドされました

- 保留中

     UI を通じて要求されたが、実際の命令にまだバインドされていない

## <a name="discussion"></a>ディスカッション
 たとえば、保留中のブレークポイントは、命令がまだ読み込まれていないときに発生します。 コードが読み込まれると、保留中のブレークポイントは、指定された場所のコードにバインドしようとします。 イベントは、バインドが成功したことを示すため、またはバインディング エラーがあったことを通知するために、セッション デバッグ マネージャー (SDM) に送信されます。

 保留中のブレークポイントは、対応するバインドされたブレークポイントの内部リストも管理します。 保留中のブレークポイントが 1 つあると、コードに多数のブレークポイントが挿入される可能性があります。 Visual Studio のデバッグ UI には、保留中のブレークポイントと、対応するバインドされたブレークポイントのツリー ビューが表示されます。

 保留中のブレークポイントの作成と使用には[、IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)メソッドの実装と[、IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)インターフェイスの次のメソッドが必要です。

|Method|説明|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|指定された保留中のブレークポイントをコードの場所にバインドできるかどうかを判断します。|
|[Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|指定された保留中のブレークポイントを 1 つ以上のコードの場所にバインドします。|
|[Getstate](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|保留中のブレークポイントの状態を取得します。|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|保留中のブレークポイントの作成に使用するブレークポイント要求を取得します。|
|[有効化](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|保留中のブレークポイントの有効な状態を切り替えます。|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|保留中のブレークポイントからバインドされているすべてのブレークポイントを列挙します。|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|保留中のブレークポイントから発生するすべてのエラー ブレークポイントを列挙します。|
|[削除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|保留中のブレークポイントと、そのブレークポイントからバインドされているすべてのブレークポイントを削除します。|

 バインドされたブレークポイントとエラー ブレークポイントを列挙するには、[すべての](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)メソッドを実装する必要[があります。](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)

 コードの場所にバインドする保留中のブレークポイントには、次の[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|ブレークポイントを含む保留中のブレークポイントを取得します。|
|[Getstate](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|バインドされたブレークポイントの状態を取得します。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|ブレークポイントを記述するブレークポイントの解像度を取得します。|
|[有効化](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|ブレークポイントを有効または無効にします。|
|[削除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|バインドされたブレークポイントを削除します。|

 解決と要求の情報は、次の[IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md)メソッドの実装を必要とします。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|解決によって表されるブレークポイントの種類を取得します。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|ブレークポイントを記述するブレークポイントの解像度情報を取得します。|

 バインディング中に発生する可能性のあるエラーの解決には、次の[IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|エラー ブレークポイントを含む保留中のブレークポイントを取得します。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|エラー ブレークポイントを記述するブレークポイント エラー解決を取得します。|

 バインディング中に発生する可能性のあるエラーの解決には、[次](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)のメソッドも必要です。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|ブレークポイントの種類を取得します。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|ブレークポイントの解決情報を取得します。|

 ブレークポイントでソース コードを表示するには[、IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)および/または[メソッドを実装](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
