---
description: 使用可能なデバッグエンジンの一意の識別子の配列を記述します。
title: GUID_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GUID_ARRAY structure
ms.assetid: 9e12500c-2c1c-49b1-a0ba-e08366c97eb8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cbdc8465bef0795649fef5b169a221a3e7b7178c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162421"
---
# <a name="guid_array"></a>GUID_ARRAY
使用可能なデバッグエンジンの一意の識別子の配列を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagGUID_ARRAY
{
    DWORD dwCount;
    GUID *Members;
} GUID_ARRAY;
```

```csharp
public struct GUID_ARRAY
{
    public uint dwCount;
    public Guid Members;
}
```

## <a name="members"></a>メンバー
`dwCount`\
配列内の一意の識別子の数。

`Members`\
一意の識別子を格納している配列。

## <a name="remarks"></a>解説
この構造体は、 [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md) メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)
