---
title: .NET Framework | の並列拡張機能の内部構造Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738273"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>.NET Framework の並列拡張の内部構造
このセクションでは、.NET Framework に対する並列拡張のカスタムデバッガーを実装するのに役立つクラスの内部型、メソッド、およびフィールドについて説明します。

## <a name="in-this-section"></a>このセクションの内容
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md) クラスの内部データメンバーについて説明し <xref:System.Threading.Tasks.Task?displayProperty=fullName> ます。

 [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md) クラスの内部データメンバーについて説明し <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> ます。

 [ContingentProperties クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md) クラスの内部データメンバーについて説明し `System.Threading.Tasks.ContingentProperties` ます。

 [AsyncTaskMethodBuilder 構造体](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md) 構造体の内部メンバーを記述し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> ます。

 [AsyncTaskMethodBuilder \<TResult> 構造](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md) 体の内部メンバーを記述し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> ます。

 [AsyncVoidMethodBuilder 構造体](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md) 構造体の内部メンバーを記述し <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> ます。

## <a name="see-also"></a>関連項目
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [並列プログラミング](/dotnet/standard/parallel-programming/index)
