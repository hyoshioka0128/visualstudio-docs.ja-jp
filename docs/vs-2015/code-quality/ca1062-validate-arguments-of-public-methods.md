---
title: 'CA1062: パブリックメソッドの引数を検証する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
- Validate arguments of public methods
helpviewer_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
ms.assetid: db1f69ca-68f7-477e-94f3-d135cc5dfcbc
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 377906675d70a712f8ca72b0b6e4d8a6864c1fbc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533238"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062:パブリック メソッドの引数の検証
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 外部から参照できるメソッドは、その引数が (Visual Basic) であるかどうかを確認せずに、参照引数の1つを逆参照 `null` `Nothing` します。

## <a name="rule-description"></a>ルールの説明
 外部から参照できるメソッドに渡されるすべての参照引数を照合する必要があり `null` ます。 必要に応じて、引数がの場合にをスローし <xref:System.ArgumentNullException> `null` ます。

 パブリックまたは protected として宣言されているために不明なアセンブリからメソッドを呼び出すことができる場合は、メソッドのすべてのパラメーターを検証する必要があります。 メソッドが既知のアセンブリによってのみ呼び出されるように設計されている場合は、メソッドを内部にし、 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> メソッドを含むアセンブリに属性を適用する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、各参照引数をに対して検証し `null` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 逆参照パラメーターが関数内の別のメソッド呼び出しによって検証されていることが確実である場合は、この規則からの警告を非表示にすることができます。

## <a name="example"></a>例
 次の例は、規則に違反するメソッドと、規則を満たすメソッドを示しています。

 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#1)]
 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#1)]
 [!code-vb[FxCop.Design.ValidateArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#1)]

## <a name="example"></a>例
 では [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] 、検証を行う別のメソッドにパラメーターが渡されているかどうかは、この規則によって検出されません。

 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#2)]
 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#2)]
 [!code-vb[FxCop.Design.ValidateArguments#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#2)]

## <a name="example"></a>例
 フィールドまたは参照オブジェクトであるプロパティを設定するコピーコンストラクターも、CA1062 の規則に違反する可能性があります。 コピーコンストラクターに渡されるコピーされたオブジェクトが `null` (Visual Basic) である可能性があるため、違反が発生し `Nothing` ます。 違反を解決するには、静的 (Visual Basic では Shared) メソッドを使用して、コピーされたオブジェクトが null でないことを確認します。

 次のクラスの例では、 `Person` `other` コピーコンストラクターに渡されるオブジェクトが `Person` である可能性があり `null` ます。

```

public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor CA1062 fires because other is dereferenced
    // without being checked for null
    public Person(Person other)
        : this(other.Name, other.Age)
    {
    }
}
```

## <a name="example"></a>例
 次の例では `Person` 、 `other` コピーコンストラクターに渡されたオブジェクトが、最初にメソッドで null であるかどうかがチェックされ `PassThroughNonNull` ます。

```
public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor
    public Person(Person other)
        : this(PassThroughNonNull(other).Name,
          PassThroughNonNull(other).Age)
    {
    }

    // Null check method
    private static Person PassThroughNonNull(Person person)
    {
        if (person == null)
            throw new ArgumentNullException("person");
        return person;
    }
}
```
