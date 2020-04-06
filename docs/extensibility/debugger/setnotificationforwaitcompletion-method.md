---
title: メソッドを待つ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 226ac41c8e3b7427ac3b9aba7bea08dbb7329d16
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712871"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion メソッド
TASK_STATE_WAIT_COMPLETION_NOTIFICATION状態ビットを設定またはクリアします。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

## <a name="syntax"></a>構文

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>パラメーター
 `enabled`

 `true`ビットを設定します。`false`をクリックしてビットを設定解除します。

## <a name="exceptions"></a>例外

## <a name="remarks"></a>Remarks
 デバッガーは、非同期メソッド本体からステップ アウトするのに役立つこのビットを設定します。 の`enabled`場合`true`、このメソッドは、まだ完了していないタスクでのみ呼び出す必要があります。 の`enabled`場合`false`、このメソッドは完了したタスクで呼び出すことができます。 どちらの場合も、promise スタイルのタスクにのみ使用する必要があります。

## <a name="requirements"></a>必要条件

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
