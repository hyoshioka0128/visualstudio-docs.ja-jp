---
title: IDebugAddress2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 402d8c8bcb50c570ff680b8fe1cf8d26f037ba17
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736573"
---
# <a name="idebugaddress2"></a>IDebugAddress2
このインターフェイスは、このインターフェイスによって表されるアドレスを持つオブジェクトを所有するプロセスの ID へのアクセスを提供します。

## <a name="syntax"></a>構文

```
IDebugAddress2 : IDebugAddress
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは[、IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、このアドレスに関連するオブジェクトを所有するプロセスの ID へのアクセスを提供します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用[します](../../../extensibility/debugger/reference/idebugaddress.md)。

## <a name="methods-in-vtable-order"></a>vtable 順序のメソッド
 このインターフェイスは[、IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイスから継承されたメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|このインターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
