---
title: CONST_GUID_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONST_GUID_ARRAY
helpviewer_keywords:
- CONST_GUID_ARRAY structure
ms.assetid: bd55e7d8-372c-4c3e-9eed-28f6b415a5db
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c0021ef24e0cafec0119263d2c74175f0d38d784
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737633"
---
# <a name="const_guid_array"></a>CONST_GUID_ARRAY
のリストを保持する構造体 `GUID` 。

## <a name="syntax"></a>構文

```cpp
typedef struct tagCONST_GUID_ARRAY {
    DWORD       dwCount;
    CONST GUID* Members;
} CONST_GUID_ARRAY;
```

```csharp
public struct CONST_GUID_ARRAY {
    public uint   dwCount;
    public Guid[] Members;
}
```

## <a name="members"></a>メンバー
`dwCount`\
`GUID`配列内のの数 `Members` 。

`Members`\
の配列 `GUID` 。

## <a name="remarks"></a>解説
この構造体は、 [Publishprogram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) メソッドに渡され、 [Getproviderprocessdata](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) メソッドと [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md) メソッドから返されます。

この構造体のインスタンスの所有者は、割り当てられたメモリを解放します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
