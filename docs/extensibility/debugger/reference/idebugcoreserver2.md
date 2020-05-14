---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7a5990c84fbaeb5ebb3b1e188d3317234afda06b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733023"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
このインターフェイスは、ネットワーク上のマシン上のサーバーを表し、情報を取得するために使用されます。

## <a name="syntax"></a>構文

```
IDebugCoreServer2 : IUknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio では、サーバーを表すためにこのインターフェイスを実装します。 Visual Studio の各インスタンスは、このインターフェイスのインスタンスを作成します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 カスタム ポート サプライヤーは[、Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)への呼び出しでこのインターフェイスを受信します。

 デバッグ エンジンは[、GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)の呼び出しを通じて間接的にこのインターフェイスを取得できます ( [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)から派生したインターフェイスを返`IDebugCoreServer2`します )。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugCoreServer2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|コンピューターの名前と属性を取得します。|
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|コンピューターの名前を取得します。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|コンピューターに存在するポートサプライヤーを取得します。|
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|コンピューターに既に存在するポートを取得します。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|マシン上のすべてのポートの列挙子を作成します。|
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|マシン上のすべてのポートサプライヤーの列挙子を作成します。|
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|マシンのマシンユーティリティを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、ネットワーク上のコンピューターで実行されているプロセスを参照するために Visual Studio によっても使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
