---
title: PROVIDER_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FIELDS
helpviewer_keywords:
- PROVIDER_FIELDS enumeration
ms.assetid: 39631545-2b0e-45b4-978b-d63656484b02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 37f64b455ab0331f9b8f08da1f29a3e2c1b82fdf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713788"
---
# <a name="provider_fields"></a>PROVIDER_FIELDS
プログラム プロバイダーに関連付けられているプロパティを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PROVIDER_FIELDS {
   PFIELD_PROGRAM_NODES       = 0x01,
   PFIELD_IS_DEBUGGER_PRESENT = 0x02
};
typedef DWORD PROVIDER_FIELDS;
```

```csharp
public enum enum_PROVIDER_FIELDS {
   PFIELD_PROGRAM_NODES       = 0x01,
   PFIELD_IS_DEBUGGER_PRESENT = 0x02
};
```

## <a name="fields"></a>フィールド
 `PFIELD_PROGRAM_NODES`\
 フィールド`ProgramNodes`は有効です。

 `PFIELD_IS_DEBUGGER_PRESENT`\
 フィールド`fIsDebuggerPresent`は有効です。

## <a name="remarks"></a>Remarks
 これらの値は、構造体の`Fields`中で明示的に入力されたフィールドを示すために[、PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)構造体のメンバーに返されます。

 これらの値はビット単位`OR`で組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
