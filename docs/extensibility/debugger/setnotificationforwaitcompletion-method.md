---
title: SetNotificationForWaitCompletion メソッド |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712871"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion メソッド
TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状態ビットを設定またはクリアします。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

## <a name="syntax"></a>構文

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>パラメーター
 `enabled`

 `true` ビットを設定するには `false` ビットを設定解除します。

## <a name="exceptions"></a>例外

## <a name="remarks"></a>注釈
 デバッガーは、非同期のメソッド本体からステップアウトするために、このビットを設定します。 がの場合 `enabled` `true` 、このメソッドは、まだ完了していないタスクでのみ呼び出す必要があります。 がの場合 `enabled` は `false` 、完了したタスクに対してこのメソッドを呼び出すことができます。 どちらのイベントでも、promise スタイルのタスクにのみ使用してください。

## <a name="requirements"></a>必要条件

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
