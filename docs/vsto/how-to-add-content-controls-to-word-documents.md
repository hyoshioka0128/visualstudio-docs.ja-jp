---
title: '方法: Word 文書にコンテンツコントロールを追加する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- DropDownListContentControl, adding to documents
- BuildingBlockGalleryContentControl, adding to documents
- partial document protection [Office development in Visual Studio]
- RichTextContentControl, adding to documents
- Word [Office development in Visual Studio], partial document protection
- content controls [Office development in Visual Studio], protecting
- PictureContentControl, adding to documents
- GroupContentControl, adding to documents
- document protection [Office development in Visual Studio]
- PlainTextContentControl, adding to documents
- content controls [Office development in Visual Studio], adding
- ComboBoxContentControl, adding to documents
- DatePickerContentControl, adding to documents
- Word [Office development in Visual Studio], restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2f15adeb801e33a134c681c206e3a5b38ccce70f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538386"
---
# <a name="how-to-add-content-controls-to-word-documents"></a>方法: Word 文書にコンテンツコントロールを追加する
  ドキュメント レベルの Word プロジェクトでは、デザイン時または実行時にプロジェクトの文書にコンテンツ コントロールを追加できます。 Word VSTO アドイン プロジェクトでは、実行時に任意の開いている文書にコンテンツ コントロールを追加できます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 このトピックでは、次のタスクについて説明します。

- [デザイン時にコンテンツコントロールを追加する](#designtime)

- [実行時にドキュメントレベルのプロジェクトにコンテンツコントロールを追加する](#runtimedoclevel)

- [実行時に VSTO アドインプロジェクトにコンテンツコントロールを追加する](#runtimeaddin)

  コンテンツコントロールの詳細については、「[コンテンツコントロール](../vsto/content-controls.md)」を参照してください。

## <a name="add-content-controls-at-design-time"></a><a name="designtime"></a>デザイン時にコンテンツコントロールを追加する
 デザイン時にドキュメント レベルのプロジェクトの文書にコンテンツ コントロールを追加する方法はいくつかあります。

- **[ツールボックス]** の **[Word コントロール]** タブからコンテンツ コントロールを追加する。

- Word でネイティブなコンテンツ コントロールを追加するのと同様に、ドキュメントにコンテンツ コントロールを追加します。

- **[データ ソース]** ウィンドウからコンテンツ コントロールを文書にドラッグする。 これは、コントロールの作成時にデータにコントロールをバインドする場合に役立ちます。 詳細については、「[方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)」および「[方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)」を参照してください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-content-control-to-a-document-by-using-the-toolbox"></a>[ツールボックス] を使用して文書にコンテンツ コントロールを追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、コンテンツ コントロールを追加する場所にカーソルを置くか、または、テキストを置換するコンテンツ コントロールを選択します。

2. **[ツールボックス]** を開き、 **[Word コントロール]** タブをクリックします。

3. 次のいずれかの方法でコントロールを追加します。

    - **[ツールボックス]** のコンテンツ コントロールをダブルクリックします。

         or

    - [**ツールボックス**] のコンテンツコントロールをクリック**し、enter キーを**押します。

         or

    - **[ツールボックス]** からコンテンツ コントロールを文書にドラッグします。 コンテンツ コントロールが、マウス ポインターの場所ではなく、ドキュメント内の現在の選択の場所で追加されます。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Word.GroupContentControl> [ツールボックス] **を使用して**を追加することはできません。 <xref:Microsoft.Office.Tools.Word.GroupContentControl> は Word で、または実行時にのみ追加できます。

> [!NOTE]
> Visual Studio では、チェック ボックス コンテンツ コントロールがツールボックスで提供されていません。 文書にチェック ボックス コンテンツ コントロールを追加するには、プログラムを使用して <xref:Microsoft.Office.Tools.Word.ContentControl> オブジェクトを作成する必要があります。 詳細については、「[コンテンツコントロール](../vsto/content-controls.md)」を参照してください。

#### <a name="to-add-a-content-control-to-a-document-in-word"></a>Word で文書にコンテンツ コントロールを追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、コンテンツ コントロールを追加する場所にカーソルを置くか、または、テキストを置換するコンテンツ コントロールを選択します。

2. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: リボンに [開発者] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

3. **[コントロール]** グループで、追加するコンテンツ コントロールのアイコンをクリックします。

## <a name="add-content-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>実行時にドキュメントレベルのプロジェクトにコンテンツコントロールを追加する
 プロジェクトで <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> クラスの `ThisDocument` プロパティのメソッドを使用して、実行時にプログラムによりドキュメントにコンテンツ コントロールを追加できます。 各メソッドには 3 つのオーバーロードがあります。それらを使用することにより、次のようにコンテンツ コントロールを追加できます。

- 現在の選択項目でコントロールを追加します。

- 指定された範囲にコントロールを追加します。

- 文書内のネイティブなコンテンツ コントロールに基づいたコントロールを追加します。

  動的に作成されたコンテンツ コントロールは、文書を閉じる際に文書に残りません。 ただし、ネイティブなコンテンツ コントロールは、文書内に残ります。 文書を次回開くときに、ネイティブのコンテンツ コントロールに基づくコンテンツ コントロールを再作成できます。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

> [!NOTE]
> Word 2010 プロジェクトで文書にチェック ボックス コンテンツ コントロールを追加するには、 <xref:Microsoft.Office.Tools.Word.ContentControl> オブジェクトを作成する必要があります。 詳細については、「[コンテンツコントロール](../vsto/content-controls.md)」を参照してください。

### <a name="to-add-a-content-control-at-the-current-selection"></a>現在の選択項目でコンテンツ コントロールを追加するには

1. という <xref:Microsoft.Office.Tools.Word.ControlCollection> 名前のメソッドを使用し `Add` \<*control class*> ます (ここで、 *control class*は、などの追加するコンテンツコントロールのクラス名です)。このメソッドには、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 新しいコントロールの名前を表す1つのパラメーターがあります。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `AddRichTextControlAtSelection` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     [!code-csharp[Trin_ContentControlReference#700](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#700)]
     [!code-vb[Trin_ContentControlReference#700](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#700)]

### <a name="to-add-a-content-control-at-a-specified-range"></a>指定された範囲にコンテンツ コントロールを追加するには

1. という <xref:Microsoft.Office.Tools.Word.ControlCollection> 名前のメソッドを使用し `Add` \<*control class*> ます (ここで、 *control class*は、などの追加するコンテンツコントロールクラスの名前で、は <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> パラメーターを持ち <xref:Microsoft.Office.Interop.Word.Range> ます)。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `AddRichTextControlAtRange` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     [!code-csharp[Trin_ContentControlReference#701](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#701)]
     [!code-vb[Trin_ContentControlReference#701](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#701)]

### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>ネイティブなコンテンツ コントロールに基づいたコンテンツ コントロールを追加するには

1. という <xref:Microsoft.Office.Tools.Word.ControlCollection> 名前のメソッドを使用し `Add` \<*control class*> ます (ここで、 *control class*は、などの追加するコンテンツコントロールクラスの名前で、は <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> パラメーターを持ち `Microsoft.Office.Interop.Word.ContentControl` ます)。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して、ドキュメント内にあるすべてのネイティブなリッチ テキスト コントロールについて新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を作成しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `CreateRichTextControlsFromNativeControls` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     [!code-csharp[Trin_ContentControlReference#702](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#702)]
     [!code-vb[Trin_ContentControlReference#702](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#702)]

## <a name="add-content-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>実行時に VSTO アドインプロジェクトにコンテンツコントロールを追加する
 コンテンツ フォーム コントロールは、実行時に VSTO アドインを使用して任意の開いているドキュメントに追加できます。 そのためには、開いている文書に基づいた <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を生成し、このホスト項目の <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> プロパティのメソッドを使用します。 各メソッドには 3 つのオーバーロードがあります。それらを使用することにより、次のようにコンテンツ コントロールを追加できます。

- 現在の選択項目でコントロールを追加します。

- 指定された範囲にコントロールを追加します。

- 文書内のネイティブなコンテンツ コントロールに基づいたコントロールを追加します。

  動的に作成されたコンテンツ コントロールは、文書を閉じる際に文書に残りません。 ただし、ネイティブなコンテンツ コントロールは、文書内に残ります。 文書を次回開くときに、ネイティブのコンテンツ コントロールに基づくコンテンツ コントロールを再作成できます。 詳細については、「 [Office ドキュメントに動的コントロールを保存](../vsto/persisting-dynamic-controls-in-office-documents.md)する」を参照してください。

  VSTO アドインプロジェクトでのホスト項目の生成の詳細については、「[実行時の Vsto アドインでの Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

> [!NOTE]
> 文書にチェック ボックス コンテンツ コントロールを追加するには、 <xref:Microsoft.Office.Tools.Word.ContentControl> オブジェクトを作成する必要があります。 詳細については、「[コンテンツコントロール](../vsto/content-controls.md)」を参照してください。

### <a name="to-add-a-content-control-at-the-current-selection"></a>現在の選択項目でコンテンツ コントロールを追加するには

1. という <xref:Microsoft.Office.Tools.Word.ControlCollection> 名前のメソッドを使用し `Add` \<*control class*> ます (ここで、 *control class*は、などの追加するコンテンツコントロールのクラス名です)。このメソッドには、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 新しいコントロールの名前を表す1つのパラメーターがあります。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用してアクティブな文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `AddRichTextControlAtSelection` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     [!code-vb[Trin_WordAddInDynamicControls#1](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#1)]
     [!code-csharp[Trin_WordAddInDynamicControls#1](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#1)]

### <a name="to-add-a-content-control-at-a-specified-range"></a>指定された範囲にコンテンツ コントロールを追加するには

1. という <xref:Microsoft.Office.Tools.Word.ControlCollection> 名前のメソッドを使用し `Add` \<*control class*> ます (ここで、 *control class*は、などの追加するコンテンツコントロールクラスの名前で、は <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> パラメーターを持ち <xref:Microsoft.Office.Interop.Word.Range> ます)。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用してアクティブな文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `AddRichTextControlAtRange` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     [!code-vb[Trin_WordAddInDynamicControls#2](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#2)]
     [!code-csharp[Trin_WordAddInDynamicControls#2](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#2)]

#### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>ネイティブなコンテンツ コントロールに基づいたコンテンツ コントロールを追加するには

1. という <xref:Microsoft.Office.Tools.Word.ControlCollection> 名前のメソッドを使用し `Add` \<*control class*> ます (ここで、 *control class*は、などの追加するコンテンツコントロールクラスの名前で、は <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> パラメーターを持ち `Microsoft.Office.Interop.Word.ContentControl` ます)。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して、文書を開いた後に文書内にあるすべてのネイティブなリッチ テキスト コントロールについて、新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を作成しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスに次のコードを追加します。

     [!code-vb[Trin_WordAddInDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#3)]
     [!code-csharp[Trin_WordAddInDynamicControls#3](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#3)]

     C# の場合、 `Application_DocumentOpen` イベント ハンドラーを <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントに接続する必要もあります。

     [!code-csharp[Trin_WordAddInDynamicControls#6](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#6)]

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)
- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
