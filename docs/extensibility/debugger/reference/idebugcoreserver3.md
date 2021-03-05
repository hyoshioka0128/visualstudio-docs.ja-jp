---
description: このインターフェイスは、プロセスが実行されているサーバーに関する情報へのアクセスを提供します。
title: IDebugCoreServer3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1328a97742a4672cdc71805c4c674d66fe05e817
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154614"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
このインターフェイスは、プロセスが実行されているサーバーに関する情報へのアクセスを提供します。

## <a name="syntax"></a>構文

```
IDebugCoreServer3 : IDebugCoreServer2
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio は、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [QueryInterface](/cpp/atl/queryinterface)を使用して、 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスからこのインターフェイスを取得します。 [Getserver](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)を呼び出すと、このインターフェイスを返すこともできます。 このインターフェイスは、多くの場合、カスタムポート供給業者が、サーバー (ローカルまたはリモート) でプログラムを起動するために使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|サーバーの名前を取得します。|
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|サーバー名のフレンドリバージョンを取得します。|
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|プロセスが開始されたときに自動的にプロセスにアタッチするように、特定のデバッグエンジンに指示します。|
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|自動アタッチに失敗した場合に、特定のエラーコードを取得します。|
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|サーバー上にデバッグエンジンのインスタンスを作成します。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|サーバーが呼び出し元と同じコンピューター上にあるかどうかを示すフラグを取得します。|
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|サーバーとの通信に使用されているプロトコルを示す値を取得します。|
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|このサーバーが認識しているすべてのデバッグエンジンのすべての自動アタッチ設定を無効にします。|

## <a name="remarks"></a>解説
 カスタムポートサプライヤーは、[イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)の呼び出しで[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスを受け取ります。 インターフェイスは、 `IDebugCoreServer3` そのインターフェイスから取得できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
