---
description: デバッグ起動フラグを指定します。
title: LAUNCH_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- LAUNCH_FLAGS
helpviewer_keywords:
- LAUNCH_FLAGS enumeration
ms.assetid: f51aab02-d257-4302-bb79-b7d8ba9ac4e5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e12dc587a77e428d3d4c4740043ab5651b7897a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058002"
---
# <a name="launch_flags"></a>LAUNCH_FLAGS
デバッグ起動フラグを指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_LAUNCH_FLAGS {
    LAUNCH_DEBUG      = 0x0000,
    LAUNCH_NODEBUG    = 0x0001,
    LAUNCH_ENABLE_ENC = 0x0002,
    LAUNCH_MERGE_ENV  = 0x0004
};
typedef DWORD LAUNCH_FLAGS;
```

```csharp
public enum enum_LAUNCH_FLAGS {
    LAUNCH_DEBUG      = 0x0000,
    LAUNCH_NODEBUG    = 0x0001,
    LAUNCH_ENABLE_ENC = 0x0002,
    LAUNCH_MERGE_ENV  = 0x0004
};
```

## <a name="fields"></a>フィールド
`LAUNCH_DEBUG`\
デバッグのプロセスを起動します。

`LAUNCH_NODEBUG`\
デバッグせずにプロセスを起動します。

`LAUNCH_ENABLE_ENC`\
非推奨です。使用しないでください。

`LAUNCH_MERGE_ENV`\
プロセスを起動し、環境を起動中のホストにマージします。

## <a name="remarks"></a>注釈
これらの値は、 [Launchsuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) メソッドに引数として渡されます。

これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
