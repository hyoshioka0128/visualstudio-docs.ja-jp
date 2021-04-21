---
title: '方法: プログラムによってワークシートの範囲内のテキストを検索する'
description: Visual Studio を使用して、Microsoft Excel ワークシートの範囲内のテキストをプログラムで検索する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, searching
- text [Office development in Visual Studio], searching in worksheets
- text searches, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 762cb3fc35b43bfd3ad15aea669adff2d370b632
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827943"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>方法: プログラムによってワークシートの範囲内のテキストを検索する
  <xref:Microsoft.Office.Interop.Excel.Range.Find%2A>オブジェクトのメソッドを <xref:Microsoft.Office.Interop.Excel.Range> 使用すると、範囲内のテキストを検索できます。 このテキストは、やなどのワークシートのセルに表示されるエラー文字列のいずれかにすることもでき `#NULL!` `#VALUE!` ます。 エラー文字列の詳細については、「 [セルエラー値](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values)」を参照してください。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 次の例では、という名前の範囲を検索 `Fruits` し、"りんご" という単語を含むセルのフォントを変更します。 この手順では、 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 以前に設定した検索設定を使用して検索を繰り返すメソッドも使用します。 検索するセルを指定すると、 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> メソッドが残りの部分を処理します。

> [!NOTE]
> <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A>メソッドの検索は、範囲の末尾に到達した後、検索範囲の先頭に戻ります。 コードでは、無限ループ内で検索がラップされていないことを確認する必要があります。 このサンプルプロシージャは、プロパティを使用してこれを処理する方法の1つを示して <xref:Microsoft.Office.Interop.Excel.Range.Address%2A> います。

## <a name="to-search-for-text-in-a-worksheet-range"></a>ワークシートの範囲内のテキストを検索するには

1. 範囲全体、検出された最初の範囲、および現在の見つかった範囲を追跡するための変数を宣言します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet58":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet58":::

2. 最初に一致した文字列を検索し、その後に検索するセル以外のすべてのパラメーターを指定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet59":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet59":::

3. 一致するものがある限り、検索を続行します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet60":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet60":::

4. 最初に見つかった範囲 ( `firstFind` ) と **Nothing** を比較します。 `firstFind`に値が含まれていない場合、コードは見つかった範囲 () を格納し `currentFind` ます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet61":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet61":::

5. 見つかった範囲のアドレスが最初に見つかった範囲のアドレスと一致する場合は、ループを終了します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet62":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet62":::

6. 検出された範囲の外観を設定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet63":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet63":::

7. 別の検索を実行します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet64":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet64":::

   このメソッドを使ったサンプル コード全体を次に示します。

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet57":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet57":::

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
