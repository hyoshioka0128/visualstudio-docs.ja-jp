---
title: 名前付けに関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis warnings, naming warnings
- naming warnings
- warnings, naming
ms.assetid: f97223ce-1d39-4134-81c9-fff2c75d979b
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03bc20d4bf39aa31865007e46e7ad3615f4b95bc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655965"
---
# <a name="naming-warnings"></a>名前付けに関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

名前付けの警告は、デザインガイドラインの名前付け規則への準拠をサポート [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] します。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1700:列挙型値に 'Reserved' という名前を指定しません](../code-quality/ca1700-do-not-name-enum-values-reserved.md)|この規則では、"reserved" を含む名前の列挙体のメンバーは、現在使用されていなくても、将来的なバージョンでは名前を変更するか削除されるプレースホルダーと想定しています。 メンバーの名前変更や削除は、互換性に影響する変更点です。|
|[CA1713:イベントは、before または after プレフィックスを含むことはできません](../code-quality/ca1713-events-should-not-have-before-or-after-prefix.md)|イベント名が "Before" または "After" で始まっています。 特定のシーケンスで発生する関連イベントに名前を付ける場合、現在時制または過去時制を使用して、アクション シーケンスの相対的な位置を示します。|
|[CA1714:フラグ列挙型は、複数形の名前を含んでいなければなりません](../code-quality/ca1714-flags-enums-should-have-plural-names.md)|パブリック列挙型には FlagsAttribute 属性があり、その名前は "s" で終了しません。 FlagsAttribute でマークされた型には複数形の名前が付いています。これは、属性が複数の値を指定できることを示すためです。|
|[CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)|外部から参照できる識別子の名前に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上含まれています。|
|[CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)|名前空間、型、メンバー、およびパラメーターの各識別子は、大文字/小文字以外のみでは区別できません。共通言語ランタイムを対象とする言語は、大文字と小文字を区別する必要はないためです。|
|[CA1715:識別子は正しいプレフィックスを含んでいなければなりません](../code-quality/ca1715-identifiers-should-have-correct-prefix.md)|外部から参照できるインターフェイスの名前が、大文字の "I" で始まっていません。  外部から参照できる型またはメソッドのジェネリック型パラメーターの名前が、大文字の "T" で始まっていません。|
|[CA1720:識別子には型名を含めないでください](../code-quality/ca1720-identifiers-should-not-contain-type-names.md)|外部から参照できるメンバーのパラメーター名にデータ型の名前が含まれているか、外部から参照できるメンバーの名前に言語固有のデータ型の名前が含まれています。|
|[CA1722:識別子は不適切なプレフィックスを含むことはできません](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)|規則では、特定のプログラミング要素にのみ、固有のプレフィックスで始まる名前を付けることができます。|
|[CA1711:識別子は、不適切なサフィックスを含むことはできません](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)|規則では、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはそのような型から派生した型の名前にのみ、固有の予約済みサフィックスを末尾に付けます。 その他の型名では、予約済みのサフィックスを使用しないでください。|
|[CA1717:FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません](../code-quality/ca1717-only-flagsattribute-enums-should-have-plural-names.md)|名前付け規則では、列挙体の複数形の名前は同時に複数の列挙値を指定できることを意味します。|
|[CA1725:パラメーター名は基本宣言と同一でなければなりません](../code-quality/ca1725-parameter-names-should-match-base-declaration.md)|オーバーライド階層のパラメーターに対する一貫性のある名前付けによって、メソッド オーバーライドの有用性が高まります。 派生メソッドのパラメーター名が基本宣言のパラメーター名と異なる場合、メソッドが基本メソッドのオーバーライドであるか、またはメソッドの新しいオーバーライドであるかについて混乱が生じる可能性があります。|
|[CA1719:パラメーター名はメンバー名と同一にすることはできません](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)|パラメーター名はパラメーターの意味を伝える必要があり、メンバー名はメンバーの意味を伝達する必要があります。 この 2 つの名前が一致するデザインは、まれにしか見られません。 パラメーターにメンバーと同じ名前を付けるとわかりづらくなり、ライブラリの操作が難しくなります。|
|[CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)|リソース文字列内の各単語は、大文字小文字に基づくトークンに分割されます。 Microsoft スペル チェック ライブラリは、隣接する 2 つのトークンの組み合わせを個別にチェックします。 それらが認識されると、その語はこの規則への違反となります。|
|[CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)|リソース文字列に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上含まれています。|
|[CA1724:型名は名前空間と同一にすることはできません](../code-quality/ca1724-type-names-should-not-match-namespaces.md)|型の名前は、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クラス ライブラリで定義されている名前空間の名前と一致しないようにする必要があります。 この規則に違反すると、ライブラリの操作性が低下する可能性があります。|
|[CA1707:識別子はアンダースコアを含むことはできません](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)|名前付け規則では、識別子名にアンダースコア (_) 文字を含めることができません。 この規則により、名前空間、型、メンバー、およびパラメーターがチェックされます。|
|[CA1721:プロパティ名は get メソッドと同一にすることはできません](../code-quality/ca1721-property-names-should-not-match-get-methods.md)|パブリック メンバーまたはプロテクト メンバーの名前が、"Get" から始まっているか、パブリック プロパティまたはプロテクト プロパティの名前と一致します。 "Get" メソッドとプロパティには、それぞれの機能を明確に区別する名前を指定しなければなりません。|
|[CA1716:識別子はキーワードと同一にすることはできません](../code-quality/ca1716-identifiers-should-not-match-keywords.md)|名前空間の名前または型の名前が、プログラミング言語で、予約済みのキーワードと一致します。 名前空間と型の識別子は、共通言語ランタイムを対象にする言語で定義されているキーワードと一致しないようにします。|
|[CA1726:適切な用語を使用します](../code-quality/ca1726-use-preferred-terms.md)|外部から参照可能な識別子の名前に含まれている用語に対応する、別の推奨される用語があります。 あるいは、名前に "Flag" または "Flags" という語が含まれています。|
|[CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)|慣例として、パラメーター名は camel 形式を使用し、名前空間、型、およびメンバー名は Pascal 形式を使用します。|
|[CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)|識別子の名前に複数の語が含まれており、大文字と小文字が正しく使い分けられていない複合語が 1 つ以上あります。|
|[CA1712:列挙型値を型名のプレフィックスにしません](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)|型情報は開発ツールによって提供されることが予想されるため、列挙型メンバーの名前の前には型名が付けられません。|
|[CA1710:識別子は、正しいサフィックスを含んでいなければなりません](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)|慣例として、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはこれらの型から派生した型の名前には、基本型またはインターフェイスに関連付けられたサフィックスがあります。|
