---
title: MODULE_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_FLAGS
helpviewer_keywords:
- MODULE_FLAGS enumeration
ms.assetid: 0e555b42-b846-4dbb-812e-8e3d11c85b2d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 41201194ee76f92b4faa101c4811c35b44a0d890
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961886"
---
# <a name="module_flags"></a>MODULE_FLAGS
モジュールを記述するために使用されます。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_FLAGS { 
   MODULE_FLAG_NONE        = 0x0000,
   MODULE_FLAG_SYSTEM      = 0x0001,
   MODULE_FLAG_SYMBOLS     = 0x0002,
   MODULE_FLAG_64BIT       = 0x0004,
   MODULE_FLAG_OPTIMIZED   = 0x0008,
   MODULE_FLAG_UNOPTIMIZED = 0x0010
};
typedef DWORD MODULE_FLAGS;
```

```csharp
public enum enum_MODULE_FLAGS { 
   MODULE_FLAG_NONE        = 0x0000,
   MODULE_FLAG_SYSTEM      = 0x0001,
   MODULE_FLAG_SYMBOLS     = 0x0002,
   MODULE_FLAG_64BIT       = 0x0004,
   MODULE_FLAG_OPTIMIZED   = 0x0008,
   MODULE_FLAG_UNOPTIMIZED = 0x0010
};
```

## <a name="fields"></a>フィールド
 `MODULE_FLAG_NONE`\
 モジュールを指定しません。

 `MODULE_FLAG_SYSTEM`\
 システムモジュールを指定します。

 `MODULE_FLAG_SYMBOLS`\
 シンボルモジュールを指定します。

 `MODULE_FLAG_64BIT`\
 64ビットモジュールを指定します。

 `MODULE_FLAG_OPTIMIZED`\
 モジュールが最適化されていることを指定します。 この状態は、[ **モジュール** ] ウィンドウに反映されます。

 `MODULE_FLAG_UNOPTIMIZED`\
 モジュールが最適化されていないことを指定します。 この状態は、[ **モジュール** ] ウィンドウに反映されます。 これが既定の状態です。

## <a name="remarks"></a>解説
 `m_dwModuleFlags` [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体のメンバーに使用されます。

 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
