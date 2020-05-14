---
title: イベントの作成2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramCreateEvent2
helpviewer_keywords:
- IDebugProgramCreateEvent2 interface
ms.assetid: b19a7934-6179-4a68-9075-bd7dcd640b05
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78088d6e5da61c32302c13b08143c9ed902452e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722628"
---
# <a name="idebugprogramcreateevent2"></a>IDebugProgramCreateEvent2
このインターフェイスは、デバッグ エンジン (DE) プログラムがアタッチされているときにセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugProgramCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE またはカスタム ポート サプライヤーは、プログラムが作成されたことを報告するこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、`QueryInterface`このメソッドを使用`IDebugEvent2`してインターフェイスにアクセスします。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE またはカスタム ポート サプライヤーは、プログラムの作成を報告するために、このイベント オブジェクトを作成して送信します。 DE は、デバッグ中のプログラムにアタッチするときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して、このイベントを送信します。 カスタム ポート サプライヤーは[、IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)インターフェイスを使用してこのイベントを送信します。

## <a name="remarks"></a>Remarks
 DE またはカスタム ポート サプライヤーは、新しい[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスを[発行](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
