---
title: MODULE_INFO_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FLAGS
helpviewer_keywords:
- MODULE_INFO_FLAGS enumeration
ms.assetid: e22d3723-b4d4-4524-8a2f-3adb55bbd273
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20a11488c32b4259105e346e7fa28fd706e48a48
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714229"
---
# <a name="module_info_flags"></a>MODULE_INFO_FLAGS
モジュールのシンボルの状態を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_INFO_FLAGS {
   MIF_SYMBOLS_LOADED = 0x0001
};
typedef DWORD MODULE_INFO_FLAGS;
```

```csharp
public enum enum_MODULE_INFO_FLAGS {
   MIF_SYMBOLS_LOADED = 0x0001
};
```

## <a name="fields"></a>フィールド
 `MIF_SYMBOLS_LOADED`\
 モジュールによって少なくとも 1 つのシンボル セットが読み込まれました (それ以外の場合はシンボルは読み込まれませんでした)。

## <a name="remarks"></a>Remarks
 この値は[、メソッドによって](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)返されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)
