---
title: Getscheduledタスク Fordebugger メソッド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- GetScheduledTasksForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 7c9b4cde-6e4a-4cef-929f-7d02b1da5762
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b4ac6fa753be7672f1e698bda231bd11217c10d4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152736"
---
# <a name="getscheduledtasksfordebugger-method"></a>GetScheduledTasksForDebugger メソッド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

すべてのスケジュールされたタスクの配列を取得します。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 .NET Framework からこの内部メンバーにアクセスすることはできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.method assembly hidebysig instance class System.Threading.Tasks.Task[] GetScheduledTasksForDebugger() cil managed  
```  
  
## <a name="return-value"></a>戻り値  
 すべてのスケジュールされたタスクの配列。 各タスクが実行中であるか、実行が完了しています。  
  
## <a name="remarks"></a>注釈  
 このメソッドはスレッドセーフではなく、の他のインスタンスと同時に使用することはできません <xref:System.Threading.Tasks.TaskScheduler> 。デバッガーが他のすべてのスレッドを中断した場合にのみ、デバッガーから呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
