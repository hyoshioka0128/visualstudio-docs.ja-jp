---
title: XmlMappedRange コントロール
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, data binding
- XMLMappedRange control
- XMLMappedRange control, events
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 01417d9c08491edc882f7f758bb36e6184500e52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985361"
---
# <a name="xmlmappedrange-control"></a>XmlMappedRange コントロール
  コントロールは、 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 非繰り返しスキーマ要素が Microsoft Office Excel のセルにマップされている場合にのみ作成される範囲です。 たとえば、 `maxOccurs` スキーマ要素の属性が1と等しい場合です。 XML にマップされた範囲が Visual Studio によって作成された後は、Excel オブジェクトモデルを走査する必要なく、直接プログラミングできます。 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>要素のマッピングが削除された場合にのみ、Excel 内のコントロールを削除できます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="bind-data-to-the-control"></a>コントロールにデータをバインドする
 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>コントロールでは、単一のデータフィールドへのバインド (単純データバインディング) がサポートされています。 コントロールは、 <xref:Microsoft.Office.Tools.Excel.ListObject> 複合データバインディングをサポートでき、繰り返しスキーマ要素がセルにマップされるときに自動的に作成されます。 詳細については、「 [ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>コントロールは、プロパティを使用してデータソースにバインドされ <xref:System.Windows.Forms.Control.DataBindings%2A> ます。 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>がワークシートセルに追加されると、Visual Studio は、マップされたセル内のデータからデータセットを自動的に生成し、そのデータセットにコントロールをバインドします。 の既定のデータバインディングプロパティ <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> は <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Value2%2A> です。

 バインドされたデータセット内のデータが任意のメカニズムによって更新された場合、コントロールには変更が反映され <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> ます。

## <a name="formatting"></a>書式設定
 に適用できるコントロールには、同じ書式設定を適用でき <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> <xref:Microsoft.Office.Interop.Excel.Range> ます。 これには、罫線、フォント、番号形式、スタイルが含まれます。

## <a name="events"></a>イベント
 コントロールで使用できるイベント <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> は次のとおりです。

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.SelectionChange>

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [方法: ワークシートに XMLMappedRange コントロールを追加する](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [方法: Visual Studio 内のワークシートにスキーマをマップする](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
