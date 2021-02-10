---
title: IDebugAddress2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b31efd42d4d51384a09d6f0468484561e32f4397
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99944818"
---
# <a name="idebugaddress2"></a>IDebugAddress2
このインターフェイスは、アドレスがこのインターフェイスによって表されるオブジェクトを所有するプロセスの ID へのアクセスを提供します。

## <a name="syntax"></a>構文

```
IDebugAddress2 : IDebugAddress
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、このアドレスに関連するオブジェクトを所有するプロセスの ID へのアクセスを提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [QueryInterface](/cpp/atl/queryinterface)を使用して、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイスからこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスから継承されたメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|このインターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
