---
title: Office ドキュメントでのダイナミックコントロールの永続化
description: ソリューションにコードを追加して、ユーザーが閉じたドキュメントを再び開いたときに永続的な動的コントロールを再作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Office documents [Office development in Visual Studio, host controls
- controls [Office development in Visual Studio], persisting in the document
- Windows Forms controls [Office development in Visual Studio], persisting in the document
- documents [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], persisting in the document
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e833a480713e3c04215c03a3dc4a549c92e0f772
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938474"
---
# <a name="persist-dynamic-controls-in-office-documents"></a>Office ドキュメントでのダイナミックコントロールの永続化

実行時に追加されたコントロールは、ドキュメントまたはブックを保存するとき、および閉じるときに永続化されません。 厳密な動作は、ホスト コントロールと Windows フォーム コントロールで違いがあります。 どちらの場合も、ソリューションにコードを追加すれば、ユーザーが同じドキュメントを再び開く時点でコントロールが再作成されるようにできます。

実行時にドキュメントに追加するコントロールのことを、 *ダイナミック コントロール* といいます。 動的コントロールの詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="persist-host-controls-in-the-document"></a>ドキュメント内のホストコントロールを保持する

ドキュメントを保存してから閉じるとき、すべてのダイナミック ホスト コントロールはドキュメントから削除されます。 基になるネイティブ Office オブジェクトのみが後に残ります。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> ホスト コントロールは <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName>になります。 ネイティブ Office オブジェクトはホスト コントロールのイベントには接続されておらず、ホスト コントロールのデータ バインディング機能を持ちません。

ホスト コントロールの種類ごとに、ドキュメントに残されるネイティブ Office オブジェクトの一覧を次の表に示します。

|ホスト コントロールの種類|ネイティブ Office オブジェクトの種類|
|-----------------------|-------------------------------|
|<xref:Microsoft.Office.Tools.Excel.Chart>|<xref:Microsoft.Office.Interop.Excel.Chart>|
|<xref:Microsoft.Office.Tools.Excel.ListObject>|<xref:Microsoft.Office.Interop.Excel.ListObject>|
|<xref:Microsoft.Office.Tools.Excel.NamedRange>|<xref:Microsoft.Office.Interop.Excel.Range>|
|<xref:Microsoft.Office.Tools.Word.Bookmark>|<xref:Microsoft.Office.Interop.Word.Bookmark>|
|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.GroupContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PictureContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|<xref:Microsoft.Office.Interop.Word.ContentControl>|

### <a name="re-create-dynamic-host-controls-when-documents-are-opened"></a>ドキュメントを開いたときに動的ホストコントロールを再作成する

ユーザーがドキュメントを開くたびに、既存のネイティブ コントロールの代わりにダイナミック ホスト コントロールを再作成することができます。 ドキュメントを開いたときにこの方法でホスト コントロールを作成すれば、ユーザーが期待するとおりの動作をシミュレートできます。

Word のホストコントロール、また <xref:Microsoft.Office.Tools.Excel.NamedRange> は Excel 用またはホストコントロールを再作成するに <xref:Microsoft.Office.Tools.Excel.ListObject> は、 `Add` \<*control class*> オブジェクトまたはオブジェクトのメソッドを使用し <xref:Microsoft.Office.Tools.Excel.ControlCollection?displayProperty=fullName> <xref:Microsoft.Office.Tools.Word.ControlCollection?displayProperty=fullName> ます。 ネイティブ Office オブジェクトのパラメーターを持つメソッドを使用します。

たとえば、ドキュメントが開かれた時点で既存のネイティブ <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> から <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> ホスト コントロールを作成するには、 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddListObject%2A> メソッドを使用し、既存の <xref:Microsoft.Office.Interop.Excel.ListObject>を渡します。 これを Excel のドキュメント レベルのプロジェクトで実行する方法を、次のコード例に示します。 このコードでは、 <xref:Microsoft.Office.Tools.Excel.ListObject> クラスの <xref:Microsoft.Office.Interop.Excel.ListObject> という名前の既存の `MyListObject` に基づいてダイナミック `Sheet1` を再作成します。

[!code-csharp[Trin_ExcelWorkbookDynamicControls#6](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/Sheet1.cs#6)]
[!code-vb[Trin_ExcelWorkbookDynamicControls#6](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/Sheet1.vb#6)]

### <a name="re-create-chart"></a>グラフの再作成

ホストコントロールを再作成するには、 <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> まずネイティブのを削除して <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> から、メソッドを使用してを再作成する必要があり <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddChart%2A> ます。 既存のに `Add` \<*control class*> 基づいて新しいを作成できる方法はありません <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> 。

ネイティブのを最初に削除しない場合は <xref:Microsoft.Office.Interop.Excel.Chart> 、を再作成するときに、2つ目の重複したグラフを作成し <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> ます。

## <a name="persist-windows-forms-controls-in-documents"></a>ドキュメント内の Windows フォームコントロールを保持する

ドキュメントを保存してから終了すると、動的に作成されたすべての Windows フォーム コントロールは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってドキュメントから自動的に削除されます。 ただし、ドキュメント レベルのプロジェクトと VSTO アドイン プロジェクトでは動作が異なります。

ドキュメント レベルのカスタマイズの場合、コントロールとその基になる ActiveX ラッパー (ドキュメント上でコントロールをホストするために使用される) は、ドキュメントを次回に開いた時点で削除されます。 かつてコントロールがあったことを示すものは何も残りません。

VSTO アドインの場合、コントロールは削除されますが、ActiveX ラッパーが文書内に残ります。 ユーザーがドキュメントを次回に開くと、その ActiveX ラッパーが表示されます。 Excel では、最後にドキュメントを保存した時点で表示されていたコントロールの画像が ActiveX ラッパーに表示されます。 Word では、ActiveX ラッパーは最初は表示されませんが、ユーザーがラッパーをクリックすると、コントロールの境界を表す点線が表示されます。 ActiveX ラッパーを削除するには、いくつかの方法があります。 詳細については、「 [アドインの ActiveX ラッパーを削除する](#removingActiveX)」を参照してください。

### <a name="re-create-windows-forms-controls-when-documents-are-opened"></a>ドキュメントを開いたときに Windows フォームコントロールを再作成する

ユーザーがドキュメントを再び開いたときに、削除された Windows フォーム コントロールを再作成することができます。 これを行うには、ソリューションで次の手順を実行する必要があります。

1. ドキュメントを保存するか閉じるときに、コントロールのサイズ、場所、状態に関する情報を保管します。 ドキュメントレベルのカスタマイズでは、データをドキュメントのデータキャッシュに保存できます。 VSTO アドインでは、ドキュメント内のカスタム XML 部分にデータを保存できます。

2. ドキュメントを開いたときに発生するイベントで、コントロールを再作成します。 ドキュメントレベルのプロジェクトでは、 `Sheet` *n* `_Startup` またはイベントハンドラーでこれを行うことができ `ThisDocument_Startup` ます。 VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> または <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントのイベント ハンドラーでこの処理を実行できます。

### <a name="remove-activex-wrappers-in-an-add-in"></a><a name="removingActiveX"></a> アドインの ActiveX ラッパーを削除する

VSTO アドインを使用してドキュメントに動的な Windows フォームコントロールを追加すると、次にそのコントロールを次に開いたときに、そのコントロールの ActiveX ラッパーがドキュメントに表示されないようにすることができます。

#### <a name="remove-activex-wrappers-when-the-document-is-opened"></a>ドキュメントを開いたときに ActiveX ラッパーを削除する

すべての ActiveX ラッパーを削除するには、`GetVstoObject` メソッドを呼び出して、新しく開いたドキュメントを表す <xref:Microsoft.Office.Interop.Word.Document> または <xref:Microsoft.Office.Interop.Excel.Workbook> のためのホスト項目を生成します。 たとえば、Word 文書からすべての ActiveX ラッパーを削除するには、`GetVstoObject` メソッドを呼び出して <xref:Microsoft.Office.Interop.Word.Document> オブジェクトのためのホスト項目を生成し、そのオブジェクトを <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントのイベント ハンドラーに渡します。

この手順は、VSTO アドインがインストールされているコンピューターでのみドキュメントが開かれることがわかっている場合に便利です。 VSTO アドインをインストールしていない他のユーザーにドキュメントを渡す可能性がある場合は、代わりに、ドキュメントを閉じる前にコントロールを削除することを検討してください。

ドキュメントが開かれたときに `GetVstoObject` メソッドを呼び出す方法を次のコード例に示します。

[!code-vb[Trin_WordAddInDynamicControls#11](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#11)]
[!code-csharp[Trin_WordAddInDynamicControls#11](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#11)]

`GetVstoObject`メソッドは、主に実行時に新しいホスト項目を生成するために使用されますが、このメソッドは、特定のドキュメントに対して初めて呼び出されたときに、ドキュメントからすべての ActiveX ラッパーもクリアします。 メソッドの使用方法の詳細については `GetVstoObject` 、「 [実行時の VSTO アドインでの Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

ドキュメントを開いたときに VSTO アドインによってダイナミックコントロールが作成された場合、VSTO アドインは、 `GetVstoObject` コントロールを作成するプロセスの一部として既にメソッドを呼び出します。 このシナリオでは、ActiveX ラッパーを削除するために `GetVstoObject` メソッドに対する別個の呼び出しを追加する必要はありません。

#### <a name="remove-the-dynamic-controls-before-the-document-is-closed"></a>ドキュメントを閉じる前にダイナミックコントロールを削除する

VSTO アドインを使用して、ドキュメントを閉じる前にドキュメントから各ダイナミック コントロールを明示的に削除できます。 この手順は、VSTO アドインをインストールしていない他のユーザーに渡す可能性があるドキュメントの場合に便利です。

Word 文書を閉じるときに文書からすべての Windows フォーム コントロールを削除する方法を次のコード例に示します。

[!code-vb[Trin_WordAddInDynamicControls#10](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#10)]
[!code-csharp[Trin_WordAddInDynamicControls#10](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#10)]

## <a name="see-also"></a>関連項目

- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
