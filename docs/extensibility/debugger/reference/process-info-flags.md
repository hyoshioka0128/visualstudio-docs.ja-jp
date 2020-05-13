---
title: PROCESS_INFO_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 36c4cbbe17a109eacd69b76500e8c10d21d2d554
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713965"
---
# <a name="process_info_flags"></a>PROCESS_INFO_FLAGS

プロセスのプロパティを記述または指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
typedef DWORD PROCESS_INFO_FLAGS;
```

```csharp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
```

## <a name="fields"></a>フィールド

`PIFLAG_SYSTEM_PROCESS`\
プロセスがシステム プロセスであることを示します。

`PIFLAG_DEBUGGER_ATTACHED`\
プロセスがデバッガーによってデバッグされていることを示します。 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]デバッガーである場合もあれば、WinDbg などの他のデバッガーである場合もあります。

`PIFLAG_PROCESS_STOPPED`\
プロセスが停止したことを示します。 また指定されている`PIFLAG_DEBUGGER_ATTACHED`場合のみ有効です。 Visual Studio 2005 以降で使用できます。

`PIFLAG_PROCESS_RUNNING`\
プロセスが実行中であることを示します。 また指定されている`PIFLAG_DEBUGGER_ATTACHED`場合のみ有効です。 Visual Studio 2005 以降で使用できます。

## <a name="remarks"></a>Remarks

PROCESS_INFO構造体の`Flags`メンバーに使用[PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)されます。

これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件

ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目

- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
