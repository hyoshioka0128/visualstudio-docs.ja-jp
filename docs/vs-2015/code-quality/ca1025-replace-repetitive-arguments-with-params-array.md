---
title: 'CA1025: 反復する引数を params array | で置き換えます。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1025
- ReplaceRepetitiveArgumentsWithParamsArray
helpviewer_keywords:
- ReplaceRepetitiveArgumentsWithParamsArray
- CA1025
ms.assetid: f009b340-dea3-4459-8fe1-2143aa8b5d0b
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 84809341d7898aeb3defe0447f2a2f1142eb460a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546628"
---
# <a name="ca1025-replace-repetitive-arguments-with-params-array"></a>CA1025:反復する引数を params 配列で置き換えます
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ReplaceRepetitiveArgumentsWithParamsArray|
|CheckId|CA1025|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック型のパブリックメソッドまたはプロテクトメソッドに3つ以上のパラメーターがあり、その最後の3つのパラメーターが同じ型です。

## <a name="rule-description"></a>ルールの説明
 引数の正確な数が不明で、可変個の引数が同じ型である場合、または同じ型として渡すことができる場合は、引数を繰り返す代わりにパラメーター配列を使用します。 たとえば、メソッドは、 <xref:System.Console.WriteLine%2A> パラメーター配列を使用して任意の数の引数を受け入れる汎用オーバーロードを提供し <xref:System.Object> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、繰り返し引数をパラメーター配列に置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは常に安全です。ただし、このような設計では、ユーザビリティの問題が発生する可能性があります。

## <a name="example"></a>例
 次の例は、この規則に違反する型を示しています。

 [!code-csharp[FxCop.Design.RepeatArgs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RepeatArgs/cs/FxCop.Design.RepeatArgs.cs#1)]
