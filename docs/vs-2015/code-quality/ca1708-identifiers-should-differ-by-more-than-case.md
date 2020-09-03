---
title: 'CA1708: 識別子は大文字と小文字を区別しないと異なる必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldDifferByMoreThanCase
- CA1708
helpviewer_keywords:
- CA1708
- IdentifiersShouldDifferByMoreThanCase
ms.assetid: dac0f01d-dd21-484d-add1-c8cd2bf6969f
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 22a33c852b941b4c7e7398416aa1e74e69ff1786
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544041"
---
# <a name="ca1708-identifiers-should-differ-by-more-than-case"></a>CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|IdentifiersShouldDifferByMoreThanCase|
|CheckId|CA1708|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 2つの型、メンバー、パラメーター、または完全修飾名前空間の名前は、小文字に変換されるときは同じです。

## <a name="rule-description"></a>ルールの説明
 名前空間、型、メンバー、およびパラメーターの各識別子は、大文字/小文字以外のみでは区別できません。共通言語ランタイムを対象とする言語は、大文字と小文字を区別する必要はないためです。 たとえば、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] は、広く使用されている大文字と小文字を区別しない言語です。

 この規則は、パブリックに表示できるメンバーにのみ適用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 大文字と小文字を区別せずに他の識別子と比較する場合は、一意の名前を選択します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 ライブラリは、の使用可能なすべての言語で使用できない場合があり [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。

## <a name="example-of-a-violation"></a>違反の例
 次の例は、このルールの違反を示しています。

 [!code-csharp[FxCop.Naming.IdentifiersShouldDifferByMoreThanCase#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldDifferByMoreThanCase/cs/FxCop.Naming.IdentifiersShouldDifferByMoreThanCase.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
