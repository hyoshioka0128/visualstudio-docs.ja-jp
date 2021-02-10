---
title: 'IDebugProgram2:: CanDetach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bdaff16923023598793dfdf9200105cc6b158ccb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99936133"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
デバッグエンジン (DE) をプログラムからデタッチできるかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>戻り値
 がデタッチできる場合はを返します。 `S_OK` それ以外の場合はエラーコードを返します。 `S_FALSE`DE がプログラムからデタッチできない場合は、を返します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
