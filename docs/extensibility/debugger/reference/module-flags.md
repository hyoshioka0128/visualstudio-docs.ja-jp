---
title: MODULE_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_FLAGS
helpviewer_keywords:
- MODULE_FLAGS enumeration
ms.assetid: 0e555b42-b846-4dbb-812e-8e3d11c85b2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 78c7f24d64ffca667706c3b2fcebeffad16a9d85
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714262"
---
# <a name="module_flags"></a>MODULE_FLAGS
モジュールを記述するために使用します。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_FLAGS { 
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
public enum enum_MODULE_FLAGS { 
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
 システム モジュールを指定します。

 `MODULE_FLAG_SYMBOLS`\
 シンボル モジュールを指定します。

 `MODULE_FLAG_64BIT`\
 64 ビット モジュールを指定します。

 `MODULE_FLAG_OPTIMIZED`\
 モジュールが最適化されたことを示します。 この状態は **、[モジュール]** ウィンドウに反映されます。

 `MODULE_FLAG_UNOPTIMIZED`\
 モジュールが最適化されていない場合を指定します。 この状態は **、[モジュール]** ウィンドウに反映されます。 これが既定の状態です。

## <a name="remarks"></a>Remarks
 MODULE_INFO構造体の`m_dwModuleFlags`メンバーに使用[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)されます。

 これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
