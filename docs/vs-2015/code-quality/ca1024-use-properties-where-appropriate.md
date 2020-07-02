---
title: 'CA1024: 適切な場所にプロパティを使用します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UsePropertiesWhereAppropriate
- CA1024
helpviewer_keywords:
- CA1024
- UsePropertiesWhereAppropriate
ms.assetid: 3a04f765-af7c-4872-87ad-9cc29e8e657f
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a240a6eea86075bbf7f721f8620b6d135d594c20
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546667"
---
# <a name="ca1024-use-properties-where-appropriate"></a>CA1024:適切な場所にプロパティを使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|UsePropertiesWhereAppropriate|
|CheckId|CA1024|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックメソッドまたはプロテクトメソッドには、で始まる名前があり `Get` 、パラメーターは使用せず、配列ではない値を返します。

## <a name="rule-description"></a>ルールの説明
 ほとんどの場合、プロパティはデータを表し、メソッドはアクションを実行します。 プロパティはフィールドのようにアクセスされるため、簡単に使用できます。 次の条件のいずれかが存在する場合、メソッドは、プロパティになることをお勧めします。

- 引数を取らず、オブジェクトの状態情報を返します。

- 1つの引数を受け取り、オブジェクトの状態の一部を設定します。

  プロパティは、フィールドであるかのように動作します。メソッドがを使用できない場合は、プロパティに変更しないでください。 メソッドは、次のような場合にプロパティよりも優れています。

- メソッドは、時間のかかる操作を実行します。 メソッドの perceivably は、フィールドの値を設定または取得するために必要な時間よりも遅くなります。

- メソッドは、変換を実行します。 フィールドにアクセスしても、格納されているデータの変換バージョンは返されません。

- Get メソッドには、観測可能な副作用があります。 フィールドの値を取得しても、副作用は生成されません。

- 実行の順序は重要です。 フィールドの値を設定しても、他の操作の発生には依存しません。

- メソッドを連続して2回呼び出すと、異なる結果が生成されます。

- メソッドは静的ですが、呼び出し元が変更できるオブジェクトを返します。 フィールドの値を取得しても、フィールドに格納されているデータを呼び出し元が変更することはできません。

- メソッドは配列を返します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドをプロパティに変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 メソッドが前述の条件のうち少なくとも1つを満たしている場合、この規則からの警告を非表示にします。

## <a name="controlling-property-expansion-in-the-debugger"></a>デバッガーでのプロパティ拡張の制御
 プログラマがプロパティを使用しない理由の1つは、プログラマがデバッガーを自動展開しないようにするためです。 たとえば、プロパティに大きなオブジェクトの割り当てや P/Invoke の呼び出しが含まれる場合がありますが、実際には観測可能な副作用がない可能性があります。

 を適用して、デバッガーが自動拡張プロパティを使用しないようにすることができ <xref:System.Diagnostics.DebuggerBrowsableAttribute?displayProperty=fullName> ます。 次の例は、この属性がインスタンスプロパティに適用されていることを示しています。

```vb
Imports System
Imports System.Diagnostics

Namespace Microsoft.Samples

    Public Class TestClass

        ' [...]

        <DebuggerBrowsable(DebuggerBrowsableState.Never)> _
        Public ReadOnly Property LargeObject() As LargeObject
            Get
                ' Allocate large object
                ' [...]
            End Get
        End Property

    End Class

End Namespace
```

```csharp

      using System;
using System.Diagnostics;

namespace Microsoft.Samples
{
    publicclass TestClass
    {
        // [...]

        [DebuggerBrowsable(DebuggerBrowsableState.Never)]
        public LargeObject LargeObject
        {
            get
            {
                // Allocate large object
                // [...]

        }
    }
}
```

## <a name="example"></a>例
 次の例には、プロパティに変換する必要があるいくつかのメソッドが含まれています。これらのメソッドは、フィールドのように動作しないためです。

 [!code-csharp[FxCop.Design.MethodsProperties#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.MethodsProperties/cs/FxCop.Design.MethodsProperties.cs#1)]
