---
title: 'CA2204: リテラルは正しく入力されている必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Literals should be spelled correctly
- CA2204
- LiteralsShouldBeSpelledCorrectly
helpviewer_keywords:
- CA2204
ms.assetid: b0bbcbb6-c92d-4c14-8ef7-9c8b38c791a6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ecf829251cbeab600cb95f8f0c0b0173cd7338d4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546277"
---
# <a name="ca2204-literals-should-be-spelled-correctly"></a>CA2204:リテラルに正しいスペルを要求
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|LiteralsShouldBeSpelledCorrectly|
|CheckId|CA2204|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 メソッドは、ローカライズされた文字列を必要とするパラメーターまたはプロパティで使用されるリテラル文字列をに渡します。リテラル文字列には、Microsoft スペルチェックライブラリで認識されない1つ以上の単語が含まれています。

## <a name="rule-description"></a>ルールの説明
 このルールでは、次のケースの1つ以上が当てはまる場合に、パラメーターまたはプロパティに値として渡されるリテラル文字列をチェックします。

- <xref:System.ComponentModel.LocalizableAttribute>パラメーターまたはプロパティの属性が true に設定されています。

- パラメーターまたはプロパティ名には、"Text"、"Message"、または "Caption" が含まれています。

- Console に渡される文字列パラメーターの名前です。 Write または Console. WriteLine メソッドは、"value" または "format" のいずれかです。

  このルールは、リテラル文字列を単語に解析し、複合語をトークン化して、各単語/トークンのスペルをチェックします。 解析アルゴリズムの詳細については、「 [CA1704: 識別子は正しく入力されている必要があり](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)ます。

  既定では、スペルチェックの英語 (en) バージョンが使用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、単語のスペルを修正するか、またはカスタム辞書に単語を追加します。 カスタム辞書の使用方法の詳細については、「[方法: コード分析辞書をカスタマイズ](../code-quality/how-to-customize-the-code-analysis-dictionary.md)する」を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 正しい綴りの単語を使用すると、新しいソフトウェアライブラリに必要な学習曲線を減らすことができます。

## <a name="related-rules"></a>関連規則
 [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

 [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
