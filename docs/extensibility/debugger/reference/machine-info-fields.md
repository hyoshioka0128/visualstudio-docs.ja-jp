---
title: MACHINE_INFO_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO_FIELDS
helpviewer_keywords:
- MACHINE_INFO_FIELDS enumeration
ms.assetid: 2d61d206-7d40-4df1-8c88-1b3c9c78821e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89a2552bb6a8bea88f54a897b829ab89b30ff413
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714530"
---
# <a name="machine_info_fields"></a>MACHINE_INFO_FIELDS
特定のマシンに対して取得する情報の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
typedef DWORD MACHINE_INFO_FIELDS;
```

```csharp
public enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
```

## <a name="fields"></a>フィールド
 `MCIF_NAME`\
 構造体のフィールドを`bstrName`初期化/使用します。

 `MCIF_FLAGS`\
 構造体のフィールドを`Flags`初期化/使用します。

 `MIF_ALL`\
 構造体のすべてのフィールドを初期化/使用します。

## <a name="remarks"></a>Remarks
 これらの値は、[初期化するMACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)構造体のメンバーを示すために[、GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)メソッドに渡されます。

 構造体の`Fields`メンバーで使用され、`MACHINE_INFO`どのフィールドが使用され、有効かを示すこともできます。

 これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
