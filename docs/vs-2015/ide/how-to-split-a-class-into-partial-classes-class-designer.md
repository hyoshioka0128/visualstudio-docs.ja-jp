---
title: '方法: 1 つのクラスを複数の部分クラスに分割する (クラス デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Class Designer, partial classes
- partial classes, Class Designer
ms.assetid: 6f6b0b30-3996-4569-9200-20482b3adf90
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9e93ebc58e4e9b6092921e4155fe3d821bb552c7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670713"
---
# <a name="how-to-split-a-class-into-partial-classes-class-designer"></a>方法: 1 つのクラスを複数の部分クラスに分割する (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

複数の宣言間でクラスまたは構造体の宣言を分割できます。Visual Basic の場合、`Partial` キーワードを、Visual C# の場合、`partial` キーワードを使用します。 部分宣言は必要な数だけ使用できます。複数のソース ファイルで使用することも、1 つのソース ファイルで使用することもできます。 ただし、すべての宣言は同じアセンブリおよび同じ名前空間にある必要があります。

 部分クラスはいくつかの状況で便利です。 たとえば、大規模なプロジェクトで作業しているとき、クラスを複数のファイルに分割すれば、複数のプログラマーが同時に作業できます。 Visual Studio によって生成されたコードを使用しているとき、ソース ファイルを再作成しなくてもクラスを変更できます。 (Visual Studio によって生成されたコードの例には、Windows フォームと Web サービス ラッパー コードが含まれています。)Visual Studio によって作成されたファイルを変更せずに、自動生成クラスを使用するコードを作成できます。

 部分メソッドには次の 2 種類があります。 Visual C# では、宣言 (declaring) と実装 (implementing) と呼ばれています。Visual Basic では、宣言 (declaration) と実装 (implementation) と呼ばれています。

 クラス デザイナーは部分クラスとメソッドに対応しています。 クラス ダイアグラムの型シェイプは、部分クラスの単一の宣言場所を参照します。 部分クラスが複数のファイルで定義されている場合、 **[プロパティ]** ウィンドウで **[新しいメンバーの場所]** プロパティを設定するときにクラス デザイナーにより使用される宣言場所を指定できます。 つまり、クラスのシェイプをダブルクリックすると、 **[新しいメンバーの場所]** プロパティで識別されるクラス宣言を含むソース ファイルにクラス デザイナーが移動します。 クラスのシェイプの部分メソッドをダブルクリックすると、クラス デザイナーは部分メソッド宣言に移動します。 また、 **[プロパティ]** ウィンドウの **[ファイル名]** プロパティは宣言場所を参照します。 部分クラスの場合、 **[ファイル名]** には、そのクラスの宣言と実装コードを含むファイルがすべて一覧表示されます。 ただし、部分メソッドの場合、 **[ファイル名]** には、部分メソッド宣言が含まれるファイルのみが一覧表示されます。

 次の例では、クラス `Employee` の定義が 2 つの宣言に分割され、それぞれが別のプロシージャを定義します。 この例にある 2 つの部分定義は、1 つのソース ファイル内にあっても、2 つの異なるソース ファイル内にあってもかまいません。

> [!NOTE]
> Visual Basic では、部分クラス定義を使用し、Visual Studio によって生成されたコードとユーザーが作成したコードを分離します。 コードは別個のソース ファイルに分割されます。 たとえば、**Windows フォーム デザイナー**では、`Form` などのコントロールに部分クラスを定義します。 これらのコントロールでは、生成されたコードを変更しないでください。

 Visual Basic の部分型に関する詳細については、「[Partial](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448)」 (部分型) を参照してください。

## <a name="example"></a>例
 Visual Basic でクラス定義を分割するには、次の例のように、`Partial` キーワードを使用します。

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

## <a name="example"></a>例
 Visual C# でクラス定義を分割するには、次の例のように、`partial` キーワードを使用します。

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

## <a name="see-also"></a>関連項目
 部分[クラスとメソッド](https://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1)部分 ([型)](https://msdn.microsoft.com/library/27320743-a22e-4c7b-b0b3-53afe3607334) partial ([メソッド) (C#参照)](https://msdn.microsoft.com/library/43f40242-17e0-4452-8573-090503ad3137) [部分](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448)
