---
title: IDebugポートサプライヤー3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f015c21f71f064f2302660ebc75ef00a245348c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724444"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
このインターフェイスを使用すると、呼び出し元は、ポートサプライヤーがデバッガの呼び出しの間にポートを(ディスクに書き込んで)保持できるかどうかを判断し、それらの保存ポートのリストを取得できます。

## <a name="syntax"></a>構文

```
IDebugPortSupplier3 : IDebugPortSupplier2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、このインターフェイスを実装して、ポート情報のディスクへの保存または保存をサポートします。 このインターフェイスは[、IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)インターフェイスと同じオブジェクトに実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[QueryInterface](/cpp/atl/queryinterface)インターフェイスを取得するには`IDebugPortSupplier2`、インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは[、IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)インターフェイスから継承されたメソッドに加えて、次の機能をサポートします。

|Method|説明|
|------------|-----------------|
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|ポートサプライヤーが、デバッガーの呼び出しの間にポートを (ディスクに書き込んで) 永続化できるかどうかを返します。|
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|このポート サプライヤーによってディスクに書き込まれたすべてのポートを列挙するために使用できるオブジェクトを返します。|

## <a name="remarks"></a>Remarks
 ポートサプライヤーが呼び出し間でポートを保持できる場合は、このインターフェイスを実装する必要があります。 ポート サプライヤーがインスタンス化されるときにポートを読み込み、ポート サプライヤーが破棄されたときにディスクに書き込む必要があります。

 通常、デバッグ エンジンはポート サプライヤーと対話せず、このインターフェイスには使用しません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
