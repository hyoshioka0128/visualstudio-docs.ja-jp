---
title: 'IDebugExtendedField:: IsClosedType |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IsClosedType
- IDebugExtendedField::IsClosedType
ms.assetid: 9136fc57-74ff-4fe4-a6e2-b137cb9d5b08
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 404b1852e0db27673ea62569b25013a7f999f16d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915489"
---
# <a name="idebugextendedfieldisclosedtype"></a>IDebugExtendedField::IsClosedType
フィールドが閉じられた型を表すかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsClosedType(
   void
);
```

```csharp
int IsClosedType();
```

## <a name="return-value"></a>戻り値
 フィールドが閉じられた型の場合はを返します `S_OK` 。それ以外の場合はを返し `S_FALSE` ます。

## <a name="see-also"></a>関連項目
- [IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)
