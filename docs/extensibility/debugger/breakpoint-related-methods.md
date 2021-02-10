---
title: Breakpoint-Related メソッド |Microsoft Docs
description: Visual Studio のデバッグでは、バインドされたブレークポイントをサポートします。このブレークポイントは、コード内の場所に正常にバインドされ、まだバインドされていない保留中のブレークポイントをサポートします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c20a92e847f120850d7cbd424cc073018903911d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930825"
---
# <a name="breakpoint-related-methods"></a>ブレークポイントに関連するメソッド
デバッグエンジン (DE) は、ブレークポイントの設定をサポートしている必要があります。 Visual Studio のデバッグでは、次の種類のブレークポイントをサポートしています。

- Bound

     UI を通じて要求され、指定したコードの場所に正常にバインドされます。

- Pending

     UI で要求されますが、実際の命令にはまだバインドされていません。

## <a name="discussion"></a>ディスカッション
 たとえば、命令がまだ読み込まれていない場合は、保留中のブレークポイントが発生します。 コードが読み込まれると、保留中のブレークポイントは、指定された場所のコードにバインドしようとします。つまり、コードに改行命令を挿入しようとします。 イベントは、バインディングが成功したことを示すため、またはバインドエラーが発生したことを通知するために、セッションデバッグマネージャー (SDM) に送信されます。

 保留中のブレークポイントも、対応するバインドされたブレークポイントの内部リストを管理します。 1つの保留中のブレークポイントによって、コード内に多数のブレークポイントが挿入されることがあります。 Visual Studio のデバッグ UI には、保留中のブレークポイントとそれに対応するバインドされたブレークポイントのツリービューが表示されます。

 保留中のブレークポイントを作成および使用するには、 [IDebugEngine2:: CreatePendingBreakpoint ポイント](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) メソッドと [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスの次のメソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|指定した保留中のブレークポイントをコードの場所にバインドできるかどうかを判断します。|
|[束縛](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|指定された保留中のブレークポイントを1つまたは複数のコードの場所にバインドします。|
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|保留中のブレークポイントの状態を取得します。|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|保留中のブレークポイントを作成するために使用されるブレークポイント要求を取得します。|
|[有効化](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|保留中のブレークポイントの有効化状態を切り替えます。|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|保留中のブレークポイントからバインドされたすべてのブレークポイントを列挙します。|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|保留中のブレークポイントによって発生するすべてのエラーブレークポイントを列挙します。|
|[削除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|保留中のブレークポイントと、それにバインドされているすべてのブレークポイントを削除します。|

 バインドされたブレークポイントとエラーのブレークポイントを列挙するには、 [IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) と [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)のすべてのメソッドを実装する必要があります。

 コードの場所にバインドする保留中のブレークポイントには、次の [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|ブレークポイントを含む保留中のブレークポイントを取得します。|
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|バインドされたブレークポイントの状態を取得します。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|ブレークポイントを説明するブレークポイントの解像度を取得します。|
|[有効化](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|ブレークポイントを有効または無効にします。|
|[削除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|バインドされたブレークポイントを削除します。|

 解決と要求情報には、次の [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|解決によって表されるブレークポイントの型を取得します。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|ブレークポイントを説明するブレークポイントの解決情報を取得します。|

 バインディング中に発生する可能性のあるエラーの解決には、次の [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|エラーブレークポイントを含む保留中のブレークポイントを取得します。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|エラーブレークポイントを説明するブレークポイントエラーの解決方法を取得します。|

 また、バインド中に発生する可能性のあるエラーを解決するには、次の [IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)メソッドも必要です。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|ブレークポイントの種類を取得します。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|ブレークポイントの解決情報を取得します。|

 ブレークポイントでソースコードを表示するには、 [IDebugStackFrame2:: GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) および [IDebugStackFrame2:: GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)のメソッドのメソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
