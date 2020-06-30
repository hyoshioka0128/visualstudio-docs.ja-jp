---
title: 'CA2234: string | の代わりに system.string オブジェクトを渡します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PassSystemUriObjectsInsteadOfStrings
- CA2234
helpviewer_keywords:
- CA2234
- PassSystemUriObjectsInsteadOfStrings
ms.assetid: 14616b37-74c4-4286-b051-115d00aceb5f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ce5c076260886def089118a4d7211d75e0185c0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545211"
---
# <a name="ca2234-pass-systemuri-objects-instead-of-strings"></a>CA2234:文字列の代わりに System.Uri オブジェクトを渡します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|PassSystemUriObjectsInsteadOfStrings|
|CheckId|CA2234|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 名前に "uri"、"Uri"、"urn"、"Urn"、"url"、"Url" を含む文字列パラメーターを持つメソッドが呼び出されました。また、メソッドの宣言する型には、パラメーターを持つ対応するメソッドオーバーロードが含まれてい <xref:System.Uri?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 パラメーター名は camel 形式の表記規則に基づいてトークンに分割され、各トークンは、"uri"、"Uri"、"urn"、"Urn"、"url"、"Url" に等しいかどうかを確認します。 一致するものがある場合、パラメーターは URI (uniform resource identifier) を表していると見なされます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 クラスは、 <xref:System.Uri> これらのサービスを安全かつ安全な方法で提供します。 URI の表現に関してのみ異なる2つのオーバーロードのいずれかを選択する場合、ユーザーは引数を受け取るオーバーロードを選択する必要があり <xref:System.Uri> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、引数を受け取るオーバーロードを呼び出し <xref:System.Uri> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 文字列パラメーターが URI を表していない場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、 `ErrorProne` 規則に違反するメソッドと、オーバーロードを正しく呼び出すメソッドを示して `SaferWay` <xref:System.Uri> います。

 [!code-cpp[FxCop.Usage.PassUri#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/cpp/FxCop.Usage.PassUri.cpp#1)]
 [!code-csharp[FxCop.Usage.PassUri#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/cs/FxCop.Usage.PassUri.cs#1)]
 [!code-vb[FxCop.Usage.PassUri#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/vb/FxCop.Usage.PassUri.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1057:文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)

 [CA1056:URI プロパティを文字列にすることはできません](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054:URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055:URI 戻り値を文字列にすることはできません](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
