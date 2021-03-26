---
description: 文字列の配列を記述する構造体。
title: BSTR_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BSTR_ARRAY
helpviewer_keywords:
- BSTR_ARRAY structure
ms.assetid: 48da37f7-a237-48a9-9ff9-389c1a00862c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5af4c0efe53625063d4bb714f3d323bef28c5954
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096617"
---
# <a name="bstr_array"></a>BSTR_ARRAY
文字列の配列を記述する構造体。

## <a name="syntax"></a>構文

```cpp
typedef struct tagBSTR_ARRAY {
    DWORD dwCount;
    BSTR* Members;
} BSTR_ARRAY;
```

```csharp
struct BSTR_ARRAY {
    DWORD    dwCount;
    string[] Members;
}
```

## <a name="members"></a>メンバー
`dwCount`\
配列内の文字列の数 `Members` 。

`Members`\
文字列の配列。

## <a name="remarks"></a>注釈
この構造体は、 [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md) メソッドから返されます。

 [C++ のみ]個々の文字列は、を使用して解放する必要があり、 `SysFreeString` `Members` 配列はで解放する必要があり `CoTaskMemFree` ます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)
