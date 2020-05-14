---
title: タスク スケジューラ クラス - 内部メンバー |マイクロソフトドキュメント
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
ms.openlocfilehash: a53abc8b24edb06445c23c19744d00d50de8735d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712563"
---
# <a name="taskscheduler-class---internal-members"></a>タスク スケジューラ クラス - 内部メンバー
この資料では、カスタム デバッガーの実装<xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>に役立つクラスの内部メンバーについて説明します。 このクラスの一般的な情報については、<xref:System.Threading.Tasks.TaskScheduler>リファレンス記事を参照してください。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 これらの内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler
       extends System.Object
```

## <a name="members"></a>メンバー

### <a name="methods"></a>メソッド

|名前|説明|
|----------|-----------------|
|[デバッガのスケジュールされたタスクを取得します。](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|すべてのスケジュールされたタスクの配列を取得します。|
|[タスク スケジューラを取得します。](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|現在アクティブなすべての<xref:System.Threading.Tasks.TaskScheduler>オブジェクトの配列を取得します。|

## <a name="remarks"></a>Remarks

## <a name="see-also"></a>関連項目
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [NET フレームワークの並列拡張内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
