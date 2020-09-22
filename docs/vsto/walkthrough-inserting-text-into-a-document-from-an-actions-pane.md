---
title: 'チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 61e71f31ce887c7e1ea9ec57b0aa3f24a45be364
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842276"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する
  このチュートリアルでは、Microsoft Office Word 文書に操作ウィンドウを作成する方法について説明します。 操作ウィンドウには、入力を収集し、そのテキストをドキュメントに送信する2つのコントロールが含まれています。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 操作ウィンドウコントロールの Windows フォームコントロールを使用して、インターフェイスをデザインします。

- アプリケーションを開いたときに操作ウィンドウを表示します。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトの作成
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **[基本的な操作] ウィンドウ**という名前の Word 文書プロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     デザイナーで新しい Word 文書が開き、 **[My Basic Actions] ウィンドウ** が **ソリューションエクスプローラー**に追加されます。

## <a name="add-text-and-bookmarks-to-the-document"></a>ドキュメントにテキストとブックマークを追加する
 操作ウィンドウは、ドキュメント内のブックマークにテキストを送信します。 ドキュメントをデザインするには、基本的なフォームを作成するためのテキストを入力します。

### <a name="to-add-text-to-your-document"></a>文書にテキストを追加するには

1. Word 文書に次のテキストを入力します。

    **2008年3月21日**

    **名前**

    **アドレス**

    **これは、Word の基本的な操作ウィンドウの例です。**

   コントロールをドキュメントに追加するには、 <xref:Microsoft.Office.Tools.Word.Bookmark> Visual Studio の **ツールボックス** からドラッグするか、Word の [ **ブックマーク** ] ダイアログボックスを使用します。

### <a name="to-add-a-bookmark-control-to-your-document"></a>ドキュメントにブックマーク コントロールを追加するには

1. **ツールボックス**の [ **Word コントロール**] タブから、 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを文書にドラッグします。

     [ **ブックマークコントロールの追加** ] ダイアログボックスが表示されます。

2. 段落記号を選択せずに単語 **名**を選択し、[ **OK]** をクリックします。

    > [!NOTE]
    > 段落記号はブックマークの外側に配置する必要があります。 ドキュメントに段落記号が表示されていない場合は、[ **ツール** ] メニューの [ **Microsoft Office Word ツール** ] をポイントし、[ **オプション**] をクリックします。 [**表示**] タブをクリックし、[**オプション**] ダイアログボックスの [**書式設定**] セクションで [**段落記号**] チェックボックスをオンにします。

3. [**プロパティ**] ウィンドウで、 **Bookmark1**の**name**プロパティを**showname**に変更します。

4. 段落記号を選択せずに、[ **住所**] を選択します。

5. リボンの [ **挿入** ] タブの [ **リンク** ] グループで、[ **ブックマーク**] をクリックします。

6. [**ブックマーク**] ダイアログボックスで、[**ブックマーク名**] ボックスに「 **showaddress** 」と入力し、[**追加**] をクリックします。

## <a name="add-controls-to-the-actions-pane"></a>[操作] ウィンドウにコントロールを追加する
 操作ウィンドウインターフェイスをデザインするには、操作ウィンドウコントロールをプロジェクトに追加し、[操作] ウィンドウコントロールに Windows フォームコントロールを追加します。

### <a name="to-add-an-actions-pane-control"></a>操作ウィンドウコントロールを追加するには

1. **ソリューションエクスプローラー**で **[My Basic Actions] ウィンドウ**プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで、[ **操作ウィンドウコントロール**] をクリックし、コントロールに **InsertTextControl** という名前を指定して、[ **追加**] をクリックします。

#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>操作ウィンドウコントロールに Windows フォームコントロールを追加するには

1. 操作ウィンドウコントロールがデザイナーに表示されていない場合は、[ **InsertTextControl**] をダブルクリックします。

2. [**ツールボックス**] の [**コモンコントロール**] タブから、[操作] ウィンドウコントロールに [**ラベル**] コントロールをドラッグします。

3. ラベルコントロールの **Text** プロパティを **Name**に変更します。

4. [操作] ウィンドウコントロールに **テキストボックス** コントロールを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**getName**|
    |**[サイズ]**|**130, 20**|

5. 操作ウィンドウコントロールに2つ目の **ラベル** コントロールを追加し、 **Text** プロパティを **Address**に変更します。

6. 操作ウィンドウコントロールに2つ目の **Textbox** コントロールを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**getAddress**|
    |**Return を受け入れる**|**True**|
    |**Multiline**|**True**|
    |**[サイズ]**|**130, 40**|

7. [操作] ウィンドウコントロールに **ボタン** コントロールを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**addText**|
    |**Text**|**挿入**|

## <a name="add-code-to-insert-text-into-the-document"></a>ドキュメントにテキストを挿入するコードを追加する
 [操作] ウィンドウで、テキストボックスのテキストをドキュメント内の適切なコントロールに挿入するコードを記述し <xref:Microsoft.Office.Tools.Word.Bookmark> ます。 クラスを使用して、 `Globals` 操作ウィンドウのコントロールからドキュメントのコントロールにアクセスできます。 詳細については、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>操作ウィンドウから文書内のブックマークにテキストを挿入するには

1. [ <xref:System.Windows.Forms.Control.Click> **Addtext** ] ボタンのイベントハンドラーに次のコードを追加します。

     [!code-csharp[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#8)]
     [!code-vb[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb#8)]

2. C# では、ボタンクリック用のイベントハンドラーを追加する必要があります。 このコードは、の `InsertTextControl` 呼び出し後にコンストラクターに配置でき `InitializeComponent` ます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreActionsPaneWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#9)]

## <a name="add-code-to-show-the-actions-pane"></a>操作ウィンドウを表示するコードを追加する
 操作ウィンドウを表示するには、作成したコントロールをコントロールコレクションに追加します。

### <a name="to-show-the-actions-pane"></a>操作ウィンドウを表示するには

1. クラスの [操作] ウィンドウコントロールの新しいインスタンスを作成し `ThisDocument` ます。

     [!code-csharp[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#10)]
     [!code-vb[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#10)]

2. のイベントハンドラーに次のコードを追加 <xref:Microsoft.Office.Tools.Word.Document.Startup> `ThisDocument` します。

     [!code-csharp[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#11)]
     [!code-vb[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#11)]

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、ドキュメントを開いたときに操作ウィンドウが開かれ、ボタンがクリックされたときにテキストボックスに入力したテキストがブックマークに挿入されていることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5**キーを押して、プロジェクトを実行します。

2. 操作ウィンドウが表示されていることを確認します。

3. 操作ウィンドウのテキストボックスに名前と住所を入力し、[ **挿入**] をクリックします。

## <a name="next-steps"></a>次の手順
 ここでは、次の作業を行います。

- Excel で操作ウィンドウを作成します。 詳細については、「 [方法: Excel ブックに操作ウィンドウを追加](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))する」を参照してください。

- 操作ウィンドウ上のコントロールにデータをバインドします。 詳細については、「 [チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [方法: Excel ブックに操作ウィンドウを追加する](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))
- [方法: 操作ウィンドウのコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Bookmark コントロール](../vsto/bookmark-control.md)
