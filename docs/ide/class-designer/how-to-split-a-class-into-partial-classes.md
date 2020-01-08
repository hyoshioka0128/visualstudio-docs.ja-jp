---
title: '方法: 1 つのクラスを複数の部分クラスに分割する (クラス デザイナー)'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer, partial classes
- partial classes, Class Designer
ms.assetid: 6f6b0b30-3996-4569-9200-20482b3adf90
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 48672e2d316828019ede7097306517b270062327
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588682"
---
# <a name="how-to-split-a-class-into-partial-classes-in-class-designer"></a>方法: クラス デザイナーで 1 つのクラスを複数の部分クラスに分割する

`partial` キーワード (Visual Basic の場合は `Partial`) を使用して、複数の宣言間でクラスまたは構造体の宣言を分割することができます。 部分宣言は必要に応じていくつでも使用できます。

宣言は、1 つまたは複数のソース ファイルで使用できます。 すべての宣言は同じアセンブリおよび同じ名前空間にある必要があります。

部分クラスはいくつかの状況で便利です。 大規模なプロジェクトでは、たとえば、クラスを複数のファイルに分割して、複数のプログラマが同時にそのプロジェクトで作業することができます。 Visual Studio によって生成されたコードを使用している場合は、ソース ファイルを再作成しなくてもクラスを変更できます。 (Visual Studio によって生成されたコードの例には、Windows フォームと Web サービス ラッパー コードが含まれています。)Visual Studio によって作成されたファイルを変更せずに、自動生成クラスを使用するコードを作成できます。

部分メソッドには次の 2 種類があります。 C# では、宣言 (declaring) と実装 (implementing) と呼ばれています。Visual Basic では、宣言 (declaration) と実装 (implementation) と呼ばれています。

**クラス デザイナー**では、部分クラスとメソッドがサポートされます。 クラス ダイアグラムの型シェイプは、部分クラスの単一の宣言場所を参照します。 部分クラスが複数のファイルで定義されている場合、 **[プロパティ]** ウィンドウで **[新しいメンバーの場所]** プロパティを設定するときに**クラス デザイナー**により使用される宣言場所を指定できます。 つまり、クラス図形をダブルクリックすると、 **[新しいメンバーの場所]** プロパティで識別されるクラス宣言を含むソース ファイルに**クラス デザイナー**が移動します。 クラス図形の部分メソッドをダブルクリックすると、**クラス デザイナー**は部分メソッド宣言に移動します。 また、 **[プロパティ]** ウィンドウの **[ファイル名]** プロパティは宣言場所を参照します。 部分クラスの場合、 **[ファイル名]** には、そのクラスの宣言と実装コードを含むファイルがすべて一覧表示されます。 ただし、部分メソッドの場合、 **[ファイル名]** には、部分メソッド宣言が含まれるファイルのみが一覧表示されます。

次の例では、クラス `Employee` の定義が 2 つの宣言に分割され、それぞれが別のプロシージャを定義します。 この例にある 2 つの部分定義は、1 つのソース ファイル内にあっても、2 つの異なるソース ファイル内にあってもかまいません。

> [!NOTE]
> Visual Basic では、部分クラス定義を使用し、Visual Studio によって生成されたコードとユーザーが作成したコードを分離します。 コードは別個のソース ファイルに分割されます。 たとえば、**Windows フォーム デザイナー**では、`Form` などのコントロールに部分クラスを定義します。 これらのコントロールでは、生成されたコードを変更しないでください。

Visual Basic の部分型に関する詳細については、「[Partial](/dotnet/visual-basic/language-reference/modifiers/partial)」 (部分型) を参照してください。

## <a name="example"></a>例

クラス定義を分割するには、次の例のように、`partial` キーワード (Visual Basic では `Partial`) を使用します。

```csharp
// First part of class definition.
public partial class Employee
{
    public void CalculateWorkHours()
    {
    }
}

// Second part of class definition.
public partial class Employee
{
    public void CalculateTaxes()
    {
    }
}
```

```vb
' First part of class definition.
Partial Public Class Employee
    Public Sub CalculateWorkHours()
    End Sub
End Class

' Second part of class definition.
Partial Public Class Employee
    Public Sub CalculateTaxes()
    End Sub
End Class
```

## <a name="see-also"></a>関連項目

- [部分クラスと部分メソッド](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)
- [partial (型) (C# リファレンス)](/dotnet/csharp/language-reference/keywords/partial-type)
- [partial (メソッド) (C# リファレンス)](/dotnet/csharp/language-reference/keywords/partial-method)
- [Partial (Visual Basic)](/dotnet/visual-basic/language-reference/modifiers/partial)
