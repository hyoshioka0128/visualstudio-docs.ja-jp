---
title: 'CA1047: SEALED: シールド型でプロテクトメンバーを宣言しません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareProtectedMembersInSealedTypes
- CA1047
helpviewer_keywords:
- CA1047
- DoNotDeclareProtectedMembersInSealedTypes
ms.assetid: 829033b5-a9d8-4f26-a719-45494c9dd035
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e115b4d327f1ac45673de491ceaffc90941e1111
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546784"
---
# <a name="ca1047-do-not-declare-protected-members-in-sealed-types"></a>CA1047:シールド型の保護されたメンバーを宣言しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotDeclareProtectedMembersInSealedTypes|
|CheckId|CA1047|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック型は `sealed` ( `NotInheritable` Visual basic では) であり、プロテクトメンバーまたは protected 入れ子にされた型を宣言します。 この規則は、メソッドの違反 <xref:System.Object.Finalize%2A> を報告しません。このパターンに従う必要があります。

## <a name="rule-description"></a>ルールの説明
 型でプロテクト メンバーを宣言するのは、継承する型からメンバーにアクセスまたはオーバーライドできるようにするためです。 定義上、シール型から継承することはできません。つまり、シール型のプロテクトメソッドを呼び出すことはできません。

 C# コンパイラは、このエラーの警告を発行します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メンバーのアクセスレベルをプライベートに変更するか、型を継承可能にします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 型を現在の状態のままにすると、メンテナンスの問題が発生する可能性があるため、利点はありません。

## <a name="example"></a>例
 次の例は、この規則に違反する型を示しています。

 [!code-csharp[FxCop.Design.SealedNoProtected#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.SealedNoProtected/cs/FxCop.Design.SealedNoProtected.cs#1)]
 [!code-vb[FxCop.Design.SealedNoProtected#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.SealedNoProtected/vb/FxCop.Design.SealedNoProtected.vb#1)]
