---
title: PROGRAM_DESTROY_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- PROGRAM_DESTROY_FLAGS enumeration
ms.assetid: be00d4a3-d5b8-4159-b632-64577f534883
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c2ddb00e2cf70055c34335d8f2123004eb031a05
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713838"
---
# <a name="program_destroy_flags"></a>PROGRAM_DESTROY_FLAGS
プログラム破棄フラグの有効な値を列挙します。

## <a name="syntax"></a>構文

```cpp
enum enum_PPROGRAM_DESTROY_FLAGS
{
   PROGRAM_DESTROY_CONTINUE_DEBUGGING = 0x1
};
typedef DWORD PROGRAM_DESTROY_FLAGS;
```

```csharp
public enum enum_PPROGRAM_DESTROY_FLAGS
{
   PROGRAM_DESTROY_CONTINUE_DEBUGGING = 0x1
};
```

## <a name="fields"></a>フィールド
 `PROGRAM_DESTROY_CONTINUE_DEBUGGING`\
 プログラムを破棄しますが、デバッグを続行します。

## <a name="remarks"></a>Remarks
 列挙体は[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)メソッドによって返されます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)
