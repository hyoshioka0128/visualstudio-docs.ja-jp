---
title: BP_RES_DATA_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RES_DATA_FLAGS
helpviewer_keywords:
- BP_RES_DATA_FLAGS enumeration
ms.assetid: d97611e2-def6-45a9-ad7d-eedf2ad4c82b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d0b687a54ddc1ed111b664a819dacfed6709196d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737866"
---
# <a name="bp_res_data_flags"></a>BP_RES_DATA_FLAGS
データ ブレークポイントをエミュレートするか、ハードウェアで実装するかを指定します。

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
データ ブレークポイントがエミュレートされることを指定します。

## <a name="remarks"></a>Remarks
BP_RESOLUTION_DATA構造体の`dwFlags`メンバーに使用[BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
