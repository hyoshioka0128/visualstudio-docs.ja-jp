---
title: 共通のクイック アクション
description: スペルミスのあるキーワードや記号の修正、マージの競合の解決、必要なインポートの削除、型の生成、ローカル変数の導入など、C# および Visual Basic での最も一般的なクイック アクション
ms.date: 03/28/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: db7a3a550f6bfc1250679eeefa0ba3ec6291eef0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75585523"
---
# <a name="common-quick-actions"></a>共通のクイック アクション

このトピックのセクションでは、C# と Visual Basic 両方のコードに共通に適用される**クイック アクション**の一部を示します。 このアクションは、コンパイラ診断、または Visual Studio の組み込みの [.NET Compiler Platform アナライザー](../code-quality/roslyn-analyzers-overview.md)のいずれかの*コード修正*です。

## <a name="actions-that-fix-errors"></a>エラーを修正するアクション

このセクションのクイック アクションにより、ビルドの失敗の原因となるコードのエラーが修正されます。 コード行のエラーの修正でクイック アクションが使用できる場合に余白または赤の波線の下に表示される電球のアイコンには、赤の 'x' が表示されます。

![クイック アクションのエラー アイコンとメニュー](media/error-light-bulb-with-code.png)

### <a name="correct-misspelled-symbol-or-keyword"></a>記号やキーワードのスペルミスの修正

Visual Studio で型やキーワードのスペルを誤って入力した場合、このクイック アクションは自動的にそれを修正します。 これらの項目は電球メニューで **"Change '\<misspelled word>' to '\<correct word>'"** と表示されます。 次に例を示します。

```csharp
// Before
private viod MyMethod()
{
}

// Change 'viod' to 'void'

// After
private void MyMethod()
{
}
```

```vb
' Before
Function MyFunction as Intger
End Function

' Change 'Intger' to 'Integer'

' After
Function MyFunction as Integer
End Function
```

| エラー ID | 該当言語 |
| - | - |
| CS0103、BC30002 | C# および Visual Basic |

### <a name="resolve-git-merge-conflict"></a>git のマージ競合を解決する

このクイック アクションを使用すると、"変更を取り入れる" ことで競合するコードおよびマーカーが削除され、git マージ競合を解決することができます。

```csharp
// Before
private void MyMethod()
{
    if (false)
    {

    }
}

// Take changes from 'HEAD'

// After
private void MyMethod()
{
    if (true)
    {

    }
}
```

| エラー ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| CS8300、BC37284 | C# および Visual Basic | Visual Studio 2017 バージョン 15.3 以降 |

## <a name="actions-that-remove-unnecessary-code"></a>不要なコードを削除するアクション

### <a name="remove-unnecessary-usingsimports"></a>不必要な using/Import を削除する

**[不要な using の削除]/[不要なインポートの削除]** クイック アクションは、現在のファイルで使われていない `using` および `Import` ディレクティブを削除します。 この項目を選ぶと、使われていない名前空間のインポートが削除されます。

| 該当言語 | サポートされているバージョン |
| - | - |
| C# および Visual Basic | Visual Studio 2015 以降 |

### <a name="remove-unnecessary-cast"></a>不要なキャストを削除する

ある型をキャストが不要な別の型にキャストしている場合、 **[不要なキャストの削除]** クイック アクション項目によって不要なキャストが削除されます。

```csharp
// before
int number = (int)3;

// Remove Unnecessary Cast

// after
int number = 3;
```

```vb
' Before
Dim number as Integer = CType(3, Integer)

' Remove Unnecessary Cast

' After
Dim number as Integer = 3
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0004 | C# および Visual Basic | Visual Studio 2015 以降 |

### <a name="remove-unused-variables"></a>未使用の変数を削除する

このクイック アクションでは、宣言されているがコードで一度も使用されていない変数を削除することができます。

```csharp
// Before
public MyMethod()
{
    var unused = 8;
    var used = 1;
    return DoStuff(used);
}

// Remove unused variables

// After
public MyMethod()
{
    var used = 1;
    return DoStuff(used);
}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| CS0219、BC42024 | C# および Visual Basic | Visual Studio 2017 バージョン 15.3 以降 |

### <a name="remove-type-from-default-value-expression"></a>既定の値式から型を削除する

このクイック アクションは、コンパイラが式の型を推論できる場合に、既定の値式から値の型を削除し、[既定のリテラル](/dotnet/csharp/language-reference/operators/default#default-literal)を使います。

```csharp
// Before
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }

// Simplify default expression

// After
void DoWork(CancellationToken cancellationToken = default) { ... }
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0034 | C# 7.1+ | Visual Studio 2017 バージョン 15.3 以降 |

## <a name="actions-that-add-missing-code"></a>不足しているコードを追加するアクション

### <a name="add-usingsimports-for-types-in-reference-assemblies-nuget-packages-or-other-types-in-your-solution"></a>参照アセンブリの型、NuGet パッケージの型、またはソリューション内の他の型に using/import を追加する

ソリューション内の他のプロジェクトにある型を使うとクイック アクションが自動的に表示されますが、それ以外の場合は **[ツール] > [オプション] > [C#]** または **[Basic] > [詳細設定]** タブで有効にする必要があります。

- 参照アセンブリの型に using/import を提案する
- NuGet パッケージの型に using/import を提案する

有効にした場合、現在はインポートされていなくても参照アセンブリまたは NuGet パッケージには存在する名前空間の型を使うと、using または import ディレクティブが作成されます。

```csharp
// Before
Debug.WriteLine("Hello");

// using System.Diagnostics;

// After
using System.Diagnostics;

Debug.WriteLine("Hello");
```

```vb
' Before
Debug.WriteLine("Hello")

' Imports System.Diagnostics

' After
Imports System.Diagnostics

Debug.WriteLine("Hello")
```

| 診断 ID | 該当言語 |
| - | - |
| CS0103、BC30451 | C# および Visual Basic|

### <a name="add-missing-casesdefault-caseboth"></a>足りないケース、既定のケース、または両方を追加する

`switch` ステートメント (C#) または `Select Case` ステートメント (Visual Basic) を作成するときは、コード アクションを使って、足りないケース項目、既定のケースのステートメント、または両方を自動的に追加できます。

次の列挙型を検討し、`switch` ステートメントまたは `Select Case` ステートメントを空にします。

```csharp
enum MyEnum
{
    Item1,
    Item2,
    Item3
}

...

MyEnum myEnum = MyEnum.Item1;

switch(myEnum)
{
}
```

```vb
Enum MyEnum
    Item1
    Item2
    Item3
End Enum

...

Dim myEnum as MyEnum = MyEnum.Item1

Select Case myEnum
End Select
```

**[Add Both]\(両方追加\)** のクイック アクションを使用すると、足りない case が入力されるとともに default の条件が追加されます。

```csharp
switch(myEnum)
{
    case MyEnum.Item1:
        break;
    case MyEnum.Item2:
        break;
    case MyEnum.Item3:
        break;
    default:
        break;
}
```

```vb
Select Case myEnum
    Case MyEnum.Item1
        Exit Select
    Case MyEnum.Item2
        Exit Select
    Case Else
        Exit Select
End Select
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0010 | C# および Visual Basic| Visual Studio 2017 バージョン 15.3 以降 |

### <a name="add-null-checks-for-parameters"></a>パラメーターの null チェックを追加する

このクイック アクションでは、パラメーターが null であるかどうかを示すチェックをコードに追加できます。

```csharp
// Before
class MyClass
{
    public string MyProperty { get; set; }

    public MyClass(string myProperty) // cursor inside myProperty
    {
        MyProperty = myProperty;
    }
}

// Add null check

// After
class MyClass
{
    public string MyProperty { get; set; }

    public MyClass(string myProperty)
    {
        MyProperty = myProperty ?? throw new ArgumentNullException(nameof(myProperty));
    }
}
```

| 該当言語 | サポートされているバージョン |
| -------------------- | ---------------- |
| C# および Visual Basic| Visual Studio 2017 バージョン 15.3 以降 |

### <a name="add-argument-name"></a>引数の名前を追加する

```csharp
// Before
var date = new DateTime(1997, 7, 8);

// Include argument name 'year' (include trailing arguments)

// After
var date = new DateTime(year: 1997, month: 7, day: 8);
```

| 該当言語 | サポートされているバージョン |
| -------------------- | ---------------- |
| C# および Visual Basic| Visual Studio 2017 バージョン 15.3 以降 |

### <a name="add-braces"></a>中かっこを追加する

"中かっこを追加する" クイック アクションは、単一行の `if` ステートメントを中かっこで囲みます。

```csharp
// Before
if (true)
    return "hello,world";

// Add braces

// After
if (true)
{
    return "hello,world";
}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0011 | C# | Visual Studio 2017 以降 |

### <a name="add-and-order-modifiers"></a>修飾子を追加および順序付けする

これらのクイック アクションを使用すると、既存のアクセシビリティ修飾子の並べ替えや、不足しているアクセシビリティ修飾子の追加が行えるようになり、修飾子を整理するのに便利です。

```csharp
// Before
enum Color
{
    Red, White, Blue
}

// Add accessibility modifiers

// After
internal enum Color
{
    Red, White, Blue
}
```

```csharp
// Before
static private int thisFieldIsPublic;

// Order modifiers

// After
private static int thisFieldIsPublic;
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0036 | C# および Visual Basic| Visual Studio 2017 バージョン 15.5 以降 |
| IDE0040 | C# および Visual Basic| Visual Studio 2017 バージョン 15.5 以降 |

## <a name="code-transformations"></a>コード変換

### <a name="convert-if-construct-to-switch"></a>'if' コンストラクトを 'switch' に変換する

このクイック アクションでは、**if-then-else** コンストラクトを **switch** コンストラクトに変換することができます。

```csharp
// Before
if (obj is string s)
{
  Console.WriteLine("obj is a string: " + s);
}

else if (obj is int i && i > 10)
{
  Console.WriteLine("obj is an int greater than 10");
}

// Convert to switch

// After
switch (obj)
{
  case string s:
    Console.WriteLine("Obj is a string: " + s);
    break;
  case int i when i > 10:
    Console.WriteLine("obj is an int greater than 10");
    break;
}
```

```vb
' Before
If TypeOf obj Is String s Then
    Console.WriteLine("obj is a string: " + s)
Else If TypeOf obj Is Integer i And i > 10 Then
    Console.WriteLine("obj is an int greater than 10")
End If

' Convert to switch

' After
Select Case obj
  Case String s
    Console.WriteLine("Obj is a string: " + s)
    Exit Sub
  Case Integer i when i > 10
    Console.WriteLine("obj is an int greater than 10")
    Exit Sub
End Select
```

| 該当言語 | サポートされているバージョン |
| -------------------- | ---------------- |
| C# および Visual Basic| Visual Studio 2017 バージョン 15.3 以降 |

### <a name="convert-to-interpolated-string"></a>挿入文字列に変換する

[挿入文字列](/dotnet/csharp/language-reference/keywords/interpolated-strings)は、埋め込み変数を含む文字列を表現する簡単な方法であり、 **[String.Format](/dotnet/api/system.string.format#overloads)** メソッドに似ています。  このクイック アクションは、文字列が連結されている場合、または **String.Format** が使われている場合を認識し、それを挿入文字列に変更します。

```csharp
// Before
int num = 3;
string s = string.Format("My string with {0} in the middle", num);

// Convert to interpolated string

// After
int num = 3;
string s = $"My string with {num} in the middle";
```

```vb
' Before
Dim num as Integer = 3
Dim s as String = String.Format("My string with {0} in the middle", num)

' Convert to interpolated string

' After
Dim num as Integer = 3
Dim s As String = $"My string with {num} in the middle"
```

| 該当言語 | サポートされているバージョン |
| -------------------- | ---------------- |
| C# 6.0+ および Visual Basic 14+ | Visual Studio 2017 以降 |

### <a name="use-object-initializers"></a>オブジェクト初期化子を使用する

このクイック アクションでは、コンストラクターを呼び出して代入ステートメントの行を追加するのでなく、[オブジェクト初期化子](/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers)を使用することができます。

```csharp
// Before
var c = new Customer();
c.Age = 21;

// Object initialization can be simplified

// After
var c = new Customer() { Age = 21 };
```

```vb
' Before
Dim c = New Customer()
c.Age = 21

' Object initialization can be simplified

' After
Dim c = New Customer() With {.Age = 21}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0017 | C# および Visual Basic | Visual Studio 2017 以降 |

### <a name="use-collection-initializers"></a>コレクション初期化子を使用する

このクイック アクションでは、クラスの `Add` メソッドを複数回呼び出すのではなく、[コレクション初期化子](/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers)を使用することができます。

```csharp
// Before
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);

// Collection initialization can be simplified

// After
var list = new List<int> { 1, 2, 3 };
```

```vb
' Before
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)

' Collection initialization can be simplified

' After
Dim list = New List(Of Integer) From {1, 2, 3}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0028 | C# および Visual Basic | Visual Studio 2017 以降 |

### <a name="convert-auto-property-to-full-property"></a>自動プロパティを完全なプロパティに変換する

このクイック アクションでは、自動プロパティから完全なプロパティへの変換、またはその逆の変換を行うことができます。

```csharp
// Before
private int MyProperty { get; set; }

// Convert to full property

// After
private int MyProperty
{
    get { return _myProperty; }
    set { _myProperty = value; }
}
```

```vb
' Before
Public Property Name As String

' Convert to full property

' After
Private _Name As String

Public Property Name As String
    Get
        Return _Name
    End Get
    Set
        _Name = Value
    End Set
End Property
```

| 該当言語 | サポートされているバージョン |
| -------------------- | ---------------- |
| C# および Visual Basic | Visual Studio 2017 バージョン 15.5 以降 |

### <a name="convert-block-body-to-expression-bodied-member"></a>ブロック本体を式のようなメンバーに変換する

このクイック アクションではブロック本体を、メソッド、コンストラクター、演算子、プロパティ、インデクサー、およびアクセサー用の式のようなメンバーに変換します。

```csharp
//Before
class MyClass4
{
    private int _myProperty;

    public int MyProperty
    {
        get { return _myProperty; }
        set
        {
            _myProperty = value;
        }
    }

    public MyClass4(int myProperty)
    {
        MyProperty = myProperty;
    }

    public void PrintProperty()
    {
        Console.WriteLine(MyProperty);
    }
}

// Use expression body for accessors/constructors/methods

// After
class MyClass4
{
    private int _myProperty;

    public int MyProperty
    {
        get => _myProperty;
        set => _myProperty = value;
    }

    public MyClass4(int myProperty) => MyProperty = myProperty;

    public void PrintProperty() => Console.WriteLine(MyProperty);
}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0021-27 | C# 6.0+ | Visual Studio 2017 以降 |

### <a name="convert-anonymous-function-to-local-function"></a>匿名関数をローカル関数に変換する

このクイック アクションは、匿名関数をローカル関数に変換します。

```csharp
// Before
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};

// Use local function

// After
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

### <a name="convert-referenceequals-to-is-null"></a>'ReferenceEquals' を 'is null' に変換する

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0041 | C# 7.0+ | Visual Studio 2017 バージョン 15.5 以降 |

このクイック アクションでは、可能な限り、```ReferenceEquals``` コーディング パターンではなく、[パターン マッチング](/dotnet/csharp/pattern-matching)の使用を提案します。

```csharp
// Before
var value = "someString";
if (object.ReferenceEquals(value, null))
{
    return;
}

// Use 'is null' check

// After
var value = "someString";
if (value is null)
{
    return;
}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0039 | C# 7.0+ | Visual Studio 2017 バージョン 15 以降 |

### <a name="introduce-pattern-matching"></a>パターン マッチングを導入する

このクイック アクションでは、C# におけるキャストおよび null チェックで、[パターン マッチング](/dotnet/csharp/pattern-matching)の使用を提案します。

```csharp
// Before
if (o is int)
{
    var i = (int)o;
    ...
}

// Use pattern matching

// After
if (o is int i)
{
    ...
}
```

```csharp
// Before
var s = o as string;
if (s != null)
{
    ...
}

// Use pattern matching

// After
if (o is string s)
{
    ...
}
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0020 | C# 7.0+ | Visual Studio 2017 以降 |
| IDE0019 | C# 7.0+ | Visual Studio 2017 以降 |

### <a name="change-base-for-numeric-literals"></a>数値リテラルの基本を変更する

このクイック アクションでは、数値リテラルの基本数値システムを別のものに変換できます。 たとえば、数値を 16 進数からバイナリ形式に変更できます。

```csharp
// Before
int countdown = 2097152;

// Convert to hex

// After
int countdown = 0x200000;
```

```vb
' Before
Dim countdown As Integer = 2097152

' Convert to hex

' After
Dim countdown As Integer = &H200000
```

| 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| C# 7.0+ および Visual Basic 14+ | Visual Studio 2017 バージョン 15.3 以降 |

### <a name="insert-digit-separators-into-literals"></a>リテラルに桁区切り記号を挿入する

このクイック アクションでは、区切り文字をリテラル値に追加することができます。

```csharp
// Before
int countdown = 1000000;

// Separate thousands

// After
int countdown = 1_000_000;
```

```vb
' Before
Dim countdown As Integer = 1000000

' Separate thousands

' After
Dim countdown As Integer = 1_000_000
```

| 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| C# 7.0+ および Visual Basic 14+ | Visual Studio 2017 バージョン 15.3 以降 |

### <a name="use-explicit-tuple-names"></a>明示的なタプル名を使用する

このクイック アクションでは、Item1、Item2 などのタプル名ではなく、明示的なタプル名を使用できる領域を識別します。

```csharp
// Before
(string name, int age) customer = GetCustomer();
var name = customer.Item1;

// Use explicit tuple name

// After
(string name, int age) customer = GetCustomer();
var name = customer.name;
```

```vb
' Before
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1

' Use explicit tuple name

' After
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0033 | C# 7.0+ および Visual Basic 15+ | Visual Studio 2017 以降 |

### <a name="use-inferred-names"></a>推論による名前を使用する

このクイック アクションでは、匿名型で推論されるメンバー名やタプルで推論される要素名を使用する場合、どのようなときにコードを簡略化できるかがわかります。

```csharp
// Before
var anon = new { age = age, name = name };

// Use inferred member name

// After
var anon = new { age, name };
```

```csharp
// Before
var tuple = (age: age, name: name);

// Use inferred tuple element name

// After
var tuple = (age, name);
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0037 | C# | Visual Studio 2017 バージョン 15.5 以降 |
| IDE0037 | C# 7.1+ | Visual Studio 2017 バージョン 15.5 以降 |

### <a name="deconstruct-tuple-declaration"></a>タプル宣言を分解する

このクイック アクションでは、タプル変数宣言を分解することができます。

```csharp
// Before
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");

//Deconstruct variable declaration

// After
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");
```

| 診断 ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| IDE0042 | C# 7.0+ | Visual Studio 2017 バージョン 15.5 以降 |

### <a name="make-method-synchronous"></a>メソッドを同期させる

`async` または `Async` のキーワードをメソッドで使う場合は、そのメソッド内で `await` または `Await` のキーワードも使われることが予想されます。 ただし、そうではない場合は、クイック アクションが表示され、`async` または `Async` のキーワードを削除して戻り値の型を変更することにより、同期メソッドにすることができます。 [クイック アクション] メニューの **[メソッドを同期させます]** オプションを選びます。

```csharp
// Before
async Task<int> MyAsyncMethod()
{
    return 3;
}

// Make method synchronous

// After
int MyAsyncMethod()
{
    return 3;
}
```

```vb
' Before
Async Function MyAsyncMethod() As Task(Of Integer)
    Return 3
End Function

' Make method synchronous

' After
Function MyAsyncMethod() As Integer
    Return 3
End Function
```

| エラー ID | 該当言語 |
| ------- | -------------------- |
| CS1998、BC42356 | C# および Visual Basic |

### <a name="make-method-asynchronous"></a>メソッドを非同期にする

メソッド内で `await` または `Await` のキーワードを使うときは、メソッドに `async` または `Async` のキーワードが指定されていることが想定されます。 ただし、そうではない場合は、メソッドを非同期にするクイック アクションが表示されます。 [クイック アクション] メニューの **[Make method/Function asynchronous (メソッド/関数を非同期にします)]** オプションを使います。

```csharp
// Before
int MyAsyncMethod()
{
    return await Task.Run(...);
}

// Make method asynchronous

// After
async Task<int> MyAsyncMethod()
{
    return await Task.Run(...);
}
```

```vb
' Before
Function MyAsyncMethod() as Integer
    Return  Await Task.Run(...)
End Function

' Make method asynchronous

' After
Async Function MyAsyncMethod() As Task(Of Integer)
    Return Await Task.Run(...)
End Function
```

| エラー ID | 該当言語 | サポートされているバージョン |
| ------- | -------------------- | ---------------- |
| CS4032、BC37057 | C# および Visual Basic | Visual Studio 2017 以降 |

## <a name="see-also"></a>参照

- [クイック アクション](../ide/quick-actions.md)
