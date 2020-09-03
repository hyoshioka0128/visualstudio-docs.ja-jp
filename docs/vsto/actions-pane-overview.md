---
title: 操作ウィンドウの概要
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], about actions panes
- actions panes [Office development in Visual Studio]
- smart documents [Office development in Visual Studio]
- user controls [Office development in Visual Studio], actions panes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 82bf3ac9515effaa1053a011085849f0afea67f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72986313"
---
# <a name="actions-pane-overview"></a>操作ウィンドウの概要
  操作ウィンドウは、特定の Microsoft Office Word 文書または Microsoft Office Excel ブックに添付された、カスタマイズ可能な **ドキュメントアクション** 作業ウィンドウです。 操作ウィンドウは、Office 作業ウィンドウ内で、Excel の [ **XML ソース** ] 作業ウィンドウや Word の [ **スタイルと書式設定** ] 作業ウィンドウなどの他の組み込み作業ウィンドウと共にホストされます。 操作ウィンドウのユーザー インターフェイスは、Windows フォーム コントロールまたは WPF コントロールを使用してデザインできます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 操作ウィンドウは、Word または Excel のドキュメント レベルのカスタマイズ内でのみ作成できます。 VSTO アドイン内に操作ウィンドウを作成することはできません。 詳細については、「 [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

> [!NOTE]
> カスタム作業ウィンドウは、操作ウィンドウとは異なります。 カスタム作業ウィンドウは、特定のドキュメントではなく、アプリケーションに関連付けられます。 カスタム作業ウィンドウは、一部の Microsoft Office アプリケーション向けの VSTO アドインで作成できます。 詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="display-the-actions-pane"></a>操作ウィンドウを表示する
 操作ウィンドウは、<xref:Microsoft.Office.Tools.ActionsPane> クラスによって表されます。 ドキュメント レベルのプロジェクトを作成するとき、`ThisWorkbook` クラス (Excel の場合) または `ThisDocument` クラス (Word の場合) の `ActionsPane` フィールドをプロジェクトで使用することで、このクラスのインスタンスをコードで使用できます。 操作ウィンドウを表示するには、`ActionsPane` フィールドの <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> プロパティに Windows フォーム コントロールを追加します。 `actions` という名前のコントロールを操作ウィンドウに追加するコード例を次に示します。

 [!code-csharp[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#7)]
 [!code-vb[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#7)]

 操作ウィンドウは、実行時にコントロールを明示的に追加するとすぐに表示されます。 操作ウィンドウが表示された後は、ユーザーの操作に応じてコントロールを動的に追加または削除できます。 通常は、ユーザーが初めてドキュメントを開くときに操作ウィンドウが表示されるように、操作ウィンドウを表示するコードを `ThisDocument` または `ThisWorkbook` の `Startup` イベント ハンドラーに追加します。 しかし、ドキュメント内でのユーザーの操作に応じてのみ操作ウィンドウを表示することもできます。 たとえば、ドキュメント上のコントロールの `Click` イベントにコードを追加できます。

### <a name="add-multiple-controls-to-the-actions-pane"></a>操作ウィンドウに複数のコントロールを追加する
 操作ウィンドウに複数のコントロールを追加する場合は、コントロールをユーザーコントロールにグループ化してから、プロパティにユーザーコントロールを追加する必要があり <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> ます。 このプロセスには、次の手順が含まれます。

1. 操作ウィンドウ **コントロール** または **ユーザーコントロール** 項目をプロジェクトに追加して、操作ウィンドウのユーザーインターフェイス (UI) を作成します。 これらのアイテムのどちらにも、カスタム Windows フォーム <xref:System.Windows.Forms.UserControl> クラスが含まれています。 **操作ウィンドウコントロール**と**ユーザーコントロール**の項目は同等です。唯一の違いは、その名前です。

2. デザイナーを使用するか、またはコードを記述して、Windows フォーム コントロールを <xref:System.Windows.Forms.UserControl> に追加します。

   > [!NOTE]
   > また、WPF の <xref:System.Windows.Controls.UserControl> を Windows フォーム <xref:System.Windows.Forms.UserControl> に追加することにより、WPF コントロールを操作ウィンドウに追加することもできます。 詳細については、「 [Office ソリューションでの WPF コントロールの使用](../vsto/using-wpf-controls-in-office-solutions.md)」を参照してください。

3. カスタム ユーザー コントロールのインスタンスを、プロジェクトの `ThisWorkbook` クラス (Excel の場合) または `ThisDocument` クラス (Word の場合) の `ActionsPane` フィールドに含まれるコントロールに追加します。

   このプロセスの詳細を示す例については、「 [方法: Word 文書または Excel ブックに操作ウィンドウを追加](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)する」を参照してください。

## <a name="hide-the-actions-pane"></a>操作ウィンドウを非表示にする
 <xref:Microsoft.Office.Tools.ActionsPane> クラスには <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> メソッドと <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> プロパティがありますが、<xref:Microsoft.Office.Tools.ActionsPane> クラス自体のメンバーを使用して、ユーザー インターフェイスから操作ウィンドウを削除することはできません。 メソッドを呼び出す <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> か、 <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> プロパティを **false** に設定すると、操作ウィンドウ上のコントロールのみが非表示になり、作業ウィンドウは非表示になりません。

 ソリューションの作業ウィンドウを非表示にするには、いくつかの方法があります。

- Word の場合は、[ <xref:Microsoft.Office.Interop.Word.TaskPane.Visible%2A> <xref:Microsoft.Office.Interop.Word.TaskPane> ドキュメントアクション] 作業ウィンドウを表すオブジェクトのプロパティを **false**に設定します。 次のコード例は、プロジェクトの `ThisDocument` クラスから実行することを前提としています。

     [!code-csharp[Trin_VstcoreActionsPaneWord#34](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#34)]
     [!code-vb[Trin_VstcoreActionsPaneWord#34](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#34)]

- Excel の場合は、 <xref:Microsoft.Office.Interop.Excel._Application.DisplayDocumentActionTaskPane%2A> オブジェクトのプロパティを <xref:Microsoft.Office.Tools.Excel.Workbook.Application%2A> **false**に設定します。 次のコード例は、プロジェクトの `ThisWorkbook` クラスから実行することを前提としています。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#11)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#11)]

- Word または Excel の場合は、 <xref:Microsoft.Office.Core.CommandBar.Visible%2A> 作業ウィンドウを表すコマンドバーのプロパティを **false**に設定することもできます。 次のコード例は、プロジェクトの `ThisDocument` クラスまたは `ThisWorkbook` から実行することを前提としています。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#9)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#9)]

### <a name="clear-the-actions-pane-when-the-document-is-opened"></a>ドキュメントを開いたときに操作ウィンドウをクリアする
 操作ウィンドウが表示されているときにユーザーがドキュメントを保存すると、[操作] ウィンドウにコントロールが表示されているかどうかにかかわらず、ドキュメントが開かれるたびに操作ウィンドウが表示されます。 それをいつ表示するかを制御するには、`ThisDocument` または `ThisWorkbook` の `Startup` イベント ハンドラーで `ActionsPane` フィールドの <xref:Microsoft.Office.Tools.ActionsPane.Clear%2A> メソッドを呼び出し、ドキュメントを開いた時点で操作ウィンドウが表示されないようにします。

### <a name="determine-when-the-actions-pane-is-closed"></a>操作ウィンドウが閉じられたことを確認する
 操作ウィンドウが閉じられたときに発生するイベントはありません。 <xref:Microsoft.Office.Tools.ActionsPane> クラスには <xref:Microsoft.Office.Tools.ActionsPane.VisibleChanged> イベントがありますが、このイベントは、エンド ユーザーによって操作ウィンドウが閉じられたときには発生しません。 代わりに、このイベントは、操作ウィンドウのコントロールがメソッドを呼び出す <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> か、プロパティを false に設定することによって非表示にされたときに発生し <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> ます。 **false**

 ユーザーは、操作ウィンドウを閉じたときに、アプリケーションのユーザーインターフェイス (UI) で次のいずれかの手順を実行することによって、もう一度表示できます。

##### <a name="to-display-the-actions-pane-by-using-the-ui-of-word-or-excel"></a>Word または Excel の UI を使用して操作ウィンドウを表示するには

1. リボンの [ **表示** ] タブをクリックします。

2. [ **表示/非** 表示] グループで、[ **ドキュメントアクション** ] トグルボタンをクリックします。

## <a name="program-actions-pane-events"></a>プログラム操作ウィンドウのイベント
 操作ウィンドウに複数のユーザー コントロールを追加し、ドキュメント上のイベントに応答するコードを作成して、ユーザー コントロールを表示したり非表示にしたりすることができます。 XML スキーマ要素をドキュメントにマップした場合は、XML 要素の 1 つにカーソルが置かれた時点で、操作ウィンドウに特定のユーザー コントロールを表示するようにできます。 詳細については、「 [方法: Visual studio 内で Word 文書にスキーマをマップ](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md) する」および「 [方法: visual studio 内のワークシートにスキーマをマップ](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)する」を参照してください。

 また、ホスト コントロール、アプリケーション、またはドキュメント イベントなど、任意のオブジェクトのイベントに応答するコードを作成することもできます。 詳細については、「 [チュートリアル: NamedRange コントロールのイベントに対してプログラムを実行する](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)」を参照してください。

## <a name="bind-data-to-controls-on-the-actions-pane"></a>操作ウィンドウのコントロールにデータをバインドする
 操作ウィンドウのコントロールは、Windows フォームのコントロールと同じデータ バインディング機能を備えています。 データセット、型指定されたデータセット、XML などのデータ ソースに、コントロールをバインドできます。 詳細については、「 [データバインディングと Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)」を参照してください。

 操作ウィンドウのコントロールとドキュメントのコントロールは、同じデータセットにバインドできます。 たとえば、操作ウィンドウのコントロールとワークシートのコントロール間でマスター/詳細関係を作成できます。 詳細については、「 [チュートリアル: Excel の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)」を参照してください。

## <a name="validate-data-in-actions-pane-controls"></a>操作ウィンドウコントロールでのデータの検証
 操作ウィンドウ上のコントロールの <xref:System.Windows.Forms.Control.Validating> イベント ハンドラーでメッセージ ボックスを表示する場合、フォーカスがコントロールからメッセージ ボックスに移った時点で 2 度目のイベントが発生することがあります。 この問題を回避するには、<xref:System.Windows.Forms.ErrorProvider> コントロールを使用して検証エラー メッセージを表示するようにします。

## <a name="user-control-stacking-order"></a>ユーザーコントロールの積み重ね順
 複数のユーザー コントロールを使用している場合は、垂直方向または水平方向のどちらにドッキングされるかにかかわらず、操作ウィンドウにユーザー コントロールを正しく積み重ねるコードを作成できます。 操作ウィンドウにユーザー コントロールを積み重ねる順序は、<xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> プロパティの <xref:Microsoft.Office.Tools.StackStyle> 列挙体を使用して設定できます。 詳細については、「 [方法: 操作ウィンドウのコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)」を参照してください。

 <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> プロパティでは、次の <xref:Microsoft.Office.Tools.StackStyle> 列挙値を使用できます。

|積み重ねのスタイル|定義|
|--------------------|----------------|
|FromBottom|操作ウィンドウの下から積み重ねます。|
|左に移動|操作ウィンドウの左から積み重ねます。|
|FromRight|操作ウィンドウの右から積み重ねます。|
|FromTop|操作ウィンドウの上から積み重ねます。|
|なし|積み重ね順を定義しません。順序は開発者が制御します。|

 次のコードでは、操作ウィンドウの上からユーザー コントロールをスタックするように <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> プロパティを設定します。

 [!code-csharp[Trin_VstcoreActionsPaneExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#10)]
 [!code-vb[Trin_VstcoreActionsPaneExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#10)]

## <a name="anchor-controls"></a>アンカーコントロール
 ユーザーが実行時に操作ウィンドウのサイズを変更した場合に、操作ウィンドウと一緒にコントロールのサイズも変更されるように設定できます。 Windows フォーム コントロールの <xref:System.Windows.Forms.Control.Anchor%2A> プロパティを使用すると、コントロールを操作ウィンドウに固定できます。 同じように、Windows フォーム コントロールをユーザー コントロールに固定することもできます。 詳細については、「 [方法: Windows フォームのコントロールを固定する](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms)」を参照してください。

## <a name="resize-the-actions-pane"></a>操作ウィンドウのサイズを変更する
 <xref:Microsoft.Office.Tools.ActionsPane> は作業ウィンドウに埋め込まれているため、<xref:Microsoft.Office.Tools.ActionsPane> のサイズを直接変更することはできません。 ただし、作業ウィンドウを表す <xref:Microsoft.Office.Core.CommandBar> の <xref:Microsoft.Office.Core.CommandBar.Width%2A> プロパティを設定すると、プログラムによって作業ウィンドウの幅を変更できます。 作業ウィンドウの高さは、作業ウィンドウが水平にドッキングされている場合、または浮動している場合に変更できます。

 ユーザーがニーズに最も合った作業ウィンドウのサイズを選択できるようにするため、プログラムによって作業ウィンドウのサイズを変更することはお勧めしません。 ただし、作業ウィンドウの幅を変更する必要がある場合には、次のコードを使用してこのタスクを実現できます。

 [!code-csharp[Trin_VstcoreActionsPaneWord#102](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#102)]
 [!code-vb[Trin_VstcoreActionsPaneWord#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#102)]

## <a name="reposition-the-actions-pane"></a>操作ウィンドウの位置を変更する
 <xref:Microsoft.Office.Tools.ActionsPane> は作業ウィンドウに埋め込まれているため、その位置を直接変更することはできません。 ただし、作業ウィンドウを表す <xref:Microsoft.Office.Core.CommandBar> の <xref:Microsoft.Office.Core.CommandBar.Position%2A> プロパティを設定すると、プログラムによって作業ウィンドウを移動できます。

 ユーザーは、必要に応じて画面上の作業ウィンドウの位置を選択できる必要があるため、プログラムで作業ウィンドウを再配置することは推奨されません。 ただし、作業ウィンドウを特定の位置に移動する必要がある場合は、次のコードを使用してこのタスクを実現できます。

 [!code-csharp[Trin_VstcoreActionsPaneWord#100](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#100)]
 [!code-vb[Trin_VstcoreActionsPaneWord#100](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#100)]

> [!NOTE]
> エンド ユーザーは、作業ウィンドウの位置を手動でいつでも変更できます。 プログラムで指定した位置に作業ウィンドウを常にドッキングしておくことはできません。 ただし、向きの変更を確認し、操作ウィンドウ上のコントロールが正しい方向で積み重ねられるようにすることは可能です。 詳細については、「 [方法: 操作ウィンドウのコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)」を参照してください。

 <xref:Microsoft.Office.Tools.ActionsPane.Top%2A> <xref:Microsoft.Office.Tools.ActionsPane.Left%2A> <xref:Microsoft.Office.Tools.ActionsPane> <xref:Microsoft.Office.Tools.ActionsPane> オブジェクトが作業ウィンドウに埋め込まれているため、のプロパティおよびプロパティを設定しても、その位置は変更されません。

 作業ウィンドウがドッキングされていない場合、作業ウィンドウを表す <xref:Microsoft.Office.Core.CommandBar> の <xref:Microsoft.Office.Core.CommandBar.Top%2A> プロパティと <xref:Microsoft.Office.Core.CommandBar.Left%2A> プロパティを設定できます。 次のコードでは、ドッキングが解除された作業ウィンドウをドキュメントの左上隅に移動します。

 [!code-csharp[Trin_VstcoreActionsPaneWord#101](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#101)]
 [!code-vb[Trin_VstcoreActionsPaneWord#101](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#101)]

## <a name="see-also"></a>関連項目
- [Office ソリューションでの WPF コントロールの使用](../vsto/using-wpf-controls-in-office-solutions.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)
- [チュートリアル: Excel の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)
- [方法: 操作ウィンドウのコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
