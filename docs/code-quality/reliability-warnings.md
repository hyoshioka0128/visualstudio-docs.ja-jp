---
title: 信頼性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e936222a95681796f5c5ca423d122995e1ea5f79
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76113255"
---
# <a name="reliability-warnings"></a>信頼性に関する警告

信頼性の警告は、正しいメモリやスレッドの使用など、ライブラリとアプリケーションの信頼性をサポートします。 信頼性の規則は次のとおりです。

|規則|説明|
|----------|-----------------|
|[CA2000: スコープが失われる前にオブジェクトを破棄します](../code-quality/ca2000.md)|例外的なイベントが発生するとオブジェクトのファイナライザーを実行できないため、オブジェクトに対するすべての参照がスコープ外になる前に、オブジェクトを明示的に破棄する必要があります。|
|[CA2001: 問題が発生する可能性のあるメソッドは呼び出しません](../code-quality/ca2001.md)|メンバーが危険性または問題のあるメソッドを呼び出します。|
|[CA2002: ID が不十分なオブジェクトをロックしないでください](../code-quality/ca2002.md)|アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。|
|[CA2003: ファイバーをスレッドとして扱いません](../code-quality/ca2003.md)|マネージスレッドは Win32 スレッドとして扱われています。|
|[CA2004: GC.KeepAlive への呼び出しを削除します](../code-quality/ca2004.md)|SafeHandle の使用法に変換する場合は、GC のすべての呼び出しを削除します。KeepAlive (オブジェクト)。 この場合、クラスは GC を呼び出す必要がありません。KeepAlive。ファイナライザーがなくても、SafeHandle に依存してそれらの OS ハンドルを最終処理することを前提としています。|
|[CA2006: SafeHandle を使用して、ネイティブ リソースを要約します](../code-quality/ca2006.md)|マネージド コードで IntPtr を使用すると、セキュリティ上の問題および信頼性の問題が発生する可能性があります。 すべての IntPtr の使用状況をレビューして、SafeHandle または類似のテクノロジに置き換える必要があるかどうかを判断してください。|
|[CA2007: タスクを直接待機しない](../code-quality/ca2007.md)|非同期メソッドは、を<xref:System.Threading.Tasks.Task>直接[待機](/dotnet/csharp/language-reference/keywords/await)します。|
