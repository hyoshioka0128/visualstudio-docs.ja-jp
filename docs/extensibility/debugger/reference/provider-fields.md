---
description: プログラムプロバイダーに関連付けられているプロパティを指定します。
title: PROVIDER_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FIELDS
helpviewer_keywords:
- PROVIDER_FIELDS enumeration
ms.assetid: 39631545-2b0e-45b4-978b-d63656484b02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a1ab410d9780078cd786b75f14d0321498eca8fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079541"
---
# <a name="provider_fields"></a>PROVIDER_FIELDS
プログラムプロバイダーに関連付けられているプロパティを指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_PROVIDER_FIELDS {
   PFIELD_PROGRAM_NODES       = 0x01,
   PFIELD_IS_DEBUGGER_PRESENT = 0x02
};
typedef DWORD PROVIDER_FIELDS;
```

```csharp
public enum enum_PROVIDER_FIELDS {
   PFIELD_PROGRAM_NODES       = 0x01,
   PFIELD_IS_DEBUGGER_PRESENT = 0x02
};
```

## <a name="fields"></a>フィールド
 `PFIELD_PROGRAM_NODES`\
 `ProgramNodes`フィールドは有効です。

 `PFIELD_IS_DEBUGGER_PRESENT`\
 `fIsDebuggerPresent`フィールドは有効です。

## <a name="remarks"></a>注釈
 これらの値は、 `Fields` 構造体のどのフィールドが明示的に入力されたかを示すために、 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) 構造体のメンバーに返されます。

 これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
