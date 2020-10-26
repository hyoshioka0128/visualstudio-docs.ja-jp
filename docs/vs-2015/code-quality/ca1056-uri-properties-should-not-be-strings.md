---
title: 'CA1056: URI プロパティを文字列にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UriPropertiesShouldNotBeStrings
- CA1056
helpviewer_keywords:
- UriPropertiesShouldNotBeStrings
- CA1056
ms.assetid: fdc99d29-0904-4a65-baa8-4f76833c953e
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 87ed8f7a291c95e500196f511c6fec0f38cef68e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85539413"
---
# <a name="ca1056-uri-properties-should-not-be-strings"></a>CA1056:URI プロパティを文字列にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|UriPropertiesShouldNotBeStrings|
|CheckId|CA1056|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型は、名前に "uri"、"Uri"、"urn"、"Urn"、"url"、"Url" を含む文字列プロパティを宣言します。

## <a name="rule-description"></a>ルールの説明
 このルールは、Pascal 形式の表記規則に基づいてプロパティ名をトークンに分割し、各トークンが "uri"、"Uri"、"urn"、"Urn"、"url"、または "Url" に等しいかどうかを確認します。 一致するものがある場合は、プロパティが URI (uniform resource identifier) を表すことを前提としています。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 クラスは、 <xref:System.Uri?displayProperty=fullName> これらのサービスを安全かつ安全な方法で提供します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、プロパティを型に変更し <xref:System.Uri> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 プロパティが URI を表していない場合は、この規則による警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、 `ErrorProne` この規則に違反する型と、規則を満たす型を示して `SaferWay` います。

 [!code-cpp[FxCop.Design.UriNotString#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cpp/FxCop.Design.UriNotString.cpp#1)]
 [!code-csharp[FxCop.Design.UriNotString#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cs/FxCop.Design.UriNotString.cs#1)]
 [!code-vb[FxCop.Design.UriNotString#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/vb/FxCop.Design.UriNotString.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1054:URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055:URI 戻り値を文字列にすることはできません](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)

 [CA2234:文字列の代わりに System.Uri オブジェクトを渡します](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1057:文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)
