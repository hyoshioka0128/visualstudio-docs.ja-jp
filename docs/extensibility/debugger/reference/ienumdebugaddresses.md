---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 14b42ec37babe72b47b0e832397d33029c4fc3d1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717590"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
このインターフェイスは[、IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは[、IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイスを実装するオブジェクトのセットを提供するシンボル プロバイダーによって実装されます。 [GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)メソッドが存在するため、これは標準の COM 列挙体ではありません。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、コンテキストと[GetAddressesFrom](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md) [位置](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)によって返されます。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|列挙体から[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)オブジェクトの次のセットを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|指定した数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|列挙を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|現在の列挙体のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|列挙体のエントリ数を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、通常、式エバリュエーターに与える適切なアドレスを決定するために、デバッグ エンジンによって使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
