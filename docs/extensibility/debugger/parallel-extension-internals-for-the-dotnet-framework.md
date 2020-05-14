---
title: NET フレームワークの並列拡張内部 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6a3583e94a0bfff4474db03aa9d083add921f3da
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738273"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>NET フレームワークの並列拡張内部
このセクションでは、.NET Framework への並列拡張機能のカスタム デバッガーを実装するのに役立つクラスの内部型、メソッド、およびフィールドについて説明します。

## <a name="in-this-section"></a>このセクションの内容
 [タスククラス](../../extensibility/debugger/task-class-internal-members.md)クラスの内部データ メンバーについて説明<xref:System.Threading.Tasks.Task?displayProperty=fullName>します。

 [タスクスケジューラクラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)クラスの内部データ メンバーについて説明<xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>します。

 [偶発プロパティ クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md)クラスの内部データ メンバーについて説明`System.Threading.Tasks.ContingentProperties`します。

 [構造体](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md)構造体の内部メンバーについて説明します<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>。

 [構造体の内部メンバー\<](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md)を表す構造体>を作成します。 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>

 [構造体](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md)構造体の内部メンバーについて説明します<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>。

## <a name="see-also"></a>関連項目
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [並列プログラミング](/dotnet/standard/parallel-programming/index)
