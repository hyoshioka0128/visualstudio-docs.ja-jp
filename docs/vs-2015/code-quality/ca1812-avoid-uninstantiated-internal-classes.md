---
title: 'CA1812: インスタンス内部クラスを回避します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1812
- AvoidUninstantiatedInternalClasses
helpviewer_keywords:
- AvoidUninstantiatedInternalClasses
- CA1812
ms.assetid: 1bb92a42-322a-44cc-98a8-8858212c1e1f
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 401fbfbccfeeeeec5cbdc0e791b110d1b5f0201b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543976"
---
# <a name="ca1812-avoid-uninstantiated-internal-classes"></a>CA1812:インスタンス化されていない内部クラスを使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidUninstantiatedInternalClasses|
|CheckId|CA1812|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 アセンブリ レベルの型のインスタンスが、アセンブリ内のコードから作成されません。

## <a name="rule-description"></a>ルールの説明
 このルールは、型のいずれかのコンストラクターへの呼び出しを検索し、呼び出しが見つからない場合は違反を報告します。

 この規則では、次の型は検証されません。

- 値型

- 抽象型

- 列挙

- 代理人

- コンパイラによって生成された配列型

- インスタンス化できず、 `static` ( `Shared` Visual Basic) メソッドのみを定義する型。

  <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute?displayProperty=fullName>分析されるアセンブリにを適用すると、 `internal` フィールドが別のアセンブリによって使用されているかどうかを判断できないため、この規則はとしてマークされているコンストラクターでは発生しません `friend` 。

  コード分析でこの制限を回避することはできません [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が、すべての `friend` アセンブリが分析に存在する場合は、外部のスタンドアロン FxCop が内部コンストラクターで発生します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、型を削除するか、この規則を使用するコードを追加します。 型に静的メソッドのみが含まれている場合は、次のいずれかを型に追加して、コンパイラが既定のパブリックインスタンスコンストラクターを生成しないようにします。

- バージョン1.0 および1.1 を対象とする型のプライベートコンストラクター [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

- を `static` `Shared` 対象とする型の (Visual Basic) 修飾子 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。 次の状況では、この警告を非表示にすることをお勧めします。

- クラスは、などの遅延バインディングされたリフレクションメソッドを使用して作成され <xref:System.Activator.CreateInstance%2A?displayProperty=fullName> ます。

- クラスは、ランタイムまたはによって自動的に作成され [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ます。 たとえば、またはを実装するクラス <xref:System.Configuration.IConfigurationSectionHandler?displayProperty=fullName> <xref:System.Web.IHttpHandler?displayProperty=fullName> です。

- クラスは、新しい制約を持つジェネリック型パラメーターとして渡されます。 たとえば、次の例では、このルールが発生します。

  ```csharp
  internal class MyClass
  {
      public DoSomething()
      {
      }
  }
  public class MyGeneric<T> where T : new()
  {
      public T Create()
      {
          return new T();
      }
  }
  // [...]
  MyGeneric<MyClass> mc = new MyGeneric<MyClass>();
  mc.Create();
  ```

  このような状況では、この警告を非表示にすることをお勧めします。

## <a name="related-rules"></a>関連規則
 [CA1811:呼び出されていないプライベート コードを使用しません](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1801:使用されていないパラメーターの確認](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)
