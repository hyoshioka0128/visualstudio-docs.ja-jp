---
title: Office ソリューションの遅延バインディング
description: Microsoft Office アプリケーション内のオブジェクトモデルのいくつかの型が、遅延バインディング機能を通じて使用できる機能を提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- objects [Office development in Visual Studio], casting
- types [Office development in Visual Studio], casting
- automation [Office development in Visual Studio], casting objects
- casting, object to specific type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e618dcd0cc699b4626f825890cf0fc8bd7ddd853
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823887"
---
# <a name="late-binding-in-office-solutions"></a>Office ソリューションの遅延バインディング
  Office アプリケーションのオブジェクトモデルの一部の型は、遅延バインディング機能を通じて使用できる機能を提供します。 たとえば、一部のメソッドとプロパティは、Office アプリケーションのコンテキストに応じて異なる種類のオブジェクトを返すことがあり、一部の型は異なるコンテキストで異なるメソッドまたはプロパティを公開できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 **Option Strict** が off で、またはを対象とする Visual C# プロジェクト [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] が、これらの [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 遅延バインディング機能を使用する型を直接操作できるプロジェクト Visual Basic ます。

## <a name="implicit-and-explicit-casting-of-object-return-values"></a>オブジェクトの戻り値の暗黙的および明示的なキャスト
 Microsoft Office プライマリ相互運用機能アセンブリ (Pia) の多くのメソッドとプロパティは、 <xref:System.Object> 複数の異なる型のオブジェクトを返すことができるため、値を返します。 たとえば、プロパティはを <xref:Microsoft.Office.Tools.Excel.Workbook.ActiveSheet%2A> 返し <xref:System.Object> ます。これは、 <xref:Microsoft.Office.Interop.Excel.Worksheet> <xref:Microsoft.Office.Interop.Excel.Chart> アクティブなシートの内容に応じて、戻り値がまたはオブジェクトである可能性があるためです。

 メソッドまたはプロパティがを返す場合は <xref:System.Object> 、 **Option Strict** がオンになっている Visual Basic プロジェクトで、オブジェクトを適切な型に明示的に変換 (Visual Basic) する必要があります。 <xref:System.Object> **Option Strict** がオフになっている Visual Basic プロジェクトでは、戻り値を明示的にキャストする必要はありません。

 ほとんどの場合、参照ドキュメントには、を返すメンバーの戻り値の型が一覧表示され <xref:System.Object> ます。 オブジェクトを変換またはキャストすると、コードエディターでオブジェクトの IntelliSense が有効になります。

 Visual Basic での変換の詳細については、「暗黙的な変換と明示的な変換」を参照してください [&#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions) および [CType 関数 &#40;](/dotnet/visual-basic/language-reference/functions/ctype-function)Visual Basic&#41;。

### <a name="examples"></a>例
 **Option Strict** がオンの Visual Basic プロジェクト内の特定の型にオブジェクトをキャストする方法を次のコード例に示します。 この種類のプロジェクトでは、プロパティを明示的ににキャストする必要があり <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> <xref:Microsoft.Office.Interop.Excel.Range> ます。 この例では、という名前のワークシートクラスを含むドキュメントレベルの Excel プロジェクトが必要です `Sheet1` 。

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet9":::

 次のコード例は、 **Option Strict** がオフ Visual Basic であるか、を対象とする Visual C# プロジェクトで、オブジェクトを特定の型に暗黙的にキャストする方法を示して [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] います。 これらの種類のプロジェクトでは、 <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> プロパティはに暗黙的にキャストされ <xref:Microsoft.Office.Interop.Excel.Range> ます。 この例では、という名前のワークシートクラスを含むドキュメントレベルの Excel プロジェクトが必要です `Sheet1` 。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet10":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="access-members-that-are-available-only-through-late-binding"></a>遅延バインディングによってのみ使用できるメンバーにアクセスする
 Office Pia の一部のプロパティとメソッドは、遅延バインディングによってのみ使用できます。 **Option Strict** がオフであるか、またはを対象とする Visual C# プロジェクトで Visual Basic プロジェクトで [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] は、これらの [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 言語の遅延バインディング機能を使用して、遅延バインドされたメンバーにアクセスできます。 **Option Strict** がオンになっている Visual Basic プロジェクトでは、これらのメンバーにアクセスするためにリフレクションを使用する必要があります。

### <a name="examples"></a>例
 次のコード例は、 **Option Strict** がオフであるか、を対象とする Visual C# プロジェクト内の Visual Basic プロジェクトの遅延バインディングメンバーにアクセスする方法を示して [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] います。 この例では、Word の [**ファイルを開く**] ダイアログボックスの "遅延バインディング **名**" プロパティにアクセスします。 この例を使用するに `ThisDocument` は、 `ThisAddIn` Word プロジェクトのクラスまたはクラスから実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet122":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet122":::

 次のコード例は、 **Option Strict** がオンになっている Visual Basic プロジェクトで同じタスクを実行するためにリフレクションを使用する方法を示しています。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet102":::

## <a name="see-also"></a>関連項目
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [「Dynamic &#40;C&#35; プログラミングガイド」を参照してください&#41;](/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [リフレクション (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [リフレクション (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
