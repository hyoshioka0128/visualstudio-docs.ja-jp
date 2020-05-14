---
title: メソッドのスケジュールタスクを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetScheduledTasksForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 7c9b4cde-6e4a-4cef-929f-7d02b1da5762
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fca6c8e92cd0b4755bd79b8e142a7e1d283f868d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738662"
---
# <a name="getscheduledtasksfordebugger-method"></a>GetScheduledTasksForDebugger メソッド
すべてのスケジュールされたタスクの配列を取得します。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 この内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.method assembly hidebysig instance class System.Threading.Tasks.Task[] GetScheduledTasksForDebugger() cil managed
```

## <a name="return-value"></a>戻り値
 スケジュールされたすべてのタスクの配列。 各タスクは実行中か、実行が終了しています。

## <a name="remarks"></a>Remarks
 このメソッドはスレッド セーフではないため、他の<xref:System.Threading.Tasks.TaskScheduler>インスタンスと同時に使用しないでください。 デバッガーが他のすべてのスレッドを中断した場合にのみ、デバッガーからこのメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [タスクスケジューラクラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
