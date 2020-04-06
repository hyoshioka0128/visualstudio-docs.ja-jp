---
title: オブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject
helpviewer_keywords:
- IDebugPointerObject interface
ms.assetid: 257fa167-b46e-4ffb-9a12-272efbf26702
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4b28189b3f0a07a27f5e4478f64963a63d634db5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725492"
---
# <a name="idebugpointerobject"></a>IDebugPointerObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、ポインター オブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugPointerObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、ポインター オブジェクトを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 インターフェイス[は](../../../extensibility/debugger/reference/idebugobject.md)、ポインターを表す場合は[、クエリ インターフェイス](/cpp/atl/queryinterface)を`IDebugObject`使用して、このインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [から](../../../extensibility/debugger/reference/idebugobject.md)継承されたメソッドに加えて、インターフェイスは`IDebugPointerObject`、次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[Dereference](../../../extensibility/debugger/reference/idebugpointerobject-dereference.md)|インターフェイスが指すオブジェクトを取得します。|
|[GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)|インターフェイスが連続する連続したバイトとして指す値を取得します。|
|[バイト数を設定](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)|一連の連続したバイトからインターフェイスが指す値を設定します。|

## <a name="remarks"></a>Remarks
 式エバリュエーターは、このインターフェイスを使用して、解析ツリー内のポインターを表します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
