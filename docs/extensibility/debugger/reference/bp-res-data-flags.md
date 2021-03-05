---
description: データブレークポイントをエミュレートするか、ハードウェアで実装するかを指定します。
title: BP_RES_DATA_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RES_DATA_FLAGS
helpviewer_keywords:
- BP_RES_DATA_FLAGS enumeration
ms.assetid: d97611e2-def6-45a9-ad7d-eedf2ad4c82b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bf1d27e876da5fdc0f95ecea0e9ba96c0a687bb1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144105"
---
# <a name="bp_res_data_flags"></a>BP_RES_DATA_FLAGS
データブレークポイントをエミュレートするか、ハードウェアで実装するかを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_RES_DATA_FLAGS {
    BP_RES_DATA_EMULATED = 0x0001
};
typedef DWORD BP_RES_DATA_FLAGS;
```

```csharp
public enum enum_BP_RES_DATA_FLAGS {
    BP_RES_DATA_EMULATED = 0x0001
};
```

## <a name="fields"></a>フィールド
`BP_RES_DATA_EMULATED`\
データブレークポイントをエミュレートすることを指定します。

## <a name="remarks"></a>解説
`dwFlags` [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)構造体のメンバーに使用されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
