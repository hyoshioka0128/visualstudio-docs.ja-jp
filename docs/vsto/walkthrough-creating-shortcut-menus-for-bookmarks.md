---
title: 'チュートリアル: ブックマークのショートカットメニューを作成する'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context menus, Word
- Bookmark control, events
- shortcut menus, Word
- menus, creating in Office applications
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9b4b412d2e9456142c1be1af388e2803634d15c0
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "91146904"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>チュートリアル: ブックマークのショートカットメニューを作成する
  このチュートリアルでは、Word のドキュメント レベルのカスタマイズを使用して <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールのショートカット メニューを作成する方法を示します。 ユーザーがブックマーク内のテキストを右クリックすると、ショートカット メニューにテキストの書式設定オプションが表示されます。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- [プロジェクトを作成](#BKMK_CreateProject)します。

- [ドキュメントにテキストとブックマークを追加](#BKMK_addtextandbookmarks)します。

- [ショートカットメニューにコマンドを追加](#BKMK_AddCmndsShortMenu)します。

- [ブックマーク内のテキストの書式を設定](#BKMK_formattextbkmk)します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]

## <a name="create-the-project"></a><a name="BKMK_CreateProject"></a> プロジェクトを作成する
 まず、Visual Studio で Word 文書プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

- "My Bookmark" という名前の **ショートカットメニュー**を持つ Word 文書プロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio では、デザイナーで新しい Word 文書が開き、 **[マイブックマーク] ショートカットメニュー** プロジェクトが **ソリューションエクスプローラー**に追加されます。

## <a name="add-text-and-bookmarks-to-the-document"></a><a name="BKMK_addtextandbookmarks"></a> ドキュメントにテキストとブックマークを追加する
 文書にテキストを追加し、部分的に重なった 2 つのブックマークを追加します。

### <a name="to-add-text-to-your-document"></a>文書にテキストを追加するには

- プロジェクトのデザイナーで表示されているドキュメントに次のテキストを入力します。

     **This is an example of creating a shortcut menu when you right-click the text in a bookmark.**

### <a name="to-add-a-bookmark-control-to-your-document"></a>ドキュメントにブックマーク コントロールを追加するには

1. [ **ツールボックス**] の [ **Word コントロール** ] タブから、 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを文書にドラッグします。

    [ **ブックマークコントロールの追加** ] ダイアログボックスが表示されます。

2. "テキストを右クリックしてショートカットメニューを作成する" という語を選択し、[ **OK**] をクリックします。

    `bookmark1` がドキュメントに追加されます。

3. <xref:Microsoft.Office.Tools.Word.Bookmark>"ブックマーク内のテキストを右クリック" という単語に別のコントロールを追加します。

    `bookmark2` がドキュメントに追加されます。

   > [!NOTE]
   > 「テキストを右クリック」という言葉は、との両方にあり `bookmark1` `bookmark2` ます。

   デザイン時に文書にブックマークを追加すると、<xref:Microsoft.Office.Tools.Word.Bookmark> コントロールが作成されます。 ブックマークの複数のイベントに対してプログラミングを行うことができます。 ブックマークの <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick> イベントにコードを作成することで、ユーザーがブックマーク内のテキストを右クリックしたときにショートカット メニューを表示できます。

## <a name="add-commands-to-a-shortcut-menu"></a><a name="BKMK_AddCmndsShortMenu"></a> ショートカットメニューにコマンドを追加する
 ドキュメントを右クリックすると表示されるショートカット メニューにボタンを追加します。

### <a name="to-add-commands-to-a-shortcut-menu"></a>ショートカット メニューにコマンドを追加するには

1. **リボン XML**項目をプロジェクトに追加します。 詳細については、「 [方法: リボンのカスタマイズを開始](../vsto/how-to-get-started-customizing-the-ribbon.md)する」を参照してください。

2. **ソリューションエクスプローラー**で、 **ThisDocument.cs**または**ThisDocument**を選択します。

3. メニューバーで、[コードの**表示**] を選択し  >  **Code**ます。

     コードエディターで **ThisDocument** クラスファイルが開きます。

4. **ThisDocument**クラスに次のコードを追加します。 このコードは、CreateRibbonExtensibilityObject メソッドをオーバーライドし、Office アプリケーションにリボン XML クラスを返します。

     [!code-csharp[Trin_Word_Document_Menus#1](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#1)]
     [!code-vb[Trin_Word_Document_Menus#1](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#1)]

5. **[ソリューション エクスプローラー]** でリボン XML ファイルを選択します。 既定では、リボン XML ファイルには Ribbon1.xml という名前が付けられます。

6. メニューバーで、[コードの**表示**] を選択し  >  **Code**ます。

     コード エディターでリボン XML ファイルが開きます。

7. コード エディターを使用して、リボン XML ファイルの内容を次のコードに置き換えます。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui" onLoad="Ribbon_Load">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="BoldButton" label="Bold" onAction="ButtonClick"
               getVisible="GetVisible" />
          <button id="ItalicButton" label="Italic" onAction="ButtonClick"
              getVisible="GetVisible"/>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

     このコードでは、ドキュメントを右クリックすると表示されるショートカット メニューに 2 つのボタンが追加されます。

8. **ソリューションエクスプローラー**で、を右クリック `ThisDocument` し、[コードの**表示**] をクリックします。

9. 次の変数とブックマーク変数をクラス レベルで宣言します。

     [!code-csharp[Trin_Word_Document_Menus#2](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#2)]
     [!code-vb[Trin_Word_Document_Menus#2](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#2)]

10. **ソリューションエクスプローラー**で、リボンコードファイルを選択します。 既定では、リボンコードファイルには **Ribbon1.cs** または **ribbon1.vb**という名前が付けられます。

11. メニューバーで、[コードの**表示**] を選択し  >  **Code**ます。

     コード エディターでリボン コード ファイルが開きます。

12. リボン コード ファイルで、次のメソッドを追加します。 これは、ドキュメントのショートカット メニューに追加した 2 つのボタンのコールバック メソッドです。 このメソッドでは、これらのボタンがショートカット メニューに表示されるかどうかが決定されます。 [太字] ボタンおよび [斜体] ボタンは、ブックマーク内のテキストを右クリックしたときにのみ表示されます。

     [!code-csharp[Trin_Word_Document_Menus#5](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#5)]
     [!code-vb[Trin_Word_Document_Menus#5](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#5)]

## <a name="format-the-text-in-the-bookmark"></a><a name="BKMK_formattextbkmk"></a> ブックマーク内のテキストの書式を設定する

### <a name="to-format-the-text-in-the-bookmark"></a>ブックマーク内のテキストに書式を設定するには

1. リボン コード ファイルで、ブックマークに書式を適用するための `ButtonClick` イベント ハンドラーを追加します。

     [!code-csharp[Trin_Word_Document_Menus#6](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#6)]
     [!code-vb[Trin_Word_Document_Menus#6](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#6)]

2. **ソリューションエクスプローラー**には、 **ThisDocument.cs** または **ThisDocument**を選択します。

3. メニューバーで、[コードの**表示**] を選択し  >  **Code**ます。

     コードエディターで **ThisDocument** クラスファイルが開きます。

4. **ThisDocument**クラスに次のコードを追加します。

     [!code-csharp[Trin_Word_Document_Menus#3](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#3)]
     [!code-vb[Trin_Word_Document_Menus#3](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#3)]

    > [!NOTE]
    > ブックマークが部分的に重なっている場合を処理するためのコードを作成する必要があります。 これを行わないと、既定でコードは選択範囲内にあるすべてのブックマークについて呼び出されます。

5. C# では、次に示すように、ブックマーク コントロールのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_Word_Document_Menus#4](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#4)]

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、ブックマーク内のテキストを右クリックしたときにショートカット メニューに太字と斜体のメニュー項目が表示され、テキストが正しく書式設定されることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5**キーを押して、プロジェクトを実行します。

2. 最初のブックマークを右クリックし、[ **太字**] をクリックします。

3. `bookmark1` 内のすべてのテキストが太字になることを確認します。

4. ブックマークが重なっているテキストを右クリックし、[ **斜体**] をクリックします。

5. `bookmark2` ではすべてのテキストが斜体になるが、`bookmark1` では `bookmark2` と重なっている部分のテキストしか斜体にならないことを確認します。

## <a name="next-steps"></a>次のステップ
 ここでは、次の作業を行います。

- Excel 内のホスト コントロールのイベントに応答するコードを作成します。 詳細については、「 [チュートリアル: NamedRange コントロールのイベントに対してプログラムを実行する](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)」を参照してください。

- チェック ボックスを使用してブックマーク内の書式を変更します。 詳細については、「 [チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [Bookmark コントロール](../vsto/bookmark-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
