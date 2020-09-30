---
title: Office ドキュメントの Windows フォームコントロールの制限事項
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], ActiveX legacy
- ActiveX controls [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], limitations
- controls [Office development in Visual Studio], Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], unsupported properties and methods
- Toolbox [Office development in Visual Studio], unsupported controls
- user controls [Office development in Visual Studio], grouping controls
- Windows Forms controls [Office development in Visual Studio], Toolbox
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ade7da21a8d07fbd429a88303ad2be375877c1ec
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91583737"
---
# <a name="limitations-of-windows-forms-controls-on-office-documents"></a>Office ドキュメントの Windows フォームコントロールの制限事項

Microsoft Office Word 文書または Microsoft Office Excel ワークシートに追加される Windows フォームコントロール Windows フォームと、Windows フォームに追加されるコントロールにはいくつかの違いがあります。 たとえば、ドキュメントにコントロールを追加した場合、 <xref:Microsoft.Office.Tools.Word.Controls.Button> 、、などの <xref:System.Windows.Forms.Control.Dock> プロパティ <xref:System.Windows.Forms.Control.Anchor> は、 <xref:System.Windows.Forms.Control.TabIndex> 予期したとおりに動作しません。

これらの違いの多くは、Windows フォームコントロールがドキュメントでホストされている方法によって発生します。 Windows フォームコントロールがドキュメントに追加されると、は [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ActiveX コントロールを埋め込み、ドキュメント内の Windows フォームコントロールをホストします。 Windows フォームコントロールがドキュメントに直接埋め込まれていません。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="limitations-of-methods-and-properties-of-windows-forms-controls"></a>Windows フォームコントロールのメソッドとプロパティの制限事項

Windows フォームコントロールのメソッドとプロパティには、Windows フォームの場合と同じように動作しないものがあります。そのため、これらを使用しないことをお勧めします。 たとえば、やなどのプロパティを設定することは、 <xref:System.Windows.Forms.Control.Dock> <xref:System.Windows.Forms.Control.Anchor> ドキュメントではなく、コンテナー ActiveX コントロールに対するコントロールの位置にのみ影響します。 Word および Excel の Windows フォームコントロールのサポートされていないメソッドとプロパティの一覧を次に示します。

- Excel コントロールのサポートされていないプロパティ:

  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>

- Word コントロールのサポートされていないメソッドとプロパティ:

  - <xref:System.Windows.Forms.Control.Hide%2A>
  - <xref:System.Windows.Forms.Control.Show%2A>
  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>
  - <xref:System.Windows.Forms.Control.Visible>

<xref:System.Windows.Forms.Control.Left>また、 <xref:System.Windows.Forms.Control.Top> Word 文書で行内にある Windows フォームコントロールのプロパティまたはプロパティを設定することもできません。 Windows フォームコントロールは、次の場合にテキストと共に行に追加されます。

- プログラムを使用して、コントロールを Word 文書に追加し、場所の範囲を指定するメソッドを使用します。

- デザイン時に Word 文書に Windows フォームコントロールを追加します。 これは、デザイナーでコントロールを変更することによって変更できます。

## <a name="differences-in-windows-forms-controls-on-office-documents"></a>Office ドキュメントの Windows フォームコントロールの相違点

Windows フォームコントロールは、通常、Windows フォームの場合と同じように Office ドキュメントで動作しますが、いくつかの違いがあります。 次の表では、Office ドキュメントの Windows フォームコントロールに存在する違いについて説明します。

|機能|相違点|
|-------------------|----------------|
|コントロールタブの順序|Excel ワークシートまたは Word 文書に配置されているコントロールを tab キーで移動することはできません。|
|コントロールのグループ化|コントロールを使用し <xref:System.Windows.Forms.GroupBox> て Office ドキュメントに他のコントロールを含めることはできません。 ドキュメントに複数のオプションボタンを直接追加する場合、オプションボタンは同時に指定できません。 オプションボタンが相互に排他的になるようにコードを記述することができます。ただし、ユーザーコントロールにオプションボタンを追加してから、ドキュメントにユーザーコントロールを追加することをお勧めします。 詳細については、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の「コントロールのサンプルまたは Excel コントロールのサンプル」を参照してください。|
|コントロール型|ドキュメントで使用される Windows フォームコントロールは、によって提供されるクラスでラップされ [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。これにより、Excel ワークシートまたは Word 文書に固有の追加機能を制御できます。 たとえば、Excel ワークシートに **ボタン** コントロールがある場合は、 <xref:Microsoft.Office.Tools.Excel.Controls.Button> オブジェクトを <xref:System.Windows.Forms.Button> 参照またはキャストするときではなく、型をとして指定する必要があります。|
|制御位置とサイズ|コントロールのサイズと位置は、コンテナー ActiveX コントロールの一部であるプロパティによって決定されます。 ActiveX コントロールのプロパティは、Windows フォームコントロールの同等のプロパティとは異なる値を受け取ります。 コントロールの、、、またはの各プロパティを設定すると、 `Top` `Left` `Height` `Width` ピクセルではなくポイント単位で測定されます。|
|Word 文書のコントロール位置|フローベースのレイアウトにコントロールを追加する場合は、コンテンツが変更されたときにコントロールがコンテンツと共にフローすることに注意してください。 コントロールがテキストと共に Word 文書に追加されるため、 **ツールボックス** からドラッグしたときにコントロールを段落に固定することはできません。 コントロールをダブルクリックするなど、別のメソッドを使用してコントロールを追加すると、画像の挿入用に設定した Word オプションに従ってコントロールが挿入されます。<br /><br /> テキストが行内に `Left` `Top` あるコントロールのプロパティまたはプロパティを設定することはできません。<br /><br /> ヘッダー、フッター、またはサブドキュメント内にコントロールを配置することはできません。|
|コントロールイベント|コントロールを選択すると、次の順序でイベントが発生します。<br /><br /> 1.  `Enter`<br />3.  `GotFocus`<br /><br /> コントロールが選択解除されると、次の順序でイベントが発生します。<br /><br /> 1.  `Leave`<br />3.  `Validating`<br />番.  `Validated`<br />4/4.  `LostFocus`|
|コントロールのスケーリング|ドキュメントのズーム設定を100% 以外の値に変更すると、コントロールは無効になりますが、ドキュメントで拡大縮小するように見えます。 たとえば、ドキュメントのサイズが130% に達したときにボタンをクリックすると、zoom が100% に設定されるまでコントロールが無効になっていることを示すメッセージが表示されます。 ズームを100% に変更すると、コントロールが正しく機能します。|
|コントロールプロパティの値|Windows フォーム上のコントロールのプロパティは、整数値に設定されますが、Word 文書のコントロールの場合は、1つのに設定されます。 Excel では、コントロールのプロパティ値が double に設定されています。 `Height` `Width` ワークシート上のコントロールのプロパティとプロパティがワークシートまたは画面のサイズを超える場合、値は切り捨てられます。|
|コントロールのサイズ変更|8つのサイズ変更ハンドルのいずれかを使用してドキュメントのコントロールのサイズを変更した場合、コントロールが再確認されるまで、新しいコントロールの寸法は [ **プロパティ** ] ウィンドウに反映されません。|
|コントロールの動作|ワークシートウィンドウが分割されると、Excel ワークシート上のコントロールが予期しない動作をする場合があります。 たとえば、ワークシート上のへのアクセスは、 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> いずれかのウィンドウでしか使用できない場合があります。|
|コントロールの名前付け|予約語を使用してコントロールの名前を指定することはできません。 たとえば、を <xref:Microsoft.Office.Tools.Excel.Controls.Button> ワークシートに追加し、名前を **System**に変更すると、プロジェクトのビルド時にエラーが発生します。|
|プログラムによるコントロールの追加|実行時にコントロールのコンストラクターを使用してドキュメントにコントロールを追加しないでください。 代わりに、によって提供されるヘルパーメソッドを使用し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ControlExtensions.AddButton%2A> ワークシートにボタンを追加するには、メソッドを使用します。 これらのヘルパーメソッドでサポートされていないコントロールを追加する場合は、メソッドを使用でき `AddControl` ます。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。|
|コントロールのコピー|Windows フォームコントロールをコピーして、実行時にドキュメントに貼り付けると、空のコンテナー ActiveX コントロールがドキュメントに貼り付けられます。 Windows フォームコントロールは新しい位置に表示されません。元のコントロールの背後にあるコードは、コンテナー ActiveX コントロールにコピーされません。|

## <a name="limitations-in-document-level-projects"></a>ドキュメントレベルのプロジェクトでの制限事項

ドキュメントレベルのプロジェクトに固有の Windows フォームコントロールの使用には、いくつかの制限があります。

### <a name="control-support-at-design-time"></a>デザイン時のコントロールのサポート

Visual Studio デザイナーで Excel ワークシートまたは Word 文書を開いたときに、特定の Windows フォームコントロールが **ツールボックス** から削除されます。 これは、技術的な制限、または Word または Excel 内で機能が既に使用可能であるためです。 Excel および Word プロジェクトは、ドキュメントにフォーカスがあるときに **ツールボックス** に表示されるすべての Windows フォームコントロールとその他のコンポーネントをサポートします。また、ワークシートまたはドキュメントにサードパーティ製のコントロールを追加することもできます。

> [!NOTE]
> ドキュメントが保護されている場合、すべてのコントロールが **ツールボックス** から削除されます。 ドキュメントの保護の詳細については、「ドキュメント [レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)」を参照してください。

> [!NOTE]
> <xref:System.Runtime.InteropServices.ComVisibleAttribute>Office ソリューションで使用するには、サードパーティのコントロールで属性が**true**に設定されている必要があります。

**ツールボックス**では、次のコントロールとコンポーネントは使用できません。

- <xref:System.Windows.Forms.BindingNavigator>

- <xref:System.Windows.Forms.ContextMenuStrip>

- <xref:System.Windows.Forms.DataGrid>

- <xref:System.DirectoryServices.DirectoryEntry>

- <xref:System.DirectoryServices.DirectorySearcher>

- <xref:System.Windows.Forms.ErrorProvider>

- <xref:System.Diagnostics.EventLog>

- <xref:System.IO.FileSystemWatcher>

- <xref:System.Windows.Forms.FlowLayoutPanel>

- <xref:System.Windows.Forms.GroupBox>

- <xref:System.Windows.Forms.MainMenu>

- <xref:System.Windows.Forms.MenuStrip>

- <xref:System.Messaging.MessageQueue>

- <xref:System.Windows.Forms.NotifyIcon>

- <xref:System.Windows.Forms.PageSetupDialog>

- <xref:System.Windows.Forms.Panel>

- <xref:System.Diagnostics.PerformanceCounter>

- <xref:System.Windows.Forms.PrintDialog>

- <xref:System.Drawing.Printing.PrintDocument>

- <xref:System.Windows.Forms.PrintPreviewControl>

- <xref:System.Diagnostics.Process>

- <xref:System.Windows.Forms.RichTextBox>

- <xref:System.IO.Ports.SerialPort>

- <xref:System.ServiceProcess.ServiceController>

- <xref:System.Windows.Forms.SplitContainer>

- <xref:System.Windows.Forms.Splitter>

- <xref:System.Windows.Forms.StatusBar>

- <xref:System.Windows.Forms.StatusStrip>

- <xref:System.Windows.Forms.TabControl>

- <xref:System.Windows.Forms.TableLayoutPanel>

- <xref:System.Timers.Timer>

- <xref:System.Windows.Forms.Timer>

- <xref:System.Windows.Forms.ToolBar>

- <xref:System.Windows.Forms.ToolStrip>

- <xref:System.Windows.Forms.ToolStripContainer>

- <xref:System.Windows.Forms.ToolStripDropDown>

- <xref:System.Windows.Forms.ToolStripDropDownMenu>

- <xref:System.Windows.Forms.ToolStripPanel>

### <a name="support-for-legacy-activex-controls"></a>従来の ActiveX コントロールのサポート

ActiveX コントロールを含む既存の Word 文書または Excel ブックを使用するドキュメントレベルの Office プロジェクトを作成する場合、ActiveX コントロールの機能は失われません。ただし、Visual Studio 内からドキュメントに新しい ActiveX コントロールを追加することはサポートされていません。 たとえば、Word 文書に Visual Basic for Applications (VBA) マクロを実行する **コントロール** ツールボックスのボタンがある場合、Office プロジェクトでドキュメントが使用された後も、マクロは引き続き実行されます。 ただし、ActiveX コントロールと VBA マクロを削除して、Windows フォームコントロールとマネージコードに置き換えることをお勧めします。

## <a name="see-also"></a>関連項目

- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [Office ドキュメントのコントロールの Windows フォームの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [方法: Office ドキュメントに Windows フォームコントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
