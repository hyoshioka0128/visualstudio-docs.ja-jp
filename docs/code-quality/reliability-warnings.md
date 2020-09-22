---
title: 信頼性の規則
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- rules, reliability
- reliability rules
- managed code analysis rules, reliability rules
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e0a35b9c49f2eb5655eeb67721b0fafdbbe1e087
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808273"
---
# <a name="reliability-rules"></a>信頼性の規則

信頼性規則は、正しいメモリやスレッドの使用など、ライブラリとアプリケーションの信頼性をサポートします。

|ルール|説明|
|----------|-----------------|
|[CA2000:スコープを失う前にオブジェクトを破棄](../code-quality/ca2000.md)|例外的なイベントが発生するとオブジェクトのファイナライザーを実行できないため、オブジェクトに対するすべての参照がスコープ外になる前に、オブジェクトを明示的に破棄する必要があります。|
|[CA2002:弱い ID を伴うオブジェクト上でロックしません](../code-quality/ca2002.md)|アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。|
|[CA2007:タスクを直接待機しないでください](../code-quality/ca2007.md)|非同期メソッドは[awaits](/dotnet/csharp/language-reference/keywords/await) 、を <xref:System.Threading.Tasks.Task> 直接待機します。|
|[CA2008:TaskScheduler を渡さずにタスクを作成しない](../code-quality/ca2008.md)|タスクの作成または継続操作で、パラメーターを指定しないメソッドオーバーロードが使用さ <xref:System.Threading.Tasks.TaskScheduler> れています。|
|[CA2009: ImmutableCollection 値で ToImmutableCollection を呼び出さないでください](../code-quality/ca2009.md)|`ToImmutable` メソッドは、名前空間から変更できないコレクションで不必要に呼び出されました <xref:System.Collections.Immutable> 。|
|[CA2011: セッター内でプロパティを割り当てません](../code-quality/ca2011.md) | プロパティに、独自の [set アクセサー](/dotnet/csharp/programming-guide/classes-and-structs/using-properties#the-set-accessor)内で誤って値が割り当てられました。 |
|[CA2012: ValueTask を正しく使用する必要があります](../code-quality/ca2012.md) | メンバーの呼び出しから返される ValueTasks は、直接待機することを意図しています。  ValueTask を複数回使用しようとするか、完了する前に1つの結果に直接アクセスすると、例外または破損が発生する可能性があります。  このような ValueTask を無視すると、機能的なバグが示され、パフォーマンスが低下する可能性があります。 |
|[CA2013: 値の型と共に ReferenceEquals を使用しないでください](../code-quality/ca2013.md) | を使用して値を比較するときに <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> 、obja と Obja が値型の場合、メソッドに渡される前にボックス化され <xref:System.Object.ReferenceEquals%2A> ます。 これは、objA と Obja の両方が値型の同じインスタンスを表している場合でも、 <xref:System.Object.ReferenceEquals%2A> メソッドは false を返すことを意味します。 |
|[CA2014: ループで stackalloc を使用しないでください。](../code-quality/ca2014.md) | Stackalloc によって割り当てられるスタック領域は、現在のメソッドの呼び出しの最後にのみ解放されます。  ループでこれを使用すると、スタックが無制限に増加し、最終的にスタックオーバーフロー状態になる可能性があります。 |
|[CA2015: MemoryManager T から派生した型に対してファイナライザーを定義しません &lt;&gt;](../code-quality/ca2015.md) | から派生した型にファイナライザーを追加する <xref:System.Buffers.MemoryManager%601> と、メモリがによってまだ使用されている間は解放される可能性があり <xref:System.Span%601> ます。 |
|[CA2016:CancellationToken パラメーターを 1 つのメソッドに転送する](ca2016.md) | 操作の `CancellationToken` キャンセル通知が適切に反映されるように、またはトークンを意図的に伝達し `CancellationToken.None` ないことを示すために明示的に渡すメソッドにパラメーターを転送します。 |
