---
title: 中断モードに入る |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738882"
---
# <a name="enter-break-mode"></a>中断モードに入る
次の情報では、関数にステップインした後、カーソルがあるソースコード行に実行しているか、ブレークポイントまで実行されているときに発生するプロセスについて説明します。

## <a name="break-mode-process"></a>中断モードプロセス

1. デバッグエンジン (DE) は、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)、 [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)、またはその他の停止イベントを送信して、IDE が中断モードになるようにします。

2. SDM は、次のように、スレッドから呼び出し履歴情報を取得します。

    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)

    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)

    - ソースコード情報を取得するための[IDebugStackFrame2:: GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)

    - [IDebugDocumentContext2:: GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md) を利用してファイル名を取得します。

    - [IDebugDocumentContext2:: GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) を指定して、ステートメントの範囲を取得します。

    - [IDebugStackFrame2:: GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md) を実行してメモリ情報を取得します。

## <a name="see-also"></a>関連項目
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
