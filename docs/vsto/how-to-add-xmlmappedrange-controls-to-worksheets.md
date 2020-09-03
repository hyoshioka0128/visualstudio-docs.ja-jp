---
title: '方法: ワークシートに XMLMappedRange コントロールを追加する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1d69e705e8f537ba3636422ad6883a7633e03322
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544886"
---
# <a name="how-to-add-xmlmappedrange-controls-to-worksheets"></a>方法: ワークシートに XMLMappedRange コントロールを追加する
  XML 要素を Microsoft Office Excel のセルにマップすると、Visual Studio によって自動的に <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールがワークシートに追加されます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> コントロールは、 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> **ツールボックス** または [ **データソース** ] ウィンドウでは使用できません。 また、プログラムによってコントロールを作成することはできません <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 。

## <a name="to-add-an-xmlmappedrange-control-to-a-worksheet"></a>ワークシートに XMLMappedRange コントロールを追加するには

1. Visual Studio デザイナーで Excel ブックを開きます。

2. コントロールを追加するワークシートを開きます。

3. [ **開発者** ] タブで、[ **ソース**] をクリックします。

    > [!NOTE]
    > リボンに [ **開発者** ] タブが表示されていない場合は、有効にする必要があります。 詳細については、「 [方法: リボンに [開発者] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

     [ **XML ソース** ] 作業ウィンドウが表示されます。

4. [ **Xml ソース** ] タスクペインで、[ **xml マップ**] をクリックします。

5. [ **XML マップ** ] ダイアログボックスで、[ **追加**] をクリックします。

     [ **XML ソース** ] ダイアログボックスが表示されます。

6. [ **Xml ソース** ] ダイアログボックスから xml スキーマを選択し、[ **開く**] をクリックします。

     [ **XML マップ** ] ダイアログボックスにスキーマが追加されます。

7. [ **XML マップ** ] ダイアログボックスで、[ **OK]** をクリックします。

8. [ **XML ソース** ] 作業ウィンドウからワークシート上のセルに要素をドラッグします。

     <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>が作成され、プロジェクトに追加されます。

    > [!NOTE]
    > [ **XML ソース** ] 作業ウィンドウから親要素をドラッグすると、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが作成されます。

## <a name="see-also"></a>関連項目
- [XmlMappedRange コントロール](../vsto/xmlmappedrange-control.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [方法: Visual Studio 内のワークシートにスキーマをマップする](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
