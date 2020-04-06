---
title: IEnum デバッグフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields
helpviewer_keywords:
- IEnumDebugFields interface
ms.assetid: 403c2a51-3ba5-431f-a1dd-2f3b2046c00c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d577ff2f5848f2cb348bcaccf57875507018634b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716783"
---
# <a name="ienumdebugfields"></a>IEnumDebugFields
このインターフェイスは[、IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugFields : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは[、IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスを実装するオブジェクトのセットを提供するシンボル プロバイダーによって実装されます。 [GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)メソッドが存在するため、これは標準の COM 列挙体ではありません。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、[メソッド フィールドの名前](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)と[名前空間を使用して返されます。](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugfields-next.md)|列挙体から[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトの次のセットを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugfields-skip.md)|指定した数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugfields-reset.md)|列挙を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugfields-clone.md)|現在の列挙体のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)|列挙体のエントリ数を取得します。|

## <a name="remarks"></a>Remarks

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)
- [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)
