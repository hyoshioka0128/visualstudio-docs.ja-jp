---
title: 'CA2104: 読み取り専用の変更可能な参照型を宣言しません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ff42cc2b8543fe8e1cf980a3574ae15922febf9b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85521044"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104:読み取り専用の変更可能な参照型を宣言しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 外部から参照できる型に、変更可能な参照型である、外部から参照可能な読み取り専用のフィールドがあります。

## <a name="rule-description"></a>ルールの説明
 変更可能な型とは、インスタンス データを変更できる型です。 クラスは、変更可能 <xref:System.Text.StringBuilder?displayProperty=fullName> な参照型の一例です。 このクラスには、クラスのインスタンスの値を変更できるメンバーが含まれています。 変更できない参照型の例として、 <xref:System.String?displayProperty=fullName> クラスがあります。 インスタンス化された後は、その値を変更することはできません。

 参照型フィールド (C++ ではポインター) で読み取り専用修飾子 (C# では[Readonly](https://msdn.microsoft.com/library/2f8081f6-0de2-4903-898d-99696c48d2f4) 、、では [readonly](https://msdn.microsoft.com/library/e868185d-6142-4359-a2fd-a7965cadfce8) 、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] c++ では [const](https://msdn.microsoft.com/library/b21c0271-1ad0-40a0-b21c-5e812bba0318) ) は、参照型の別のインスタンスによってフィールドが置換されないようにします。 ただし、修飾子を使用しても、フィールドのインスタンスデータが参照型によって変更されるのを防ぐことはできません。

 読み取り専用の配列フィールドはこのルールから除外されますが、代わりに [CA2105: array フィールド](../code-quality/ca2105-array-fields-should-not-be-read-only.md) には読み取り専用ルールを指定できません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、読み取り専用の修飾子を削除するか、互換性に影響する変更が許容される場合は、フィールドを変更できない型に置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 フィールドの種類が不変である場合は、このルールからの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、この規則に違反するフィールド宣言を示しています。

 [!code-cpp[FxCop.Security.MutableReferenceTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cpp/FxCop.Security.MutableReferenceTypes.cpp#1)]
 [!code-csharp[FxCop.Security.MutableReferenceTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cs/FxCop.Security.MutableReferenceTypes.cs#1)]
 [!code-vb[FxCop.Security.MutableReferenceTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/vb/FxCop.Security.MutableReferenceTypes.vb#1)]
