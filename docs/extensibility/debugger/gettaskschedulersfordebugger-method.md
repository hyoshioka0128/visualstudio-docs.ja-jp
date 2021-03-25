---
description: 現在アクティブなすべての TaskScheduler オブジェクトの配列を取得します。
title: GetTaskSchedulersForDebugger メソッド |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d024e44dee8e7513d862e3d299c2ed2b9e53cd5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054856"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger メソッド
現在アクティブなすべてのオブジェクトの配列を取得 <xref:System.Threading.Tasks.TaskScheduler> します。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>戻り値
 <xref:System.Threading.Tasks.TaskScheduler>こので現在アクティブなすべてのオブジェクトの配列 <xref:System.AppDomain> 。

## <a name="remarks"></a>注釈
 このメソッドはスレッドセーフではなく、の他のインスタンスと同時に使用することはできません <xref:System.Threading.Tasks.TaskScheduler> 。 デバッガーが他のすべてのスレッドを中断した場合にのみ、このメソッドをデバッガーから呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
