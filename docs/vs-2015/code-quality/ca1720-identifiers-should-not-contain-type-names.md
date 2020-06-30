---
title: 'CA1720: 識別子には型名 | を含めることはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1720
- IdentifiersShouldNotContainTypeNames
helpviewer_keywords:
- IdentifiersShouldNotContainTypeNames
- CA1720
ms.assetid: c95ee48f-f23a-45f0-ac9e-a3c1ecfabdea
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f6d228b0fbf5507ba135f9ddc35d6d8b161f0011
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534850"
---
# <a name="ca1720-identifiers-should-not-contain-type-names"></a>CA1720:識別子には型名を含めないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|IdentifiersShouldNotContainTypeNames|
|CheckId|CA1720|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できるメンバーのパラメーターの名前にデータ型の名前が含まれています。

 \- または -

 外部から参照できるメンバーの名前には、言語固有のデータ型名が含まれます。

## <a name="rule-description"></a>ルールの説明
 パラメーターとメンバーの名前は、開発ツールによって提供されると予想される型を記述するよりも、その意味を伝えるために使用する方が適切です。 メンバーの名前については、データ型名を使用する必要がある場合は、言語固有の名前ではなく、言語に依存しない名前を使用します。 たとえば、C# の型名 ' int ' ではなく、言語に依存しないデータ型名 Int32 を使用します。

 パラメーターまたはメンバーの名前に含まれる各個別トークンは、大文字と小文字を区別せずに、次の言語固有のデータ型名に対してチェックされます。

- Bool

- WChar

- Int8

- UInt8

- Short

- UShort

- Int

- UInt

- 整数型

- UInteger

- Long

- ULong

- 符号なし

- 符号付き

- Float

- Float32

- Float64

  さらに、パラメーターの名前は、大文字と小文字を区別せずに、次の言語に依存しないデータ型名に対してもチェックされます。

- Object

- Obj

- ブール型

- Char

- String

- SByte

- Byte

- UByte

- Int16

- UInt16

- Int32

- UInt32

- Int64

- UInt64

- IntPtr

- ポインター

- ポインター

- UInptr

- UPtr

- UPointer

- Single

- Double

- Decimal (10 進数型)

- GUID

## <a name="how-to-fix-violations"></a>違反の修正方法
 **パラメーターに対してが発生した場合:**

 パラメーターの名前に含まれるデータ型識別子を、その意味またはより汎用的な用語 (' value ' など) により適切に記述された用語で置き換えます。

 **メンバーに対して起動される場合:**

 メンバー名に含まれる言語固有のデータ型識別子を、その意味、言語に依存しないもの、または一般的な用語 (' value ' など) をより詳細に記述した用語で置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 型ベースのパラメーターとメンバー名をときどき使用することが適切な場合があります。 ただし、新しい開発では、この規則による警告を抑制する必要がある既知のシナリオはありません。 以前に出荷されたライブラリについては、このルールからの警告を抑制することが必要になる場合があります。

## <a name="related-rules"></a>関連規則
 [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707:識別子はアンダースコアを含むことはできません](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1719:パラメーター名はメンバー名と同一にすることはできません](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)
