---
title: 'CA1053: スタティックホルダー型はコンストラクターを含むことはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldNotHaveConstructors
- CA1053
helpviewer_keywords:
- CA1053
- StaticHolderTypesShouldNotHaveConstructors
ms.assetid: 10302b9a-fa5e-4935-a06a-513d9600f613
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 29cc322dd59dc0de66af8f92a46524d15b0022c7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539582"
---
# <a name="ca1053-static-holder-types-should-not-have-constructors"></a>CA1053:スタティック ホルダー型はコンストラクターを含むことはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|StaticHolderTypesShouldNotHaveConstructors|
|CheckId|CA1053|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型または入れ子になったパブリック型で、静的なメンバーのみが宣言されています。また、パブリックまたはプロテクトの既定のコンストラクターが含まれます。

## <a name="rule-description"></a>ルールの説明
 静的メンバーの呼び出しに型のインスタンスは必要ないため、コンストラクターは不要です。 また、型には非静的メンバーがないため、インスタンスを作成しても、型のメンバーへのアクセスは提供されません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、既定のコンストラクターを削除するか、またはプライベートにします。

> [!NOTE]
> コンパイラによっては、型でコンストラクターが定義されていない場合に、パブリックな既定のコンストラクターが自動的に作成されます。 これが型の場合は、プライベートな既定のコンストラクターを追加して違反を排除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 コンストラクターが存在する場合は、型が静的な型ではないことを示します。

## <a name="example"></a>例
 次の例は、この規則に違反する型を示しています。 ソースコードに既定のコンストラクターがないことに注意してください。 このコードがアセンブリにコンパイルされると、C# コンパイラによって既定のコンストラクターが挿入され、この規則に違反することになります。 これを修正するには、プライベートコンストラクターを宣言します。

 [!code-csharp[FxCop.Design.StaticTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticTypes/cs/FxCop.Design.StaticTypes.cs#1)]
