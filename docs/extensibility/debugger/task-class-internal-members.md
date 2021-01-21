---
title: Task クラス-Internal Members |Microsoft Docs
description: カスタムデバッガーの実装に役立つ、システムの内部メンバーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f18de66a524fbc652b8153c5b34b4464cda60f5
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996020"
---
# <a name="task-class---internal-members"></a>タスククラス-内部メンバー
この記事では、カスタムデバッガーの実装に役立つクラスの内部メンバーについて説明し <xref:System.Threading.Tasks.Task?displayProperty=fullName> ます。 このクラスに関する一般的な情報については、リファレンス記事を参照してください <xref:System.Threading.Tasks.Task> 。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
.class public auto ansi System.Threading.Tasks.Task
       extends System.Object
       implements System.Threading.IThreadPoolWorkItem,
                  System.IAsyncResult,
                  System.IDisposable,
                  System.Threading.ICancelableOperation
```

## <a name="members"></a>メンバー

### <a name="methods"></a>メソッド

|名前|説明|
|----------|-----------------|
|[SetNotificationForWaitCompletion メソッド](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状態ビットを設定またはクリアします。|
|[NotifyDebuggerOfWaitCompletion メソッド](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|デバッガーによってブレークポイントターゲットとして使用されるプレースホルダーメソッド。|

### <a name="fields"></a>フィールド

|名前|説明|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|オブジェクトで実行するコードを表すデリゲート <xref:System.Threading.Tasks.Task> 。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|オブジェクトの追加のプロパティを格納 <xref:System.Threading.Tasks.Task> します。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|親プロパティのバッキングフィールド <xref:System.Threading.Tasks.Task?displayProperty=fullName> 。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|オブジェクトの現在の状態に関する情報を格納 <xref:System.Threading.Tasks.Task> します。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|アクションで使用されるデータを表すオブジェクト。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|プロパティのバッキングフィールド <xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName> 。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|オブジェクトの次に使用できる識別子 <xref:System.Threading.Tasks.Task> 。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|実行状態に到達する前にタスクがキャンセルされたこと、またはタスクが取り消しを確認し、例外なしで完了したことを示します。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|タスクが実行されていることを示します。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|未処理の例外のためにタスクが完了したことを示します。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|タスクの実行が正常に完了したことを示します。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|タスクがデリゲートの実行を完了し、アタッチされた子タスクが終了するのを暗黙的に待機していることを示します。|

## <a name="remarks"></a>注釈
 次の内部メソッドは、開始をコード実行にマークするため、デバッガーエンジンに役立ち <xref:System.Threading.Tasks.Task> ます。

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>こちらもご覧ください
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [.NET Framework の並列拡張の内部構造](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
