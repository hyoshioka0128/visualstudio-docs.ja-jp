---
title: 'CA1061: 基底クラスのメソッドを非表示にします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1061
- DoNotHideBaseClassMethods
helpviewer_keywords:
- DoNotHideBaseClassMethods
- CA1061
ms.assetid: 0bda9dc8-87b4-4038-ab9d-563298387466
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c884eb569d5682326d2dc667363f991467171386
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533355"
---
# <a name="ca1061-do-not-hide-base-class-methods"></a>CA1061:基底クラス メソッドを非表示にしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotHideBaseClassMethods|
|CheckId|CA1061|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 派生型は、その基本メソッドの1つと同じ名前とパラメーター数を持つメソッドを宣言します。1つ以上のパラメーターが、基本メソッドの対応するパラメーターの基本型です。また、その他のパラメーターには、基本メソッドの対応するパラメーターと同じ型があります。

## <a name="rule-description"></a>ルールの説明
 派生メソッドのパラメーターシグネチャが、基本メソッドのパラメーターシグネチャ内の対応する型よりも弱い派生型である場合、基本型のメソッドは派生型の同じ名前のメソッドによって非表示になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドを削除するか名前を変更するか、またはメソッドが基本メソッドを非表示にしないようにパラメーターシグネチャを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反するメソッドを示しています。

 [!code-csharp[FxCop.Design.HideBaseMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.HideBaseMethod/cs/FxCop.Design.HideBaseMethod.cs#1)]
