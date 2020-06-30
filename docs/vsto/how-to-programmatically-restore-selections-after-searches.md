---
title: '方法: プログラムによって検索後に選択を復元する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- searches, restoring selection after
- documents [Office development in Visual Studio], restoring selections
- selections, restoring after a search
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 30daa81c33070db3f9418b45b84b4acc6e243dc9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547096"
---
# <a name="how-to-programmatically-restore-selections-after-searches"></a>方法: プログラムによって検索後に選択を復元する
  ドキュメント内のテキストを検索して置換する場合は、検索の完了後にユーザーの元の選択を復元することができます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 サンプルプロシージャのコードでは、2つのオブジェクトを使用し <xref:Microsoft.Office.Interop.Word.Range> ます。 1つは現在のを格納 <xref:Microsoft.Office.Interop.Word.Selection> し、もう1つは検索範囲として使用するドキュメント全体を設定します。

## <a name="to-restore-the-users-original-selection-after-a-search"></a>検索後にユーザーの元の選択を復元するには

1. <xref:Microsoft.Office.Interop.Word.Range>ドキュメントと現在の選択範囲のオブジェクトを作成します。

    [!code-vb[Trin_VstcoreWordAutomation#83](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#83)]
    [!code-csharp[Trin_VstcoreWordAutomation#83](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#83)]

2. 検索と置換の操作を実行します。

    [!code-vb[Trin_VstcoreWordAutomation#84](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#84)]
    [!code-csharp[Trin_VstcoreWordAutomation#84](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#84)]

3. [範囲の開始] を選択して、ユーザーの元の選択を復元します。

    [!code-vb[Trin_VstcoreWordAutomation#85](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#85)]
    [!code-csharp[Trin_VstcoreWordAutomation#85](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#85)]

   このメソッドを使ったサンプル コード全体を次に示します。

## <a name="example"></a>例
 [!code-vb[Trin_VstcoreWordAutomation#82](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#82)]
 [!code-csharp[Trin_VstcoreWordAutomation#82](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#82)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [方法: プログラムによって Word の検索オプションを設定する](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [方法: ドキュメント内の見つかった項目をプログラムによってループする](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
