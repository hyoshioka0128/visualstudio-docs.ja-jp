---
title: DEBUG_REASON |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REASON
helpviewer_keywords:
- DEBUG_REASON enumeration
ms.assetid: ad2ee898-8648-4671-9078-d32873862346
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59954ea7e89390a5e35dbe0bfb0412da1aabc80f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737424"
---
# <a name="debug_reason"></a>DEBUG_REASON
デバッグのためにプロセスが起動された理由を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
typedef DWORD DEBUG_REASON;
```

```csharp
public enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
```

## <a name="fields"></a>フィールド
`DEBUG_REASON_ERROR`\
非特定エラーが発生しました (これは、他の理由のいずれも適合しない場合にデフォルトの条件として使用されます)。

`DEBUG_REASON_USER_LAUNCHED`\
プロセスはユーザーの要求で起動されました。

`DEBUG_REASON_USER_ATTACHED`\
既に実行されているプロセスは、ユーザーによってアタッチされました。

`DEBUG_REASON_AUTO_ATTACHED`\
プロセスは、起動時に自動的にアタッチされました。

`DEBUG_REASON_CAUSALITY`\
このプロセスは、*ジャスト イン タイム*(JIT) デバッグ イベントにより起動されました。

## <a name="remarks"></a>Remarks
[メソッドから](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)
