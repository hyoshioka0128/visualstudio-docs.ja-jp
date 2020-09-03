---
title: 'CA1309: 序数の StringComparison | を使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseOrdinalStringComparison
- CA1309
helpviewer_keywords:
- UseOrdinalStringComparison
- CA1309
ms.assetid: 19be0854-cb6e-4efd-a4c8-a5c1fc6f7a71
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: be60d2a1dcb769a0b7a8574984de3d288bf57af4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538880"
---
# <a name="ca1309-use-ordinal-stringcomparison"></a>CA1309:順序を示す StringComparison を使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|UseOrdinalStringComparison|
|CheckId|CA1309|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 非言語的な文字列比較操作では、パラメーターは <xref:System.StringComparison> **序数** または **stringcomparison.ordinalignorecase**に設定されません。

## <a name="rule-description"></a>ルールの説明
 多くの文字列操作 (最も重要 <xref:System.String.Compare%2A?displayProperty=fullName> な <xref:System.String.Equals%2A?displayProperty=fullName> メソッドとメソッド) は、 <xref:System.StringComparison?displayProperty=fullName> 列挙値をパラメーターとして受け取るオーバーロードを提供するようになりました。

 Stringcomparison.ordinalignorecase または**stringcomparison.** を指定すると、文字列の比較は非言語に**なります。** つまり、比較の決定が行われると、自然言語に固有の機能は無視されます。 つまり、決定は単純なバイト比較に基づいており、カルチャによってパラメーター化された大文字と小文字の区別や等価性のテーブルを無視します。 結果として、パラメーターを **Stringcomparison. Ordinal** または **stringcomparison.ordinalignorecase**のいずれかに明示的に設定すると、コードの速度が向上し、正確性が向上し、信頼性も高くなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、文字列比較メソッドを <xref:System.StringComparison?displayProperty=fullName> パラメーターとして列挙型を受け入れるオーバーロードに変更し、 **Ordinal** または **stringcomparison.ordinalignorecase**を指定します。 たとえば、`String.Compare(str1, str2)` を `String.Compare(str1, str2, StringComparison.Ordinal)` に変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 ライブラリまたはアプリケーションが限定されたローカルユーザーを対象としている場合、または現在のカルチャのセマンティクスを使用する必要がある場合は、この規則からの警告を抑制することが安全です。

## <a name="see-also"></a>参照
 [グローバリゼーションの警告](../code-quality/globalization-warnings.md) [CA1307: Stringcomparison の指定](../code-quality/ca1307-specify-stringcomparison.md)
