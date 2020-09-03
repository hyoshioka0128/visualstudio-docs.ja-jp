---
title: GUID_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GUID_ARRAY structure
ms.assetid: 9e12500c-2c1c-49b1-a0ba-e08366c97eb8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e163674b5622146ef1a270920dc7458dce2e3993
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736646"
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
