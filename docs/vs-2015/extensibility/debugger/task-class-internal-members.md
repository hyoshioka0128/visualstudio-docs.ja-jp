---
title: Task クラス-Internal Members |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ef0cd907c25a90ee90e3ed23a773d0ae8ba0ce1f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841517"
---
# <a name="task-class---internal-members"></a>Task クラス - 内部メンバー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このトピックでは、カスタムデバッガーの実装に役立つクラスの内部メンバーについて説明し <xref:System.Threading.Tasks.Task?displayProperty=fullName> ます。 このクラスに関する一般的な情報については、リファレンストピックを参照してください <xref:System.Threading.Tasks.Task> 。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
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
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|タスクが実行状態に到達する前に取り消されたか、タスクが取り消しを確認し、例外なしで完了したことを示します。|  
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
  
## <a name="see-also"></a>参照  
 <xref:System.Threading.Tasks.Task?displayProperty=fullName>   
 [.NET Framework の並列拡張機能の内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
