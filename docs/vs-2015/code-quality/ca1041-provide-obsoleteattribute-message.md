---
title: 'CA1041: ObsoleteAttribute message | を指定します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1041
- ProvideObsoleteAttributeMessage
helpviewer_keywords:
- ProvideObsoleteAttributeMessage
- CA1041
ms.assetid: be5bee69-d2d2-44e1-be2e-3ea451969003
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d738cf15ebe734cb74e553f38f6eb26af17e8cfd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542312"
---
# <a name="ca1041-provide-obsoleteattribute-message"></a>CA1041:ObsoleteAttribute メッセージを指定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ProvideObsoleteAttributeMessage|
|CheckId|CA1041|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 型またはメンバーが、プロパティが指定されていない属性を使用してマークされてい <xref:System.ObsoleteAttribute?displayProperty=fullName> <xref:System.ObsoleteAttribute.Message%2A?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 <xref:System.ObsoleteAttribute>は、非推奨のライブラリの型とメンバーをマークするために使用されます。 ライブラリコンシューマーは、古い形式に設定されている型またはメンバーを使用しないようにする必要があります。 これは、サポートされていない可能性があり、最終的にはライブラリの新しいバージョンから削除されるためです。 を使用してマークされている型またはメンバーがコンパイルされると <xref:System.ObsoleteAttribute> 、 <xref:System.ObsoleteAttribute.Message%2A> 属性のプロパティが表示されます。 これによって、ユーザーは旧式の型またはメンバーに関する情報を知ることができます。 通常、この情報には、ライブラリデザイナーによって使用されていない型またはメンバーがサポートされる期間、および使用する代わりに使用する代替の長さが含まれます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 `message` コンストラクターにパラメーターを追加し <xref:System.ObsoleteAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 <xref:System.ObsoleteAttribute.Message%2A>プロパティは互換性のために残されている型またはメンバーに関する重要な情報を提供するため、この規則による警告を抑制しないでください。

## <a name="example"></a>例
 次の例は、が正しく宣言されている古いメンバーを示して <xref:System.ObsoleteAttribute> います。

 [!code-cpp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cpp/FxCop.Design.ObsoleteAttributeOnMember.cpp#1)]
 [!code-csharp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cs/FxCop.Design.ObsoleteAttributeOnMember.cs#1)]
 [!code-vb[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/vb/FxCop.Design.ObsoleteAttributeOnMember.vb#1)]

## <a name="see-also"></a>関連項目
 <xref:System.ObsoleteAttribute?displayProperty=fullName>
