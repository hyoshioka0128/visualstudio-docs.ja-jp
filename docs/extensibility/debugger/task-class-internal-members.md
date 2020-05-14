---
title: タスク クラス - 内部メンバ |マイクロソフトドキュメント
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
ms.openlocfilehash: dcf278c0248b344cea4be7cf161ecc91581f5f2e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712735"
---
# <a name="task-class---internal-members"></a>タスク クラス - 内部メンバー
この資料では、カスタム デバッガーの実装<xref:System.Threading.Tasks.Task?displayProperty=fullName>に役立つクラスの内部メンバーについて説明します。 このクラスの一般的な情報については、<xref:System.Threading.Tasks.Task>リファレンス記事を参照してください。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 これらの内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

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
|[SetNotificationForWaitCompletion メソッド](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|TASK_STATE_WAIT_COMPLETION_NOTIFICATION状態ビットを設定またはクリアします。|
|[NotifyDebuggerOfWaitCompletion メソッド](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|デバッガーによってブレークポイント ターゲットとして使用されるプレースホルダー メソッド。|

### <a name="fields"></a>フィールド

|名前|説明|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|<xref:System.Threading.Tasks.Task>オブジェクトで実行するコードを表すデリゲート。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|オブジェクトの追加プロパティを<xref:System.Threading.Tasks.Task>格納します。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|親プロパティの<xref:System.Threading.Tasks.Task?displayProperty=fullName>バッキング フィールド。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|オブジェクトの現在の状態に関する<xref:System.Threading.Tasks.Task>情報を格納します。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|アクションで使用されるデータを表すオブジェクト。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|<xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName>プロパティのバッキング フィールド。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|オブジェクトの次に使用可能な<xref:System.Threading.Tasks.Task>識別子。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|タスクが実行状態になる前にタスクがキャンセルされたことを示します。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|タスクが実行中であることを示します。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|ハンドルされない例外が原因でタスクが完了したことを示します。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|タスクが正常に実行されたことを示します。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|タスクがデリゲートの実行を完了し、アタッチされた子タスクが終了するのを暗黙的に待機していることを示します。|

## <a name="remarks"></a>Remarks
 次の内部メソッドは、コード実行の入り口を示すため<xref:System.Threading.Tasks.Task>、デバッガー エンジンにとって便利です。

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>関連項目
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [NET フレームワークの並列拡張内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
