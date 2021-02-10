---
title: MACHINE_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO_FIELDS
helpviewer_keywords:
- MACHINE_INFO_FIELDS enumeration
ms.assetid: 2d61d206-7d40-4df1-8c88-1b3c9c78821e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 70d289315219fd6e49f528a5ec95d560191b5cc4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962068"
---
# <a name="machine_info_fields"></a>MACHINE_INFO_FIELDS
特定のコンピューターに対して取得する情報の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
typedef DWORD MACHINE_INFO_FIELDS;
```

```csharp
public enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
```

## <a name="fields"></a>フィールド
 `MCIF_NAME`\
 構造体のフィールドを初期化/使用し `bstrName` ます。

 `MCIF_FLAGS`\
 構造体のフィールドを初期化/使用し `Flags` ます。

 `MIF_ALL`\
 構造体のすべてのフィールドを初期化/使用します。

## <a name="remarks"></a>解説
 これらの値は、 [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)構造体のどのメンバーを初期化するかを示すために[getmachineinfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)メソッドに渡されます。

 また、 `Fields` 構造体のメンバーで、使用され `MACHINE_INFO` ているフィールドと有効なフィールドを示すためにも使用されます。

 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
