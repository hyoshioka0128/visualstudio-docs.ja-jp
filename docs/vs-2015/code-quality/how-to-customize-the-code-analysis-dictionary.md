---
title: '方法: コード分析辞書をカスタマイズする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e3c8e8005a585e57f61ed873203305517d7b204a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658634"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>方法 : コード分析辞書をカスタマイズする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード分析では、組み込みの辞書を使用して、コード内の識別子を確認し、スペル、文法ケース、およびガイドラインのその他の名前付け規則を確認し [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。 カスタム辞書 Xml ファイルを作成して、組み込みの辞書に用語、略語、および頭字語を追加、削除、または変更することができます。

 たとえば、コードに **DoorKnokker**という名前のクラスが含まれているとします。 コード分析では、 **ドア** と **knokker**という2つの単語の複合として名前が識別されます。 その後、 **knokker** のスペルが正しくないという警告が生成されます。 コード分析でスペルを認識させるには、カスタム辞書に **knokker** という用語を追加します。

## <a name="to-create-a-custom-dictionary"></a>カスタム辞書を作成するには
 **CustomDictionary.xml**という名前のファイルを作成します。

 次の XML 構造を使用して、カスタム単語を定義します。

```
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>knokker</Word>
         </Unrecognized>
         <Recognized>
            <Word></Word>
         </Recognized>
         <Deprecated>
            <Term PreferredAlternate=""></Term>
         </Deprecated>
         <Compound>
            <Term CompoundAlternate=""></Term>
         </Compound>
         <DiscreteExceptions>
            <Term></Term>
         </DiscreteExceptions>
      </Words>
      <Acronyms>
         <CasingExceptions>
            <Acronym></Acronym>
         </CasingExceptions>
      </Acronyms>
   </Dictionary>
```

## <a name="custom-dictionary-elements"></a>カスタム辞書要素
 コード分析ディクショナリの動作を変更するには、カスタム辞書の次の要素の内部テキストとして用語を追加します。

- [辞書/単語/認識/単語](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)

- [辞書/単語/認識されない/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)

- [Dictionary/Words/Deprecated/Term [ @PreferredAlternate ]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)

- [辞書/単語/複合/語句 [ @CompoundAlternate ]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)

- [Dictionary/Words/DiscreteExceptions/Term](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)

- [Dictionary/頭字語/CasingExceptions/頭字語](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)

### <a name="dictionarywordsrecognizedword"></a><a name="BKMK_DictionaryWordsRecognizedWord"></a> 辞書/単語/認識/単語
 コード分析によって正しくスペルが識別される用語の一覧に用語を含めるには、用語を辞書/単語/認識/単語要素の内部テキストとして追加します。 辞書/単語/認識された要素または Word 要素の用語では、大文字と小文字は区別されません。

 **例**

```
<Dictionary>
      <Words>
         <Recognized>
            <Word>knokker</Word>
            ...
         </Recognized>
         ...
      </Words>
      ...
</Dictionary>

```

 ディクショナリ/単語/認識されたノードの用語は、次のコード分析規則に適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

- [CA1726:適切な用語を使用します](../code-quality/ca1726-use-preferred-terms.md)

- [CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

### <a name="dictionarywordsunrecognizedword"></a><a name="BKMK_DictionaryWordsUnrecognizedWord"></a> 辞書/単語/認識されない/Word
 コード分析によって正しくスペルが識別される用語の一覧から用語を除外するには、辞書/単語/認識されていない要素の内部テキストとして除外する用語を追加します。 辞書/単語/認識されない/Word 要素の用語では、大文字と小文字は区別されません。

 **例**

```
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>meth</Word>
            ...
         </Unrecognized>
         ...
      </Words>
      ...
</Dictionary>

```

 辞書/単語/認識されていないノードの用語は、次のコード分析規則に適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

- [CA1726:適切な用語を使用します](../code-quality/ca1726-use-preferred-terms.md)

- [CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

### <a name="dictionarywordsdeprecatedtermpreferredalternate"></a><a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> Dictionary/Words/Deprecated/Term [ @PreferredAlternate ]
 コード分析によって非推奨と識別された用語の一覧に用語を含めるには、用語を辞書/単語/非推奨の要素の内部テキストとして追加します。 非推奨の用語は、スペルが正しく、使用すべきではない単語です。

 警告に提案された代替用語を含めるには、Term 要素の PreferredAlternate 属性で代替用語を指定します。 代替を提案しない場合は、属性値を空のままにしておくことができます。

- Dictionary/Words/Deprecated/Term 要素の非推奨の用語では、大文字と小文字は区別されません。

- PreferredAlternate 属性値では大文字と小文字が区別されます。 複合代替の場合は、Pascal 形式を使用します。

  **例**

```
<Dictionary>
      <Words>
         <Deprecated>
            <Term PreferredAlternate="LogOn">login</Term>
            ...
         </Deprecated>
         ...
      </Words>
      ...
</Dictionary>

```

 [辞書/単語/非推奨] ノードの用語は、次のコード分析規則に適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1726:適切な用語を使用します](../code-quality/ca1726-use-preferred-terms.md)

### <a name="dictionarywordscompoundtermcompoundalternate"></a><a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> 辞書/単語/複合/語句 [ @CompoundAlternate ]
 組み込みの辞書は、複合語句ではなく、単一の個別の用語として用語を識別します。 コード分析で特定の単語として識別される用語の一覧に用語を含めるには、用語を辞書/単語/複合/用語要素の内部テキストとして追加します。 Term 要素の CompoundAlternate 属性で、個別の単語の最初の文字を大文字にして (Pascal 形式)、複合語句を構成する個々の単語を指定します。 内部テキストで指定された用語は、辞書/単語/DiscreteExceptions リストに自動的に追加されることに注意してください。

- Dictionary/Words/Deprecated/Term 要素の非推奨の用語では、大文字と小文字は区別されません。

- PreferredAlternate 属性値では大文字と小文字が区別されます。 複合代替の場合は、Pascal 形式を使用します。

  **例**

```
<Dictionary>
      <Words>
         <Compound>
            <Term CompoundAlternate="CheckBox">checkbox</Term>
            ...
         </Compound>
         ...
      </Words>
      ...
</Dictionary>

```

 [ディクショナリ/単語/複合] ノードの用語は、次のコード分析規則に適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

### <a name="dictionarywordsdiscreteexceptionsterm"></a><a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> Dictionary/Words/DiscreteExceptions/Term
 コード分析で、複合語の大文字と小文字の規則によって語句がチェックされるときに、単語として識別される用語を一覧から除外するには、辞書/単語/DiscreteExceptions/Term 要素の内部テキストとして用語を追加します。 Dictionary/Words/DiscreteExceptions/Term 要素の用語では、大文字と小文字は区別されません。

 **例**

```
<Dictionary>
      <Words>
         <DiscreteExceptions>
            <Term>checkbox</Term>
            ...
         </DiscreteExceptions>
         ...
      </Words>
      ...
</Dictionary>

```

 [ディクショナリ/単語/DiscreteExceptions] ノードの用語は、次のコード分析規則に適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

### <a name="dictionaryacronymscasingexceptionsacronym"></a><a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> Dictionary/頭字語/CasingExceptions/頭字語
 コード分析によって識別される用語の一覧に頭字語を含め、複合語の大文字と小文字の規則によって用語がチェックされる方法を指定するには、辞書/頭字語/CasingExceptions/頭字語要素の内部テキストとして用語を追加します。 Dictionary/頭字/CasingExceptions/頭字語の頭字語では、大文字と小文字が区別されます。

 **例**

```
<Dictionary>
      <Acronyms>
         <CasingExceptions>
            <Acronym>NESW</Acronym>   <!-- North East South West -->
            ...
         </CasingExceptions>
         ...
      </Acronyms>
      ...
</Dictionary>

```

 [辞書/頭字語/CasingExceptions] ノードの用語は、次のコード分析規則に適用されます。

- [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

## <a name="to-apply-a-custom-dictionary-to-a-project"></a><a name="BKMK_ToApplyACustomDictionaryToAProject"></a> プロジェクトにカスタム辞書を適用するには

1. **ソリューションエクスプローラー**で、次のいずれかの手順を実行します。

2. 1つのプロジェクトに辞書を追加するには、プロジェクト名を右クリックし、[ **既存項目の追加**] をクリックします。 [ **既存項目の追加** ] ダイアログボックスでファイルを指定します。

3. 複数のプロジェクト間で共有される辞書を追加するには、[ **既存項目の追加** ] ダイアログボックスで共有するファイルを探し、[ **追加** ] ボタンの下矢印をクリックして、[ **リンクとして追加**] をクリックします。

4. **ソリューションエクスプローラー**で、 **CustomDictionary.xml**ファイル名を右クリックし、[**プロパティ**] をクリックします。

5. [ **ビルドアクション** ] ボックスの一覧で、[ **CodeAnalysisDictionary**] を選択します。

6. [ **出力ディレクトリにコピー** ] ボックスの一覧の [ **コピー**しない] を選択します。
