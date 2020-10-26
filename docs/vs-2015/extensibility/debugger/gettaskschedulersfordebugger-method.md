---
title: GetTaskSchedulersForDebugger メソッド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 995bf40669a4480f6f1ddfe8071a7885a4659c9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152722"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger メソッド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在アクティブなすべてのオブジェクトの配列を取得 <xref:System.Threading.Tasks.TaskScheduler> します。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 .NET Framework からこの内部メンバーにアクセスすることはできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed  
```  
  
## <a name="return-value"></a>戻り値  
 <xref:System.Threading.Tasks.TaskScheduler>こので現在アクティブなすべてのオブジェクトの配列 <xref:System.AppDomain> 。  
  
## <a name="remarks"></a>注釈  
 このメソッドはスレッドセーフではなく、の他のインスタンスと同時に使用することはできません <xref:System.Threading.Tasks.TaskScheduler> 。 デバッガーが他のすべてのスレッドを中断した場合にのみ、デバッガーから呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
