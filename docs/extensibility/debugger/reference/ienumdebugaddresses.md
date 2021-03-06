---
description: このインターフェイスは、IDebugAddress インターフェイスを実装するオブジェクトのコレクションを表します。
title: IEnumDebugAddresses |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ea9e4115c1664e1dcd05041f7ece056b5de01dae
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222641"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
このインターフェイスは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するオブジェクトのセットを提供するために、シンボルプロバイダーによって実装されます。 これは、 [GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md) メソッドが存在するため、標準の COM 列挙ではないことに注意してください。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、 [Getアドレス Fromcontext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md) と [Getアドレス fromposition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)によって返されます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|列挙体から次の [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトのセットを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|指定された数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|列挙体を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|現在の列挙体のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|列挙体のエントリ数を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、通常、式エバリュエーターに渡す適切なアドレスを決定するために、デバッグエンジンによって使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
