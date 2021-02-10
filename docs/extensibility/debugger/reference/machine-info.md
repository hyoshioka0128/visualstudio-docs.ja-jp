---
title: MACHINE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO
helpviewer_keywords:
- MACHINE_INFO structure
ms.assetid: e7564ff2-00b5-4750-8fd5-dc1029a16912
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c37819234d794226a41625f3c2e9eccd1b69066c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938812"
---
# <a name="machine_info"></a>MACHINE_INFO
特定のコンピューターについて説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagMACHINE_INFO { 
   MACHINE_INFO_FIELDS Fields;
   BSTR                bstrName;
   MACHINE_INFO_FLAGS  Flags;
} MACHINE_INFO;
```

```csharp
public struct MACHINE_INFO { 
   public uint   Fields;
   public string bstrName;
   public uint   Flags;
};
```

## <a name="members"></a>メンバー
 `Fields`\
 構造体のどのフィールドが初期化されるかを指定する、 [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md) 列挙型のフラグの組み合わせ。

 `bstrName`\
 コンピューター名。 [Getmachinename](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)の呼び出しと同じです。

 `Flags`\
 コンピューターの属性を記述する [MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md) 列挙型のフラグの組み合わせ。

## <a name="remarks"></a>解説
 この構造体は、 [Getmachineinfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md) メソッドの呼び出しによって返されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
