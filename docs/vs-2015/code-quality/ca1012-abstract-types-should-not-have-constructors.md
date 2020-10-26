---
title: 'CA1012: 抽象型にはコンストラクターを含めることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AbstractTypesShouldNotHaveConstructors
- CA1012
helpviewer_keywords:
- CA1012
ms.assetid: 09f458ac-dd88-4cd7-a47f-4106c1e80ece
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2c88144e788fb35a3c330aa28b4e9d8b91ff8003
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545458"
---
# <a name="ca1012-abstract-types-should-not-have-constructors"></a>CA1012:抽象型にはコンストラクターを含めません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AbstractTypesShouldNotHaveConstructors|
|CheckId|CA1012|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック型は abstract であり、パブリックコンストラクターを持ちます。

## <a name="rule-description"></a>ルールの説明
 抽象型上のコンストラクターは、派生型からのみ呼び出すことができます。 パブリック コンストラクターで型のインスタンスが作成され、抽象型のインスタンスは自分で作成できないため、パブリック コンストラクターが含まれる抽象型のデザインは不適切になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、コンストラクターを保護するか、型を abstract として宣言しないようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 抽象型にはパブリックコンストラクターがあります。

## <a name="example"></a>例
 次の例には、この規則に違反する抽象型が含まれています。

 [!code-csharp[FxCop.Design.AbstractTypeBad#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeBad/cs/FxCop.Design.AbstractTypeBad.cs#1)]
 [!code-vb[FxCop.Design.AbstractTypeBad#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeBad/vb/FxCop.Design.AbstractTypeBad.vb#1)]

## <a name="example"></a>例
 次の例では、コンストラクターのアクセシビリティをからに変更することによって、以前の違反を修正し `public` `protected` ます。

 [!code-csharp[FxCop.Design.AbstractTypeGood#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeGood/cs/FxCop.Design.AbstractTypeGood.cs#1)]
 [!code-vb[FxCop.Design.AbstractTypeGood#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeGood/vb/FxCop.Design.AbstractTypeGood.vb#1)]
