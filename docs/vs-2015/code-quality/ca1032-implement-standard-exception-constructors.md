---
title: 'CA1032: 標準の例外コンストラクターを実装します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1032
- ImplementStandardExceptionConstructors
helpviewer_keywords:
- CA1032
- ImplementStandardExceptionConstructors
ms.assetid: a8623c56-273a-4c95-8d83-95911a042be7
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 61b0157200ddff4cb8335118b30832a0c8950f65
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542286"
---
# <a name="ca1032-implement-standard-exception-constructors"></a>CA1032:標準例外コンストラクターを実装します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ImplementStandardExceptionConstructors|
|CheckId|CA1032|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 型はを拡張 <xref:System.Exception?displayProperty=fullName> し、必要なすべてのコンストラクターを宣言しません。

## <a name="rule-description"></a>ルールの説明
 例外の種類には、次のコンストラクターを実装する必要があります。

- public NewException ()

- public NewException (文字列)

- public NewException (文字列、例外)

- protected または private NewException (SerializationInfo、StreamingContext)

  コンストラクターを完全に宣言していないと、例外を正しく処理するのが困難になります。 たとえば、シグネチャを持つコンストラクターは、 `NewException(string, Exception)` 他の例外によって発生する例外を作成するために使用されます。 このコンストラクターがない場合、内部 (入れ子になった) 例外を含むカスタム例外のインスタンスを作成してスローすることはできません。このような状況では、マネージコードで実行する必要があります。 最初の3つの例外コンストラクターは規約によって公開されています。 4番目のコンストラクターは、封印されていないクラスで保護され、シールクラスでプライベートになります。 詳細については、「 [CA2229: 実装シリアル化コンストラクター](../code-quality/ca2229-implement-serialization-constructors.md) 」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、不足しているコンストラクターを例外に追加し、適切なアクセシビリティが設定されていることを確認します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パブリックコンストラクターに別のアクセスレベルを使用することによって違反が発生した場合に、この規則からの警告を抑制するのは安全です。

## <a name="example"></a>例
 次の例には、この規則に違反する例外の種類と、正しく実装されている例外の種類が含まれています。

 [!code-csharp[FxCop.Design.ExceptionMultipleCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionMultipleCtors/cs/FxCop.Design.ExceptionMultipleCtors.cs#1)]
