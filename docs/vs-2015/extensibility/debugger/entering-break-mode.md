---
title: 中断モードに入る |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c4251779593e237713258fd54c80dcb311ce4b80
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182253"
---
# <a name="entering-break-mode"></a>中断モードの開始
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次に示すのは、関数にステップインした後にブレークポイントが検出されたとき、そのカーソルがあるソースコード行に実行されているか、ブレークポイントまで実行されている場合に発生する処理です。  
  
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
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
