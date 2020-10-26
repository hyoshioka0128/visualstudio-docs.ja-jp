---
title: 信頼性に関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 250eb10581858534ec6325a1bfb61d84bddac05a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72603973"
---
# <a name="reliability-warnings"></a>信頼性に関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

信頼性の警告は、正しいメモリやスレッドの使用など、ライブラリとアプリケーションの信頼性をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA2000:スコープを失う前にオブジェクトを破棄](../code-quality/ca2000-dispose-objects-before-losing-scope.md)|例外的なイベントが発生するとオブジェクトのファイナライザーを実行できないため、オブジェクトに対するすべての参照がスコープ外になる前に、オブジェクトを明示的に破棄する必要があります。|
|[CA2001:問題が発生する可能性のあるメソッドは呼び出しません](../code-quality/ca2001-avoid-calling-problematic-methods.md)|メンバーが危険性または問題のあるメソッドを呼び出します。|
|[CA2002:弱い ID を伴うオブジェクト上でロックしません](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。|
|[CA2003:ファイバーをスレッドとして扱いません](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|マネージスレッドは Win32 スレッドとして扱われています。|
|[CA2004:GC.KeepAlive への呼び出しを削除します](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|SafeHandle の使用法に変換する場合は、GC のすべての呼び出しを削除します。KeepAlive (オブジェクト)。 この場合、クラスは GC を呼び出す必要がありません。KeepAlive。ファイナライザーがなくても、SafeHandle に依存してそれらの OS ハンドルを最終処理することを前提としています。|
|[CA2006:SafeHandle を使用して、ネイティブ リソースを要約します](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|マネージド コードで IntPtr を使用すると、セキュリティ上の問題および信頼性の問題が発生する可能性があります。 すべての IntPtr の使用状況をレビューして、SafeHandle または類似のテクノロジに置き換える必要があるかどうかを判断してください。|
