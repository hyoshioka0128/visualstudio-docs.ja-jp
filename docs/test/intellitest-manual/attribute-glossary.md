---
title: 属性の解説 | Microsoft IntelliTest 開発者テスト ツール
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Attribute glossary
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 00d8b24d26237a3c7b4130eba4614b5ea7b7eccd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89315227"
---
# <a name="attribute-glossary"></a>属性の解説

## <a name="attributes-by-namespace"></a>名前空間別の属性

* **Microsoft.Pex.Framework**
  * [PexAssumeNotNull](#pexassumenotnull)
  * [PexClass](#pexclass)
  * [PexGenericArguments](#pexgenericarguments)
  * [PexMethod](#pexmethod)
    * [PexExplorationAttributeBase](#pexexplorationattributebase)

* **Microsoft.Pex.Framework.Settings**
  * [PexAssemblySettings](#pexassemblysettings)

* **Microsoft.Pex.Framework.Instrumentation**
  * [PexAssemblyUnderTest](#pexassemblyundertest)
  * [PexInstrumentAssembly](#pexinstrumentassemblyattribute)

* **Microsoft.Pex.Framework.Using**
  * [PexUseType](#pexusetype)

* **Microsoft.Pex.Framework.Validation**
  * [PexAllowedException](#pexallowedexception)
  * [PexAllowedExceptionFromAssembly](#pexallowedexceptionfromassembly)
  * [PexAllowedExceptionFromType](#pexallowedexceptionfromtype)
  * [PexAllowedExceptionFromTypeUnderTest](#pexallowedexceptionfromtypeundertest)

<a name="pexassumenotnull"></a>
## <a name="pexassumenotnull"></a>PexAssumeNotNull

この属性は、制御された値が **null** ではないことをアサートします。 次のものにアタッチできます。

* パラメーター化されたテスト メソッドの**パラメーター**

  ```csharp
  // assume foo is not null
  [PexMethod]
  public void SomeTest([PexAssumeNotNull]IFoo foo, ...) {}
  ```

* **フィールド**

  ```csharp
  public class Foo {
     // this field should not be null
     [PexAssumeNotNull]
     public object Bar;
  }
  ```

* **型**

  ```csharp
  // never consider null for Foo types
  [PexAssumeNotNull]
  public class Foo {}
  ```

テスト アセンブリ、テスト フィクスチャ、またはテスト メソッドにアタッチすることもできます。その場合、最初の引数では、想定が適用されるフィールドまたは型を指定する必要があります。 属性が型に適用される場合は、この仮引数型のすべてのフィールドに適用されます。

<a name="pexclass"></a>
## <a name="pexclass"></a>PexClass

この属性は、"*探索*" を含むクラスをマークします。 MSTest の **TestClassAttribute** (または、NUnit の **TestFixtureAttribute**) と同等です。 この属性は省略できます。

[PexClass](#pexclass) でマークされるクラスは、"*既定で構造化可能*" である必要があります。

* パブリックにエクスポートされる型
* 既定のコンストラクター
* 非抽象

クラスがこれらの要件を満たしていない、エラーが報告されて、探索は失敗します。

また、IntelliTest がクラスの一部である新しいテストを別のファイルに生成できるように、これらのクラスを **partial** にすることを強くお勧めします。 この方法は[可視性](input-generation.md#visibility)による多くの問題を解決し、一般に C# での手法です。

**その他のスイートとカテゴリ**:

```csharp
[TestClass] // MSTest test fixture attribute
[PexClass(Suite = "checkin")] // fixture attribute
public partial class MyTests { ... }
```

**テスト対象の型の指定**:

```csharp
[PexClass(typeof(Foo))] // this is a test for Foo
public partial class FooTest { ... }
```

クラスには、[PexMethod](#pexmethod) で注釈が付けられたメソッドが含まれることがあります。 IntelliTest は[セットアップと破棄のメソッド](test-generation.md#setup-teardown)も認識します。

<a name="pexgenericarguments"></a>
## <a name="pexgenericarguments"></a>PexGenericArguments

この属性は、[パラメーター化されたジェネリック単体テスト](test-generation.md#generic-parameterized)をインスタンス化するために型のタプルを提供します。

<a name="pexmethod"></a>
## <a name="pexmethod"></a>PexMethod

この属性は、[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)としてメソッドをマークします。
メソッドは、[PexClass](#pexclass) 属性でマークされたクラス内に存在する必要があります。

IntelliTest は従来のパラメーターなしのテストを生成し、これは異なるパラメーターで[パラメーター化された単体テスト](test-generation.md#parameterized-unit-testing)を呼び出します。

パラメーター化された単体テスト:

* インスタンス メソッドである必要があります
* 生成されたテストが[設定ウォーターフォール](settings-waterfall.md)に従って配置されるテスト クラスに対して[可視](input-generation.md#visibility)である必要があります
* 任意の数のパラメーターを受け取ることができます
* ジェネリックでもかまいません

**例**

```csharp
[PexClass]
public partial class MyTests {
     [PexMethod]
     public void MyTest(int i)
     { ... }
}
```

<a name="pexexplorationattributebase"></a>
## <a name="pexexplorationattributebase"></a>PexExplorationAttributeBase

[詳細情報](xref:Microsoft.Pex.Framework.PexExplorationAttributeBase)

<a name="pexassemblysettings"></a>
## <a name="pexassemblysettings"></a>PexAssemblySettings

この属性は、アセンブリ レベルで設定して、すべての探索の既定の設定値をオーバーライドできます。

```csharp
using Microsoft.Pex.Framework;
// overriding the test framework selection
[assembly: PexAssemblySettings(TestFramework = "MSTestv2")]
```

<a name="pexassemblyundertest"></a>
## <a name="pexassemblyundertest"></a>PexAssemblyUnderTest

この属性は、現在のテスト プロジェクトによってテストされているアセンブリを指定します。

```csharp
[assembly: PexAssemblyUnderTest("MyAssembly")]
```

<a name="pexinstrumentassemblyattribute"></a>
## <a name="pexinstrumentassemblyattribute"></a>PexInstrumentAssemblyAttribute

この属性は、インストルメント化されるアセンブリの指定に使われます。

**例**

```csharp
using Microsoft.Pex.Framework;

// the assembly containing ATypeFromTheAssemblyToInstrument should be instrumented
[assembly: PexInstrumentAssembly(typeof(ATypeFromTheAssemblyToInstrument))]

// the assembly name can be used as well
[assembly: PexInstrumentAssembly("MyAssemblyName")]
```

<a name="pexusetype"></a>
## <a name="pexusetype"></a>PexUseType

この属性は、特定の型を使用して基本型またはインターフェイスをインスタンス化 (抽象化) できることが IntelliTest に伝えられます。

**例**

```csharp
[PexMethod]
[PexUseType(typeof(A))]
[PexUseType(typeof(B))]
public void MyTest(object testParameter)
{
     ... // IntelliTest will consider types A and B to instantiate 'testParameter'
}
```

<a name="pexallowedexception"></a>
## <a name="pexallowedexception"></a>PexAllowedException

この属性を [PexMethod](#pexmethod) (または [PexClass](#pexclass)) にアタッチすると、テストが失敗するときを示す IntelliTest の既定のロジックが変更されます。 テストは、指定された例外をスローした場合であっても、失敗と見なされません。

**例**

次のテストは、**Stack** のコンストラクターが **ArgumentOutOfRangeException** をスローできることを指定します。

```csharp
class Stack {
  int[] _elements;
  int _count;
  public Stack(int capacity) {
    if (capacity<0) throw new ArgumentOutOfRangeException();
    _elements = new int[capacity];
    _count = 0;
  }
  ...
}
```

フィルターは次のようにフィクスチャにアタッチされます (アセンブリ レベルまたはテスト レベルでも定義できます)。

```csharp
[PexMethod]
[PexAllowedException(typeof(ArgumentOutOfRangeException))]
class CtorTest(int capacity) {
  Stack s = new Stack(capacity); // may throw ArgumentOutOfRangeException
}
```

<a name="pexallowedexceptionfromassembly"></a>
## <a name="pexallowedexceptionfromassembly"></a>PexAllowedExceptionFromAssembly

[詳細情報](xref:Microsoft.Pex.Framework.Validation.PexAllowedExceptionFromAssemblyAttribute)

<a name="pexallowedexceptionfromtype"></a>
## <a name="pexallowedexceptionfromtype"></a>PexAllowedExceptionFromType

[詳細情報](xref:Microsoft.Pex.Framework.Validation.PexAllowedExceptionFromTypeAttribute)

<a name="pexallowedexceptionfromtypeundertest"></a>
## <a name="pexallowedexceptionfromtypeundertest"></a>PexAllowedExceptionFromTypeUnderTest

[詳細情報](xref:Microsoft.Pex.Framework.Validation.PexAllowedExceptionFromTypeUnderTestAttribute)

## <a name="got-feedback"></a>フィードバックが欲しい場合

ご意見や機能に関するご要望を[開発者コミュニティ](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)で投稿してください。
