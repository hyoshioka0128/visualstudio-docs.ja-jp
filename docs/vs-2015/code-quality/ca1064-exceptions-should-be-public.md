---
title: 'CA1064: 例外は public | である必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1064
- ExceptionsShouldBePublic
helpviewer_keywords:
- ExceptionsShouldBePublic
- CA1064
ms.assetid: 83eb224c-2456-4368-acf4-3b3378e67759
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fc78c4eaacc3ef0a480b913d20537aeebe5bfc01
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539270"
---
# <a name="ca1064-exceptions-should-be-public"></a>CA1064:例外は public として設定する必要があります
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ExceptionsShouldBePublic|
|CheckId|CA1064|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 パブリックでない例外は、、、 <xref:System.Exception> またはから直接派生 <xref:System.SystemException> <xref:System.ApplicationException> します。

## <a name="rule-description"></a>ルールの説明
 内部例外は、独自の内部スコープ内でのみ表示されます。 内部スコープの外側にある例外は、基本例外を使用しなければキャッチできません。 内部例外が、、またはから継承されている場合、外部コードには、例外の処理 <xref:System.Exception> <xref:System.SystemException> 内容を <xref:System.ApplicationException> 認識するのに十分な情報がありません。

 ただし、後で内部例外のベースとして使用されるパブリック例外がコードにある場合は、さらに詳細なコードが基本例外でインテリジェントな処理を実行できると想定することが妥当です。 パブリック例外には、T:System.Exception、T:System.SystemException、または T:System.ApplicationException. によって提供されるものよりも多くの情報が含まれます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 例外をパブリックにするか、、、またはではないパブリック例外から内部例外を派生させ <xref:System.Exception> <xref:System.SystemException> <xref:System.ApplicationException> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 常にプライベート例外が独自の内部スコープ内でキャッチされる場合は、この規則からのメッセージを抑制します。

## <a name="example"></a>例
 この規則は、最初の例のメソッドである FirstCustomException で、例外クラスが例外から直接派生し、内部であるために発生します。 このルールは、クラスは例外から直接派生していますが、クラスは public として宣言されているため、このクラスでは起動されません。 3番目のクラスは <xref:System.Exception?displayProperty=fullName> 、、 <xref:System.SystemException?displayProperty=fullName> 、またはから直接派生していないため、ルールを起動しません <xref:System.ApplicationException?displayProperty=fullName> 。

 [!code-csharp[FxCop.Design.ExceptionsShouldBePublic.CA1064#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.design.exceptionsshouldbepublic.ca1064/cs/ca1064 - exceptionsshouldbepublic.cs#1)]
