---
title: 'CA1704: 識別子は正しく入力されている必要があります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
helpviewer_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
ms.assetid: f2c7a44d-1690-44ca-9cd0-681b04b12b2a
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5e078fc1bb7fe247d541e7695e98c2de76c2466
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544067"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704:識別子は正しく入力されなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 識別子の名前に、Microsoft スペルチェックライブラリで認識されない1つ以上の単語が含まれています。 この規則では、コンストラクターや、get や set プロパティアクセサーなどの特別な名前のメンバーはチェックされません。

## <a name="rule-description"></a>ルールの説明
 このルールは、識別子をトークンに解析し、各トークンのスペルをチェックします。 解析アルゴリズムでは、次の変換が実行されます。

- 大文字は新しいトークンを開始します。 たとえば、MyNameIsJoe は、"My"、"Name"、"Is"、"Joe" になります。

- 大文字を複数使用する場合は、最後の大文字の文字によって新しいトークンが開始されます。 たとえば、"GUI"、"Editor" に GUIEditor ます。

- 先頭と末尾のアポストロフィは削除されます。 たとえば、"sender" は "sender" にトークンを送信します。

- アンダースコアはトークンの末尾を表し、削除されます。 たとえば、"Hello", "world" にトークンを Hello_world します。

- 埋め込みアンパサンドは削除されます。 たとえば、&台紙を "format" に設定します。

  既定では、スペルチェックの英語 (en) バージョンが使用されます。 他の言語辞書は現在使用できません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、単語のスペルを修正するか、CustomDictionary.xml という名前のカスタム辞書に単語を追加します。 ツールのインストールディレクトリ、プロジェクトディレクトリ、またはユーザーのプロファイルにあるツールに関連付けられているディレクトリ (%USERPROFILE%\Application Data \\ ...) に辞書を配置します。でカスタム辞書をプロジェクトに追加する方法につい [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ては、「[方法: コード分析辞書をカスタマイズ](../code-quality/how-to-customize-the-code-analysis-dictionary.md)する」を参照してください。

- 辞書/単語/認識されたパスで違反が発生しないようにする単語を追加します。

- 辞書/単語/認識されないパスで違反を引き起こす可能性のある単語を追加します。

- [辞書/単語/非推奨のパス] の下で、不使用としてフラグが設定されている単語を追加します。 詳細については、関連ルールのトピック「 [CA1726: Use terms](../code-quality/ca1726-use-preferred-terms.md)」を参照してください。

- 略語の大文字と小文字の規則に、辞書/頭字語/CasingExceptions パスに例外を追加します。

  カスタム辞書ファイルの構造の例を次に示します。

```
<Dictionary>
   <Words>
      <Unrecognized>
         <Word>cb</Word>
      </Unrecognized>
      <Recognized>
         <Word>stylesheet</Word>
         <Word>GotDotNet</Word>
      </Recognized>
      <Deprecated>
         <Term PreferredAlternate="EnterpriseServices">ComPlus</Term>
      </Deprecated>
   </Words>
   <Acronyms>
      <CasingExceptions>
         <Acronym>CJK</Acronym>
         <Acronym>Pi</Acronym>
      </CasingExceptions>
   </Acronyms>
</Dictionary>
```

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告が表示されないようにするには、単語のスペルが意図的に間違っていて、その単語がライブラリの限られたセットに適用されます。 正しい綴りの単語を使用すると、新しいソフトウェアライブラリに必要な学習曲線を減らすことができます。

## <a name="related-rules"></a>関連規則
 [CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

 [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

 [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707:識別子はアンダースコアを含むことはできません](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1726:適切な用語を使用します](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>関連項目
 [方法 : コード分析辞書をカスタマイズする](../code-quality/how-to-customize-the-code-analysis-dictionary.md)
