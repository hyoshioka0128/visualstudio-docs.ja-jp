---
title: 'CA1017: ComVisibleAttribute | を使用してアセンブリをマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1017
- MarkAssembliesWithComVisible
helpviewer_keywords:
- MarkAssembliesWithComVisible
- CA1017
ms.assetid: 4842cb49-8dd8-4e5d-a2d6-ceeaf6c6cf8e
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 17f0a540a436316d3a4fb3b71a2a51b1c5a90a6d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535071"
---
# <a name="ca1017-mark-assemblies-with-comvisibleattribute"></a>CA1017:アセンブリに ComVisibleAttribute を設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|MarkAssembliesWithComVisible|
|CheckId|CA1017|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 アセンブリに属性が適用されていません <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> 。

## <a name="rule-description"></a>ルールの説明
 属性は、 <xref:System.Runtime.InteropServices.ComVisibleAttribute> COM クライアントがマネージコードにアクセスする方法を決定します。 アセンブリで COM の参照範囲を明示することをお勧めします。 COM の可視性は、アセンブリ全体に対して設定し、個々の型および型のメンバーに対してオーバーライドできます。 属性が存在しない場合、アセンブリの内容は COM クライアントから参照できます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性をアセンブリに追加します。 アセンブリが COM クライアントに表示されないようにするには、属性を適用し、その値をに設定し `false` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 アセンブリを表示する場合は、属性を適用し、その値をに設定し `true` ます。

## <a name="example"></a>例
 次の例は、 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性が COM クライアントに表示されないようにするために属性が適用されているアセンブリを示しています。

 [!code-cpp[FxCop.Design.AssembliesCom#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/cpp/FxCop.Design.AssembliesCom.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesCom#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/cs/FxCop.Design.AssembliesCom.cs#1)]
 [!code-vb[FxCop.Design.AssembliesCom#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/vb/FxCop.Design.AssembliesCom.vb#1)]

## <a name="see-also"></a>関連項目
 [相互運用のための .Net 型を満たす](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[アンマネージコードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
