---
title: IDebugポートサプライヤー2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2
helpviewer_keywords:
- IDebugPortSupplier2 interface
ms.assetid: 37067324-2ea6-4a01-8829-a6e9c7a70068
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddce454e6634d8cc177019e9d30b0ffcc7e7f1cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724474"
---
# <a name="idebugportsupplier2"></a>IDebugPortSupplier2
このインターフェイスは、セッション デバッグ マネージャー (SDM) にポートを提供します。

## <a name="syntax"></a>構文

```
IDebugPortSupplier2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
カスタム ポート サプライヤーは、ポート サプライヤーを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
ポートサプライヤー`CoCreateInstance`との呼び出しは`GUID`、このインターフェイスを返します(これは、このインターフェイスを取得する一般的な方法です)。 次に例を示します。

```cpp
IDebugPortSupplier2 *GetPortSupplier(GUID *pPortSupplierGuid)
{
    IDebugPortSupplier2 *pPS = NULL;
    if (pPortSupplierGuid != NULL) {
        CComPtr<IDebugPortSupplier2> spPortSupplier;
        spPortSupplier.CoCreateInstance(*pPortSupplierGuid);
        if (spPortSupplier != NULL) {
            pPS = spPortSupplier.Detach();
        }
    }
    return (pPS);
}
```

[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)の呼び出しは、このインターフェイスを返します[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]。

- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)は、ポートを作成したポートサプライヤーを表すこのインターフェイスを返します。

- [インターフェイス](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)の`IDebugPortSupplier`一覧を表します (`IEnumDebugPortSuppliers`インターフェイスは[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)から取得され、登録されているすべてのポート サプライヤを表[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]します)。

通常、デバッグ エンジンはポート サプライヤーと対話しません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に`IDebugPortSupplier2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetPortSupplierName](../../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)|ポートサプライヤー名を取得します。|
|[GetPortSupplierId](../../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)|ポートの仕入先の識別子を取得します。|
|[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)|ポート サプライヤーからポートを取得します。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)|既に存在するポートを列挙します。|
|[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)|ポート サプライヤーが新しいポートの追加をサポートしていることを確認します。|
|[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)|ポートを追加します。|
|[RemovePort](../../../extensibility/debugger/reference/idebugportsupplier2-removeport.md)|ポートを削除します。|

## <a name="remarks"></a>Remarks
ポート サプライヤーは、名前と ID で自身を識別し、ポートを追加および削除し、ポート サプライヤーが提供するすべてのポートを列挙できます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
