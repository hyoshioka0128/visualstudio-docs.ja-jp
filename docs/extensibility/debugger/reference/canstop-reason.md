---
description: プログラムの実行を特定の時点に達した後に実行を停止できるかどうかを判断するために使用されます。
title: CANSTOP_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CANSTOP_REASON
helpviewer_keywords:
- CANSTOP_REASON enumeration
ms.assetid: 6da944eb-36cd-4a8c-8d71-544c775cfcc1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39a22a0534a464e9899e666550b31ab24503c05d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096526"
---
# <a name="canstop_reason"></a>CANSTOP_REASON
プログラムの実行を特定の時点に達した後に実行を停止できるかどうかを判断するために使用されます。

## <a name="syntax"></a>Syntax

```cpp
enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
typedef DWORD CANSTOP_REASON;
```

```csharp
public enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
```

## <a name="fields"></a>フィールド
`CANSTOP_ENTRYPOINT`\
指定されたプログラムのエントリポイントを指定します。

`CANSTOP_STEPIN`\
関数へのステップインを指定します。

## <a name="remarks"></a>注釈
プログラムのエントリポイントに到達した後、または関数またはメソッドにステップインした後に、セッションデバッグマネージャー (SDM) で確認するために、 [Getreason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) メソッドに引数として渡されます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
