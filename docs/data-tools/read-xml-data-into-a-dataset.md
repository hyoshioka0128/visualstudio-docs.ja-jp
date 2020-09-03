---
title: XML データのデータセットへの読み込み
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reading XML
- data access [Visual Studio], XML data
- reading files, XML
- data [Visual Studio], reading from XML files
- reading data, XML files
- XML [Visual Studio], reading
- XML documents, reading
- datasets [Visual Basic], reading XML data
ms.assetid: fae72958-0893-47d6-b3dd-9d42418418e4
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 6cceca336403bdd8907cf0e28e36387eb25a2402
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85281787"
---
# <a name="read-xml-data-into-a-dataset"></a>XML データのデータセットへの読み込み

ADO.NET には、XML データを操作するための単純なメソッドが用意されています。 このチュートリアルでは、XML データをデータセットに読み込む Windows アプリケーションを作成します。 次に、データセットがコントロールに表示され <xref:System.Windows.Forms.DataGridView> ます。 最後に、XML ファイルの内容に基づく XML スキーマがテキストボックスに表示されます。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

C# または Visual Basic 用の新しい **Windows フォームアプリ** プロジェクトを作成します。 プロジェクトに **ReadingXML**という名前を指定します。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>データセットに読み込む XML ファイルを生成します。

このチュートリアルでは、XML データをデータセットに読み込むことに重点を置いて、XML ファイルの内容を示します。

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

2. [ **XML ファイル**] を選択し、ファイルに **authors.xml**という名前を指定して、[ **追加**] を選択します。

   XML ファイルがデザイナーに読み込まれ、編集できる状態になります。

3. 次の XML データをエディターの XML 宣言の下に貼り付けます。

   ```xml
   <Authors_Table>
     <authors>
       <au_id>172-32-1176</au_id>
       <au_lname>White</au_lname>
       <au_fname>Johnson</au_fname>
       <phone>408 496-7223</phone>
       <address>10932 Bigge Rd.</address>
       <city>Menlo Park</city>
       <state>CA</state>
       <zip>94025</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>213-46-8915</au_id>
       <au_lname>Green</au_lname>
       <au_fname>Margie</au_fname>
       <phone>415 986-7020</phone>
       <address>309 63rd St. #411</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94618</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>238-95-7766</au_id>
       <au_lname>Carson</au_lname>
       <au_fname>Cheryl</au_fname>
       <phone>415 548-7723</phone>
       <address>589 Darwin Ln.</address>
       <city>Berkeley</city>
       <state>CA</state>
       <zip>94705</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>267-41-2394</au_id>
       <au_lname>Hunter</au_lname>
       <au_fname>Anne</au_fname>
       <phone>408 286-2428</phone>
       <address>22 Cleveland Av. #14</address>
       <city>San Jose</city>
       <state>CA</state>
       <zip>95128</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>274-80-9391</au_id>
       <au_lname>Straight</au_lname>
       <au_fname>Dean</au_fname>
       <phone>415 834-2919</phone>
       <address>5420 College Av.</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94609</zip>
       <contract>true</contract>
     </authors>
   </Authors_Table>
   ```

4. [ **ファイル** ] メニューの [ **authors.xmlの保存 **] を選択します。

## <a name="create-the-user-interface"></a>ユーザー インターフェイスを作成する

このアプリケーションのユーザーインターフェイスは、次の要素で構成されています。

- <xref:System.Windows.Forms.DataGridView>XML ファイルの内容をデータとして表示するコントロール。

- <xref:System.Windows.Forms.TextBox>Xml ファイルの xml スキーマを表示するコントロール。

- 2つ <xref:System.Windows.Forms.Button> のコントロール。

  - 1つのボタンが XML ファイルをデータセットに読み込み、コントロールに表示し <xref:System.Windows.Forms.DataGridView> ます。

  - 2番目のボタンは、データセットからスキーマを抽出し、を使用して <xref:System.IO.StringWriter> コントロールにスキーマを表示し <xref:System.Windows.Forms.TextBox> ます。

### <a name="to-add-controls-to-the-form"></a>フォームにコントロールを追加するには

1. `Form1`デザインビューで開きます。

2. [ **ツールボックス**] から、次のコントロールをフォームにドラッグします。

    - 1つの <xref:System.Windows.Forms.DataGridView> コントロール

    - 1つの <xref:System.Windows.Forms.TextBox> コントロール

    - 2つの <xref:System.Windows.Forms.Button> コントロール

3. 次のプロパティを設定します。

    |コントロール|プロパティ|設定|
    |-------------|--------------|-------------|
    |`TextBox1`|**Multiline**|`true`|
    ||**スクロールバー**|**垂直方向**|
    |`Button1`|**名前**|`ReadXmlButton`|
    ||**Text**|`Read XML`|
    |`Button2`|**名前**|`ShowSchemaButton`|
    ||**Text**|`Show Schema`|

## <a name="create-the-dataset-that-receives-the-xml-data"></a>XML データを受け取るデータセットを作成する

この手順では、という名前の新しいデータセットを作成し `authors` ます。 データセットの詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

1. **ソリューションエクスプローラー**で、 **Form1**のソースファイルを選択し、[**ソリューションエクスプローラー** ] ツールバーの [**デザイナーの表示**] をクリックします。

2. [ [ツールボックス] の [データ] タブ](../ide/reference/toolbox-data-tab.md)で、 **データセット** を **Form1**にドラッグします。

3. [ **データセットの追加** ] ダイアログボックスで、[型指定されていない **データセット**] を選択し、[ **OK]** を選択します。

     **DataSet1** がコンポーネントトレイに追加されます。

4. [ **プロパティ** ] ウィンドウで、の **名前** とプロパティを設定し <xref:System.Data.DataSet.DataSetName%2A> `AuthorsDataSet` ます。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>XML ファイルをデータセットに読み込むイベントハンドラーを作成する

[ **Xml の読み取り** ] ボタンをクリックすると、xml ファイルがデータセットに読み込まれます。 次に、それを <xref:System.Windows.Forms.DataGridView> データセットにバインドするコントロールのプロパティを設定します。

1. **ソリューションエクスプローラー**で [ **Form1**] を選択し、[**ソリューションエクスプローラー** ] ツールバーの [**デザイナーの表示**] をクリックします。

2. [ **XML の読み取り** ] ボタンを選択します。

     イベントハンドラーで **コードエディター** が開き `ReadXmlButton_Click` ます。

3. イベントハンドラーに次のコードを入力し `ReadXmlButton_Click` ます。

     [!code-csharp[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_1.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_1.vb)]

4. `ReadXMLButton_Click`イベントハンドラーのコードで、エントリを `filepath =` 正しいパスに変更します。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>イベントハンドラーを作成し、テキストボックスにスキーマを表示します。

[ **スキーマの表示** ] ボタンをクリックすると、スキーマを格納したオブジェクトが作成され、 <xref:System.IO.StringWriter> コントロールに表示され <xref:System.Windows.Forms.TextBox> ます。

1. **ソリューションエクスプローラー**で [ **Form1**] を選択し、[**ビューデザイナー** ] をクリックします。

2. [ **スキーマの表示** ] ボタンを選択します。

     イベントハンドラーで **コードエディター** が開き `ShowSchemaButton_Click` ます。

3. `ShowSchemaButton_Click` イベント ハンドラーに次のコードを貼り付けます。

     [!code-csharp[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_2.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_2.vb)]

## <a name="test-the-form"></a>フォームをテストする

フォームをテストして、期待どおりに動作することを確認します。

1. **F5 キーを押し**てアプリケーションを実行します。

2. [ **XML の読み取り** ] ボタンを選択します。

     DataGridView には、XML ファイルの内容が表示されます。

3. [ **スキーマの表示** ] ボタンを選択します。

     このテキストボックスには、XML ファイルの XML スキーマが表示されます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、xml ファイルをデータセットに読み込む方法、および XML ファイルの内容に基づいてスキーマを作成する方法の基本について説明します。 次に、次のタスクについて説明します。

- データセット内のデータを編集し、XML として書き戻します。 詳細については、 <xref:System.Data.DataSet.WriteXml%2A> を参照してください。

- データセット内のデータを編集し、データベースに書き込みます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [Visual Studio の XML ツール](../xml-tools/xml-tools-in-visual-studio.md)
