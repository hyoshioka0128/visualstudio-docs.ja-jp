---
title: TaskScheduler クラス-Internal Members |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TaskScheduler class [.NET Framework debug engines]
- debug engines, TaskScheduler class [.NET Framework]
ms.assetid: 87f1c969-0217-4464-8907-7609c1bf61d3
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 427a84b3dcda0471f5ec9d71883a5a8e859bb92d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176700"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler クラスの内部メンバー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このトピックでは、カスタムデバッガーの実装に役立つクラスの内部メンバーについて説明し <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> ます。 このクラスに関する一般的な情報については、リファレンストピックを参照してください <xref:System.Threading.Tasks.TaskScheduler> 。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler  
       extends System.Object  
```  
  
## <a name="members"></a>メンバー  
  
### <a name="methods"></a>メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[Getscheduledタスク Fordebugger](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|すべてのスケジュールされたタスクの配列を取得します。|  
|[GetTaskSchedulersForDebugger](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|現在アクティブなすべてのオブジェクトの配列を取得 <xref:System.Threading.Tasks.TaskScheduler> します。|  
  
## <a name="remarks"></a>注釈  
  
## <a name="see-also"></a>参照  
 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>   
 [.NET Framework の並列拡張機能の内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
