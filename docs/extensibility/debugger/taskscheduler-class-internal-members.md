---
title: TaskScheduler クラス-Internal Members |Microsoft Docs
description: カスタムデバッガーの実装に役立つ TaskScheduler クラスの内部メンバーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TaskScheduler class [.NET Framework debug engines]
- debug engines, TaskScheduler class [.NET Framework]
ms.assetid: 87f1c969-0217-4464-8907-7609c1bf61d3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 10528e57137f8605e7f140d4ab8d4a3399029a5f
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996007"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler クラスの内部メンバー
この記事では、カスタムデバッガーの実装に役立つクラスの内部メンバーについて説明し <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> ます。 このクラスに関する一般的な情報については、リファレンス記事を参照してください <xref:System.Threading.Tasks.TaskScheduler> 。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
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

## <a name="see-also"></a>こちらもご覧ください
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [.NET Framework の並列拡張の内部構造](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
