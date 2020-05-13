---
title: MACHINE_INFO_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO_FLAGS
helpviewer_keywords:
- MACHINE_INFO_FLAGS enumeration
ms.assetid: 1482095d-9a2e-4ef1-9e14-362c0b85194e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b74955d65ff34c4787de03c3b03383fe7eb702cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714507"
---
# <a name="machine_info_flags"></a>MACHINE_INFO_FLAGS
マシンを記述するために使用されます。

## <a name="syntax"></a>構文

```cpp
enum enum_MACHINE_INFO_FLAGS { 
   MCIFLAG_TERMINAL_SERVICES_AVAILABLE = 0x00000001
};
typedef DWORD MACHINE_INFO_FLAGS;
```

```csharp
public enum enum_MACHINE_INFO_FLAGS { 
   MCIFLAG_TERMINAL_SERVICES_AVAILABLE = 0x00000001
};
```

## <a name="fields"></a>フィールド
 `MCIFLAG_TERMINAL_SERVICES_AVAILABLE`\
 ターミナル サービスが利用可能であることを示します。

## <a name="remarks"></a>Remarks
 MACHINE_INFO構造体の`Flags`メンバーとして使用[MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
