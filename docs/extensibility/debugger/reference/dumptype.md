---
description: ダンプするプログラムの状態 (スレッドの実行、スタックフレーム、現在の命令アドレスなど) の量を指定します。
title: DUMPTYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DUMPTYPE
helpviewer_keywords:
- DUMPTYPE enumeration
ms.assetid: ea8160db-8732-4056-a1d7-892ef72da71e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cef9f90c1f08dac742a6f01a4dd48f6bff76848b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150979"
---
# <a name="dumptype"></a>DUMPTYPE
ダンプするプログラムの状態 (スレッドの実行、スタックフレーム、現在の命令アドレスなど) の量を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
typedef DWORD DUMPTYPE;
```

```csharp
public enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
```

## <a name="fields"></a>フィールド
`DUMP_MINIDUMP`\
小さいコンパクトなダンプを指定します。

`DUMP_FULLDUMP`\
大きな完全なダンプを指定します。

## <a name="remarks"></a>解説
[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)メソッドに引数として渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)
