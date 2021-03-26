---
description: デバッグのためにプロセスが起動された理由を指定します。
title: DEBUG_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REASON
helpviewer_keywords:
- DEBUG_REASON enumeration
ms.assetid: ad2ee898-8648-4671-9078-d32873862346
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db5d6697f222015cc4f6dbedbc6258e00c9b285f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096253"
---
# <a name="debug_reason"></a>DEBUG_REASON
デバッグのためにプロセスが起動された理由を指定します。

## <a name="syntax"></a>Syntax

```cpp
enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
typedef DWORD DEBUG_REASON;
```

```csharp
public enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
```

## <a name="fields"></a>フィールド
`DEBUG_REASON_ERROR`\
特定できないエラーが発生しました (これは、他の理由がいずれも満たされていない場合の既定の条件として使用されます)。

`DEBUG_REASON_USER_LAUNCHED`\
ユーザーの要求でプロセスが起動されました。

`DEBUG_REASON_USER_ATTACHED`\
既に実行中のプロセスが、ユーザーによってにアタッチされました。

`DEBUG_REASON_AUTO_ATTACHED`\
プロセスは、起動されたときに自動的にアタッチされました。

`DEBUG_REASON_CAUSALITY`\
*ジャストインタイム*(JIT) デバッグイベントが発生したため、プロセスが起動されました。

## <a name="remarks"></a>注釈
[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)メソッドから返されます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)
