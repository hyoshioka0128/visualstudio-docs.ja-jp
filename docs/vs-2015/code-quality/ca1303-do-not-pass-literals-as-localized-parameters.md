---
title: 'CA1303: ローカライズされたパラメーターとしてリテラルを渡さないでください |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Do not pass literals as localized parameters
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
helpviewer_keywords:
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
ms.assetid: 904d284e-76d0-4b8f-a4df-0094de8d7aac
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f3ad1f56215d002c03d346b38ce6155e8df7412b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539114"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303:ローカライズされるパラメーターとしてリテラルを渡さない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 メソッドは、パラメーターとして文字列リテラルをクラスライブラリ内のコンストラクターまたはメソッドに渡し [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 、その文字列はローカライズ可能である必要があります。

 この警告は、リテラル文字列が値としてパラメーターまたはプロパティに渡され、次の1つ以上のケースが true の場合に発生します。

- <xref:System.ComponentModel.LocalizableAttribute>パラメーターまたはプロパティの属性が true に設定されています。

- パラメーターまたはプロパティ名には、"Text"、"Message"、または "Caption" が含まれています。

- Console に渡される文字列パラメーターの名前です。 Write または Console. WriteLine メソッドは、"value" または "format" のいずれかです。

## <a name="rule-description"></a>ルールの説明
 ソースコードに埋め込まれている文字列リテラルをローカライズするのは困難です。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、文字列リテラルをクラスのインスタンスを通じて取得される文字列に置き換え <xref:System.Resources.ResourceManager> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 コードライブラリがローカライズされていない場合、またはコードライブラリを使用して、エンドユーザーまたは開発者に対して文字列が公開されていない場合は、この規則による警告を抑制することが安全です。

 ユーザーは、という名前のパラメーターまたはプロパティの名前を変更するか、これらの項目を条件付きとしてマークすることによって、ローカライズされた文字列を渡さないメソッドに対するノイズを排除できます。

## <a name="example"></a>例
 次の例は、2つの引数のいずれかが範囲外にある場合に例外をスローするメソッドを示しています。 最初の引数では、この規則に違反するリテラル文字列が例外コンストラクターに渡されます。 2番目の引数のコンストラクターには、から取得した文字列が正しく渡され <xref:System.Resources.ResourceManager> ます。

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cpp/FxCop.Globalization.DoNotPassLiterals.cpp#1)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cs/FxCop.Globalization.DoNotPassLiterals.cs#1)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/vb/FxCop.Globalization.DoNotPassLiterals.vb#1)]

## <a name="see-also"></a>関連項目
 [デスクトップ アプリケーションのリソース](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
