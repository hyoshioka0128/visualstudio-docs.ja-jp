---
title: ダンプタイプ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DUMPTYPE
helpviewer_keywords:
- DUMPTYPE enumeration
ms.assetid: ea8160db-8732-4056-a1d7-892ef72da71e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0d4d42709efdefe097b4c8a78a0b00f45f2e1a2b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737206"
---
# <a name="dumptype"></a>DUMPTYPE
プログラムの状態 (実行中のスレッド、スタック フレーム、現在の命令アドレスなど) のダンプ量を指定します。

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
小さい、コンパクトなダンプを指定します。

`DUMP_FULLDUMP`\
大きな完全なダンプを指定します。

## <a name="remarks"></a>Remarks
引数として[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)メソッドに渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)
