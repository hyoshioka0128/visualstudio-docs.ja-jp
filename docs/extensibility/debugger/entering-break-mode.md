---
title: 中断モードに入る |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4bbcec8adf6468f70d95df5f291ce1e5540406cf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738882"
---
# <a name="enter-break-mode"></a>ブレーク モードに入る
次の情報は、関数にステップ インした後、カーソルが含まれているソース コードの行に対して実行された後、またはブレークポイントに実行された後にブレークポイントが発生したときに発生するプロセスについて説明します。

## <a name="break-mode-process"></a>中断モードプロセス

1. デバッグ エンジン (DE) は、IDE が中断モードに入る原因となる[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) [、IDebugExceptionEvent2、](../../extensibility/debugger/reference/idebugexceptionevent2.md)またはその他の停止イベントを送信します。

2. SDM は、次のようにスレッドからコール スタック情報を取得します。

    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)

    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)

    - ソース コード情報を取得する[IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)

    - [ファイル名を取得する IDebugDocumentContext2::GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)

    - [ステートメント範囲を](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)取得します。

    - メモリ情報を取得する[IDebugStackFrame2::GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
