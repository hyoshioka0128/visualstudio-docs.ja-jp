---
title: 'CA1307: StringComparison | を指定します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1307
- SpecifyStringComparison
helpviewer_keywords:
- CA1307
- SpecifyStringComparison
ms.assetid: 9b0d5e71-1683-4a0d-bc4a-68b2fbd8af71
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 033d8f0e22ec040ffb10821993a5a9c647ee401e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538919"
---
# <a name="ca1307-specify-stringcomparison"></a>CA1307:StringComparison の指定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|SpecifyStringComparison|
|CheckId|CA1307|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 文字列比較操作では、パラメーターを設定しないメソッドオーバーロードが使用されてい <xref:System.StringComparison> ます。

## <a name="rule-description"></a>ルールの説明
 多くの文字列操作 (最も重要 <xref:System.String.Compare%2A> な <xref:System.String.Equals%2A> メソッドとメソッド) は、 <xref:System.StringComparison> 列挙値をパラメーターとして受け取るオーバーロードを提供します。

 パラメーターを受け取るオーバーロードが存在する場合は常に <xref:System.StringComparison> 、このパラメーターを受け取らないオーバーロードの代わりに使用する必要があります。 このパラメーターを明示的に設定することにより、コードを明確にし、保守を容易にすることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.StringComparison> 列挙体をパラメーターとして受け入れるオーバーロードに文字列比較メソッドを変更します。 例: `String.Compare(str1, str2)` をに変更 `String.Compare(str1, str2, StringComparison.Ordinal)` します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 ライブラリまたはアプリケーションが限定されたローカルユーザーを対象としていて、ローカライズされない場合は、この規則による警告を抑制することが安全です。

## <a name="see-also"></a>参照
 [グローバリゼーションの警告](../code-quality/globalization-warnings.md) [CA1309: 序数の Stringcomparison を使用する](../code-quality/ca1309-use-ordinal-stringcomparison.md)
