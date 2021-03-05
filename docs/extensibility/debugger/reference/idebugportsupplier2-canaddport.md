---
description: ポート供給業者が新しいポートを追加できることを確認します。
title: 'IDebugPortSupplier2:: CanAddPort |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5c53abba81b02aa6125d4fa25ce16db85579ce5c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142662"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
ポート供給業者が新しいポートを追加できることを確認します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanAddPort( 
   void 
);
```

```csharp
int CanAddPort();
```

## <a name="return-value"></a>戻り値
 ポートを追加できる場合はを返し `S_OK` ます。それ以外の場合はを返し、 `S_FALSE` このポートサプライヤーにポートを追加できないことを示します。

## <a name="remarks"></a>解説
 このメソッドは、 [Addport](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) メソッドを呼び出す前に呼び出します。後者の方法では、ポートが作成され、追加されるため、時間がかかることがあります。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
