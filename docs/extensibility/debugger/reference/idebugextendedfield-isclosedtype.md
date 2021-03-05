---
description: フィールドが閉じられた型を表すかどうかを判断します。
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
ms.openlocfilehash: 4f13fa0f143ac6adb8fb3493621b7ef638a394ca
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152118"
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
