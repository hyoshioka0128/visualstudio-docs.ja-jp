---
title: をクリックしてサービスを開始する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d110e66e937249fdee34f424d4f68a9b914113d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732806"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
このインターフェイスは、プロセスが実行されているサーバーに関する情報にアクセスします。

## <a name="syntax"></a>構文

```
IDebugCoreServer3 : IDebugCoreServer2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio では、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 インターフェイスからこの[インターフェイスを取得](../../../extensibility/debugger/reference/idebugcoreserver2.md)するのにには[、インターフェイス](/cpp/atl/queryinterface)を使用します。 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)への呼び出しもこのインターフェイスを返すことができます。 このインターフェイスは、サーバー (ローカルまたはリモート) でプログラムを起動するカスタム ポート サプライヤーによって最も頻繁に使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは[、IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[サーバー名を取得します。](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|サーバーの名前を取得します。|
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|サーバー名のわかりやすいバージョンを取得します。|
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|プロセスが開始されたときに、プロセスに自動的にアタッチするように、特定のデバッグ エンジンに指示します。|
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|自動アタッチが失敗した場合に、特定のエラー コードを取得します。|
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|サーバー上にデバッグ エンジンのインスタンスを作成します。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|サーバーが呼び出し元と同じコンピューター上にあるかどうかを示すフラグを取得します。|
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|サーバーとの通信に使用されているプロトコルを示す値を取得します。|
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|このサーバーが認識しているすべてのデバッグ エンジンに対して、すべての自動アタッチ設定を無効にします。|

## <a name="remarks"></a>Remarks
 カスタム ポート サプライヤーは[、イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)への呼び出しで[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスを受信します。 インターフェイス`IDebugCoreServer3`は、そのインターフェイスから取得できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
