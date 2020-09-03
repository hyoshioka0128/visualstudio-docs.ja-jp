---
title: 匿名メソッドとコード分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- methods, anonymous
- code analysis, anonymous methods
- anonymous methods, code analysis
ms.assetid: bf0a1a9b-b954-4d46-9c0b-cee65330ad00
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 49da7d5e7f6a7731a708accb3d52fb6383ff1017
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72652221"
---
# <a name="anonymous-methods-and-code-analysis"></a>匿名メソッドとコード分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*匿名メソッド*は、名前のないメソッドです。 匿名メソッドは、コードブロックをデリゲートパラメーターとして渡すために最も頻繁に使用されます。

 このトピックでは、匿名メソッドに関連付けられている警告とメトリックをコード分析によって処理する方法について説明します。

## <a name="anonymous-methods-declared-in-a-member"></a>メンバーで宣言された匿名メソッド
 メソッドやアクセサーなど、メンバーで宣言されている匿名メソッドの警告とメトリックは、メソッドを宣言するメンバーに関連付けられています。 これらは、メソッドを呼び出すメンバーに関連付けられていません。

 たとえば、次のクラスでは、 **anonymousMethod**の宣言で見つかったすべての警告は、 **Method2**ではなく**Method1**に対して発生する必要があります。

```vb

      Delegate Function ADelegate(ByVal value As Integer) As Boolean
Class AClass

    Sub Method1()
        Dim anonymousMethod As ADelegate = Function(ByVal value As Integer) value > 5
        Method2(anonymousMethod)
    End SubSub Method2(ByVal anonymousMethod As ADelegate)
        anonymousMethod(10)
    End SubEnd Class
```

```csharp

      delegate void Delegate();
class Class
{
    void Method1()
    {
        Delegate anonymousMethod = delegate()
        {
          Console.WriteLine("");
        }
        Method2(anonymousMethod);
    }

    void Method2(Delegate anonymousMethod)
    {
        anonymousMethod();
    }
}
```

## <a name="inline-anonymous-methods"></a>インライン匿名メソッド
 フィールドへのインライン割り当てとして宣言されている匿名メソッドの警告とメトリックは、コンストラクターに関連付けられています。 フィールドが (では) として宣言されている場合、 `static` `Shared` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 警告とメトリックはクラスコンストラクターに関連付けられます。それ以外の場合は、インスタンスコンストラクターに関連付けられます。

 たとえば、次のクラスでは、 **anonymousMethod1** の宣言で検出されたすべての警告が、暗黙的に生成された **クラス**の既定のコンストラクターに対して発生します。 一方、 **anonymousMethod2** で見つかったものは、暗黙的に生成されたクラスコンストラクターに適用されます。

```vb

  Delegate Function ADelegate(ByVal value As Integer) As BooleanClass AClass
Dim anonymousMethod1 As ADelegate = Function(ByVal value As    Integer) value > 5
Shared anonymousMethod2 As ADelegate = Function(ByVal value As     Integer) value > 5

Sub Method1()
    anonymousMethod1(10)
    anonymousMethod2(10)
End SubEnd Class
```

```csharp

      delegate void Delegate();
class Class
{
    Delegate anonymousMethod1 = delegate()
    {
       Console.WriteLine("");
    }

    static Delegate anonymousMethod2 = delegate()
    {
       Console.WriteLine("");
    }

    void Method()
    {
       anonymousMethod1();
       anonymousMethod2();
    }
}
```

 クラスには、複数のコンストラクターを持つフィールドに値を割り当てるインライン匿名メソッドを含めることができます。 この場合、警告とメトリックは、コンストラクターが同じクラス内の別のコンストラクターにチェーンされていない限り、すべてのコンストラクターに関連付けられます。

 たとえば、次のクラスでは、 **anonymousMethod** の宣言で見つかったすべての警告をクラス ( **Int)** と **クラス (string)** に対して生成する必要がありますが、クラス **()** に対しては発生しません。

```vb

  Delegate Function ADelegate(ByVal value As Integer) As BooleanClass AClass

Dim anonymousMethod As ADelegate = Function(ByVal value As Integer)
value > 5

SubNew()
    New(CStr(Nothing))
End SubSub New(ByVal a As Integer)
End SubSub New(ByVal a As String)
End SubEnd Class
```

```csharp

      delegate void Delegate();
class Class
{
    Delegate anonymousMethod = delegate()
    {
       Console.WriteLine("");
    }

    Class() : this((string)null)
    {
    }

    Class(int a)
    {
    }

    Class(string a)
    {
    }
}
```

 これは予期しないように思えるかもしれませんが、これは、別のコンストラクターにチェーンされていないすべてのコンストラクターに対して、コンパイラが一意のメソッドを出力するためです。 この動作のため、 **anonymousMethod** で発生する違反は個別に抑制する必要があります。 これはまた、新しいコンストラクターが導入された場合に、 **クラス (int)** および **クラス (文字列)** に対して以前に抑制された警告を新しいコンストラクターに対しても抑制する必要があることを意味します。

 この問題は、次の2つの方法のいずれかで回避できます。 すべてのコンストラクターがチェーンする共通コンストラクターで **anonymousMethod** を宣言できます。 または、すべてのコンストラクターによって呼び出される初期化メソッドで宣言することもできます。

## <a name="see-also"></a>参照
 [マネージド コードの品質の分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)
