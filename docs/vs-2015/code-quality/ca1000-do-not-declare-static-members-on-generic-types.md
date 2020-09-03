---
title: 'CA1000: ジェネリック型の静的メンバーを宣言しません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1000
- DoNotDeclareStaticMembersOnGenericTypes
helpviewer_keywords:
- DoNotDeclareStaticMembersOnGenericTypes
- CA1000
ms.assetid: 5c0da594-f8d0-4f40-953d-56bf7fbd2087
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 66bca5b8b039de59509cecf4ecfae6bd6b4f0162
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548331"
---
# <a name="ca1000-do-not-declare-static-members-on-generic-types"></a>CA1000:ジェネリック型の静的メンバーを宣言しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotDeclareStaticMembersOnGenericTypes|
|CheckId|CA1000|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できるジェネリック型には、 `static` (Visual Basic) メンバーが含まれてい `Shared` ます。

## <a name="rule-description"></a>ルールの説明
 `static`ジェネリック型のメンバーを呼び出す場合は、型に対して型引数を指定する必要があります。 推論をサポートしないジェネリック インスタンス メンバーを呼び出すときには、そのメンバーに型引数を指定する必要があります。 この2つのケースで型引数を指定する構文は、次の呼び出しで示すように、異なっていて簡単に混同できます。

```vb
' Shared method in a generic type.
GenericType(Of Integer).SharedMethod()

' Generic instance method that does not support inference.
someObject.GenericMethod(Of Integer)()
```

```csharp
// Static method in a generic type.
GenericType<int>.StaticMethod();

// Generic instance method that does not support inference.
someObject.GenericMethod<int>();
```

 一般に、メンバーを呼び出すときに型引数を指定する必要がないように、前の宣言は両方とも回避する必要があります。 これにより、非ジェネリックの構文とは異なるジェネリックのメンバーを呼び出すための構文が生成されます。 詳細については、「 [CA1004: ジェネリックメソッドは型パラメーターを提供する必要があり](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)ます」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、静的メンバーを削除するか、またはインスタンスメンバーに変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 簡単に理解して使用できる構文でジェネリックを提供することで、新しいライブラリの導入率を習得し、向上させるために必要な時間を短縮できます。

## <a name="related-rules"></a>関連規則
 [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1002:ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:ジェネリック メソッドは型パラメーターを指定しなければなりません](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:汎用イベント ハンドラーのインスタンスを使用します](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007:適切な場所にジェネリックを使用します](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>参照
 [ジェネリック](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
