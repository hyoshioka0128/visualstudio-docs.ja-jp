---
title: メソッドを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a3b0c8c16b10a4cf2268161d8a2db96c10303b1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738648"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger メソッド
現在アクティブなすべての<xref:System.Threading.Tasks.TaskScheduler>オブジェクトの配列を取得します。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 この内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>戻り値
 この<xref:System.AppDomain>で現在アクティブ<xref:System.Threading.Tasks.TaskScheduler>になっているすべてのオブジェクトの配列。

## <a name="remarks"></a>Remarks
 このメソッドはスレッド セーフではないため、他の<xref:System.Threading.Tasks.TaskScheduler>インスタンスと同時に使用しないでください。 デバッガーが他のすべてのスレッドを中断した場合にのみ、デバッガーからこのメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [タスクスケジューラクラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
