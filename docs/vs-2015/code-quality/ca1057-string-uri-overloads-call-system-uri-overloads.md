---
title: 'CA1057: 文字列 URI のオーバーロードは、System. Uri overloads | を呼び出します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1057
- StringUriOverloadsCallSystemUriOverloads
helpviewer_keywords:
- StringUriOverloadsCallSystemUriOverloads
- CA1057
ms.assetid: ef1e983e-9ca7-404b-82d7-65740ba0ce20
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bcdb4d8333b0a4d2d06580d882cf736d4527eca4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85539530"
---
# <a name="ca1057-string-uri-overloads-call-systemuri-overloads"></a>CA1057:文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 型は、パラメーターの文字列パラメーターの置換によってのみ異なるメソッドオーバーロードを宣言 <xref:System.Uri?displayProperty=fullName> します。文字列パラメーターを受け取るオーバーロードは、パラメーターを受け取るオーバーロードを呼び出しません <xref:System.Uri> 。

## <a name="rule-description"></a>ルールの説明
 オーバーロードは文字列/パラメーターのみが異なるため <xref:System.Uri> 、文字列は URI (uniform resource identifier) を表すと見なされます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 クラスは、 <xref:System.Uri> これらのサービスを安全かつ安全な方法で提供します。 クラスの利点を得るために、文字列の <xref:System.Uri> オーバーロードは <xref:System.Uri> 文字列引数を使用してオーバーロードを呼び出す必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 URI の文字列形式を使用するメソッドを再実装して、 <xref:System.Uri> 文字列引数を使用してクラスのインスタンスを作成し、そのオブジェクトをパラメーターを <xref:System.Uri> 持つオーバーロードに渡し <xref:System.Uri> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 文字列パラメーターが URI を表していない場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、正しく実装された文字列オーバーロードを示しています。

 [!code-cpp[FxCop.Design.CallUriOverload#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cpp/FxCop.Design.CallUriOverload.cpp#1)]
 [!code-csharp[FxCop.Design.CallUriOverload#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cs/FxCop.Design.CallUriOverload.cs#1)]
 [!code-vb[FxCop.Design.CallUriOverload#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/vb/FxCop.Design.CallUriOverload.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2234:文字列の代わりに System.Uri オブジェクトを渡します](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1056:URI プロパティを文字列にすることはできません](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054:URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055:URI 戻り値を文字列にすることはできません](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
