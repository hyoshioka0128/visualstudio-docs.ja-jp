---
title: 'CA2200: スタックの詳細を保持するための再スロー |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RethrowToPreserveStackDetails
- CA2200
helpviewer_keywords:
- CA2200
- RethrowToPreserveStackDetails
ms.assetid: 046e1b98-c4dc-4515-874f-9c0de2285621
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6d63ef6ff3647742e931fd05f59c66b40059ad00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546368"
---
# <a name="ca2200-rethrow-to-preserve-stack-details"></a>CA2200:スタック詳細を保持するために再度スローします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|RethrowToPreserveStackDetails|
|CheckId|CA2200|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 例外が再スローされ、ステートメントで例外が明示的に指定され `throw` ます。

## <a name="rule-description"></a>ルールの説明
 例外がスローされると、それに含まれる情報の一部がスタックトレースになります。 スタックトレースは、例外をスローするメソッドで始まり、例外をキャッチするメソッドで終了するメソッド呼び出し階層のリストです。 ステートメントで例外を指定することによって例外が再スローされた場合 `throw` 、現在のメソッドでスタックトレースが再開され、例外をスローした元のメソッドと現在のメソッドとの間のメソッド呼び出しのリストが失われます。 例外と共に元のスタックトレース情報を保持するには、 `throw` 例外を指定せずにステートメントを使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、例外を明示的に指定せずに例外を再スローします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に `CatchAndRethrowExplicitly` 違反するメソッドと、規則を満たすメソッドを示して `CatchAndRethrowImplicitly` います。

 [!code-csharp[FxCop.Usage.Rethrow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/cs/FxCop.Usage.Rethrow.cs#1)]
 [!code-vb[FxCop.Usage.Rethrow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/vb/FxCop.Usage.Rethrow.vb#1)]
