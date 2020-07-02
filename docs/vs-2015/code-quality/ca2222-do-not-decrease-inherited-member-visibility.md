---
title: 'CA2222: 継承されたメンバーの可視性を下げません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
helpviewer_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
ms.assetid: 066c8675-381f-43cc-956c-d757cc494028
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 04109e821d3a739b96ad63e1a441089a5d479cd8
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540778"
---
# <a name="ca2222-do-not-decrease-inherited-member-visibility"></a>CA2222:継承されたメンバーの参照範囲を縮小しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|DoNotDecreaseInheritedMemberVisibility|
|CheckId|CA2222|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 シールされていない型のプライベートメソッドには、基本型で宣言されたパブリックメソッドと同一のシグネチャがあります。 プライベートメソッドは final ではありません。

## <a name="rule-description"></a>ルールの説明
 継承メンバーのアクセス修飾子は変更しないでください。 継承メンバーをプライベートに変更しても、呼び出し元はメソッドの基本クラスの実装にアクセスできます。 メンバーがプライベートになり、型がシールされていない場合、継承する型は継承階層内のメソッドの最後のパブリック実装を呼び出すことができます。 アクセス修飾子を変更する必要がある場合は、メソッドを final に設定するか、メソッドがオーバーライドされないようにその型を sealed にする必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、アクセスを非プライベートに変更します。 または、プログラミング言語でサポートされている場合は、メソッドを final にすることができます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、この規則に違反する型を示しています。

 [!code-csharp[FxCop.Usage.InheritedPublic#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InheritedPublic#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/vb/FxCop.Usage.InheritedPublic.vb#1)]
