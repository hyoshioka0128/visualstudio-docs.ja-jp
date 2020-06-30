---
title: 'CA2219: 例外句で例外を発生させません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
helpviewer_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 960c74625a04b209dc9aa251256e994517a3a52f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538529"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219:exception 句に例外を発生させないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断しない、中断|

## <a name="cause"></a>原因
 `finally`、Filter、または fault 句から例外がスローされます。

## <a name="rule-description"></a>ルールの説明
 例外句で例外が発生すると、デバッグの難易度が大幅に向上します。

 または fault 句で例外が発生すると、 `finally` 新しい例外によってアクティブな例外が非表示になります (存在する場合)。 これにより、元のエラーの検出とデバッグが困難になります。

 フィルター句で例外が発生すると、ランタイムはその例外をサイレントにキャッチし、フィルターを false に評価します。 フィルターが false と評価され、フィルターによって例外がスローされるという違いを通知する方法はありません。 これにより、フィルターのロジックでエラーを検出してデバッグすることが難しくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 `finally` 、filter、または fault 句から明示的に例外を発生させないようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールの警告を抑制しないでください。 例外句で発生した例外によって実行コードに利点が得られるシナリオはありません。

## <a name="related-rules"></a>関連規則
 [CA1065:予期しない場所に例外を発生させません](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>関連項目
 [デザインの警告](../code-quality/design-warnings.md)
