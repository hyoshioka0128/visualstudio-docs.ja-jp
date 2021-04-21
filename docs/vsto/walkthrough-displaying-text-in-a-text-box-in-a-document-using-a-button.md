---
title: ボタンを使用してドキュメント内のテキストボックスにテキストを表示する
description: Microsoft Word のドキュメントレベルのカスタマイズでボタンとテキストボックスを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text boxes, displaying text in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 716d0ed0b203d55932fef4d6e3e22eabf1137ded
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824199"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-document-using-a-button"></a>チュートリアル: ボタンを使用してドキュメント内のテキストボックスにテキストを表示する
  このチュートリアルでは、Microsoft Office Word のドキュメント レベルのカスタマイズでボタンやテキスト ボックスを使用する方法を示します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- デザイン時にドキュメント レベルのプロジェクトで Word 文書にコントロールを追加する。

- ボタンがクリックされたときにテキスト ボックスにデータを読み込む。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>プロジェクトを作成する
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **[マイ Word] ボタン** という名前の word 文書プロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio では、デザイナーで新しい Word 文書が開き、 **[マイ Word] ボタン** プロジェクトが **ソリューションエクスプローラー** に追加されます。

## <a name="add-controls-to-the-word-document"></a>Word 文書にコントロールを追加する
 ユーザー インターフェイス コントロールは、Word 文書上のボタンとテキスト ボックスで構成されます。

### <a name="to-add-a-button-and-a-text-box"></a>ボタンとテキスト ボックスを追加するには

1. Visual Studio デザイナーで文書が開いていることを確認します。

2. **ツールボックス** の [**コモンコントロール**] タブから、 <xref:Microsoft.Office.Tools.Word.Controls.TextBox> コントロールを文書にドラッグします。

   > [!NOTE]
   > Word の既定では、コントロールはテキスト中にインラインでドロップされます。 Word の [**オプション**] ダイアログボックスの [**編集**] タブで既定値を変更することで、コントロールと図形オブジェクトの挿入方法を変更できます。

3. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

4. [**プロパティ**] ウィンドウのドロップダウンボックスで **TextBox1** を検索し、テキストボックスの [**名前**] プロパティを [表示 **] に変更** します。

5. **ボタン** コントロールをドキュメントにドラッグし、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**insertText**|
   |**[テキスト]**|**テキストの挿入**|

   これで、ボタンがクリックされたときに実行されるコードを記述できるようになりました。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキストボックスにデータを設定する
 ユーザーがボタンをクリックするたびに、 **Hello World ます。** がテキストボックスに追加されます。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキスト ボックスに書き込むには

1. **ソリューションエクスプローラー** で、[ **ThisDocument**] を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet7":::

3. C# では、ボタンのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet8":::

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、メッセージが Hello World ことを確認できるようになりました **。** ボタンをクリックすると、テキストボックスに表示されます。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. ボタンをクリックします。

3. Hello World していることを確認し **ます。** がテキストボックスに表示されます。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Word 文書でボタンとテキスト ボックスを使用する際の基本事項について説明しました。 ここでは、次の作業を行います。

- コンボ ボックスを使用して書式設定を変更する。 詳細については、「 [チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)」を参照してください。

- オプション ボタンを使用してグラフのスタイルを選択する。 詳細については、「 [チュートリアル: オプションボタンを使用してドキュメントのグラフを更新](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ドキュメントのコントロールの Windows フォームの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [方法: Office ドキュメントに Windows フォームコントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
