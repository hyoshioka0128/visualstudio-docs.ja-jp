---
description: このインターフェイスは、セッションデバッグマネージャー (SDM) にポートを提供します。
title: IDebugPortSupplier2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2
helpviewer_keywords:
- IDebugPortSupplier2 interface
ms.assetid: 37067324-2ea6-4a01-8829-a6e9c7a70068
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5e9523212ea83182e69e83b4f8353f1a9ba7dd8c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172040"
---
# <a name="idebugportsupplier2"></a>IDebugPortSupplier2
このインターフェイスは、セッションデバッグマネージャー (SDM) にポートを提供します。

## <a name="syntax"></a>構文

```
IDebugPortSupplier2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
カスタムポート供給業者は、このインターフェイスを実装して、ポート供給元を表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
ポート供給業者を使用してを呼び出すと、 `CoCreateInstance` `GUID` このインターフェイスが返されます (これは、このインターフェイスを取得するための一般的な方法です)。 次に例を示します。

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

[Getportsupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)を呼び出すと、によって使用されている現在のポート供給を表すインターフェイスが返され [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。

- [Getportsupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md) は、ポートを作成したポートサプライヤーを表すこのインターフェイスを返します。

- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) は、インターフェイスの一覧を表し `IDebugPortSupplier` `IEnumDebugPortSuppliers` ます (インターフェイスは、に登録されているすべてのポートサプライヤーを表す、 [enumportsuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)から取得され [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます)。

通常、デバッグエンジンは、ポート供給元と対話しません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、のメソッドを示し `IDebugPortSupplier2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetPortSupplierName](../../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)|ポートのサプライヤー名を取得します。|
|[GetPortSupplierId](../../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)|ポートサプライヤー識別子を取得します。|
|[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)|ポートサプライヤーからポートを取得します。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)|既に存在するポートを列挙します。|
|[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)|ポートサプライヤーが新しいポートの追加をサポートしていることを確認します。|
|[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)|ポートを追加します。|
|[RemovePort](../../../extensibility/debugger/reference/idebugportsupplier2-removeport.md)|ポートを削除します。|

## <a name="remarks"></a>解説
ポートサプライヤーは、名前と ID で自身を識別したり、ポートを追加および削除したり、ポート供給元が提供するすべてのポートを列挙したりできます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
