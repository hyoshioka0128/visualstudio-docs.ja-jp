---
title: 'IEnumDebugBoundBreakpoints2:: GetCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2::GetCount
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2::GetCount
ms.assetid: 5a572eeb-beb7-4fc7-8259-792d277069be
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 059ac49ebec0d8a7ef1a9aa54dab085a2cbf525c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875693"
---
# <a name="ienumdebugboundbreakpoints2getcount"></a>IEnumDebugBoundBreakpoints2::GetCount
列挙体の要素の数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCount(
   ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>パラメーター
`pcelt`\
入出力列挙体の要素の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは `Next` 、、、 `Clone` `Skip` 、およびメソッドのみを `Reset` 実装する必要があることを指定する、慣例的な COM 列挙インターフェイスの一部ではありません。

## <a name="see-also"></a>関連項目
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
