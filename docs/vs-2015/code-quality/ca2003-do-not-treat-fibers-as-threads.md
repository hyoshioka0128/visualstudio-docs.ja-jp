---
title: 'CA2003: ファイバーをスレッドとして扱いません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a8172490b267949686dd3390c85ed6d86531b192
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521175"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003:ファイバーをスレッドとして扱いません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 マネージスレッドは Win32 スレッドとして扱われています。

## <a name="rule-description"></a>ルールの説明
 マネージスレッドが Win32 スレッドであると想定しないでください。 ファイバーです。 共通言語ランタイム (CLR) は、SQL によって所有されている実際のスレッドのコンテキストで、マネージスレッドをファイバーとして実行します。 これらのスレッドは、SQL Server プロセス内の複数の Appdomain とデータベース間で共有できます。 マネージスレッドローカルストレージを使用することはできますが、アンマネージスレッドローカルストレージを使用したり、現在の OS スレッドでコードを再実行したりすることはできません。 スレッドのロケールなどの設定は変更しないでください。 P/Invoke を使用して CreateCriticalSection または Createmutex にを呼び出さないでください。そのためには、ロックを開始するスレッドもロックを終了する必要があります。 これはファイバーを使用する場合には当てはまりません。そのため、SQL では Win32 の重要なセクションとミューテックスは役に立ちません。 マネージドシステムの Thread オブジェクトでは、ほとんどの状態を安全に使用できます。 これには、マネージスレッドローカルストレージと、スレッドの現在のユーザーインターフェイス (UI) カルチャが含まれます。 ただし、プログラミングモデルの理由により、SQL を使用する場合、スレッドの現在のカルチャを変更することはできません。これは、新しいアクセス許可を使用して適用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 スレッドの使用状況を確認し、それに応じてコードを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールを抑制しないでください。
