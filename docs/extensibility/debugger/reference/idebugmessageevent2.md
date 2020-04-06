---
title: メッセージイベント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 180162988cbb09f98b7fc2e8f33f6b5d0ed322ae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727359"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
このインターフェイスは、ユーザーからの応答を必要とする Visual Studio にメッセージを送信するデバッグ エンジン (DE) によって使用されます。

## <a name="syntax"></a>構文

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デは、ユーザーの応答を必要とする Visual Studio にメッセージを送信するには、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

 このインターフェイスの実装は、De に対する Visual Studio の[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)の呼び出しを通信する必要があります。 たとえば、この処理は、DE のメッセージ処理スレッドにポストされたメッセージで行うことができます。 `IDebugMessageEvent2::SetResponse`

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、応答を必要とするメッセージをユーザーに表示するために、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされるときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugMessageEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|表示するメッセージを取得します。|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|メッセージ ボックスから応答を設定します (存在する場合)。|

## <a name="remarks"></a>Remarks
 DE は、特定のメッセージに対してユーザーからの特定の応答を必要とする場合に、このインターフェイスを使用します。 たとえば、プログラムにリモートでアタッチしようとして DE が "アクセスが拒否されました" というメッセージを受け取った場合、DE は、メッセージ`IDebugMessageEvent2`ボックス スタイル`MB_RETRYCANCEL`のイベントでこのメッセージを Visual Studio に送信します。 これにより、ユーザーは接続操作を再試行またはキャンセルできます。

 DE は、Win32 関数`MessageBox`の規則に従ってこのメッセージを処理する方法を指定します (詳細については[AfxMessageBox を](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)参照してください)。

 [インターフェイスを](../../../extensibility/debugger/reference/idebugerrorevent2.md)使用して、ユーザーからの応答を必要としないメッセージを Visual Studio に送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
