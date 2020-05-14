---
title: Iデバッグアドレス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1f281ceb1f305c5774fedbf725f2e6a9481d073d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736594"
---
# <a name="idebugaddress"></a>IDebugAddress
このインターフェイスは、アイテムのアドレスを表します。 これは、シンボル ハンドラーによって返されます。

## <a name="syntax"></a>構文

```
IDebugAddress : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは、オブジェクトのアドレスを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 多くのインターフェイスの多くのメソッドは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|オブジェクトとその場所を記述する[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体を取得します。|

## <a name="remarks"></a>Remarks
 シンボル プロバイダーは、オブジェクトとその特定のスコープ内の位置 (関数、メソッド、クラスなど) を表すこのインターフェイスを返します。 このインターフェイスは、シンボル プロバイダーと式エバリュエーターのさまざまなメソッドから返され、渡されます。 通常、シンボル プロバイダーは、このインターフェイスの内容を解釈する必要がある唯一のエンティティです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
