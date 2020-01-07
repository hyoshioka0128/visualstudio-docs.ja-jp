---
title: XML データのデータセットへの読み込み
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 5f89645b9d5ec8ab0f69fad4fea5a399d8e6764d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586329"
---
# <a name="read-xml-data-into-a-dataset"></a>XML データのデータセットへの読み込み

ADO.NET には、XML データを操作するための単純なメソッドが用意されています。 このチュートリアルでは、XML データをデータセットに読み込む Windows アプリケーションを作成します。 次に、データセットが <xref:System.Windows.Forms.DataGridView> コントロールに表示されます。 最後に、XML ファイルの内容に基づく XML スキーマがテキストボックスに表示されます。

## <a name="create-a-new-project"></a>新しいプロジェクトの作成

または Visual Basic 用の新しい**Windows フォームアプリ**プロジェクトを作成します。 C# プロジェクトに**ReadingXML**という名前を指定します。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>データセットに読み込む XML ファイルを生成します。

このチュートリアルでは、XML データをデータセットに読み込むことに重点を置いて、XML ファイルの内容を示します。

1. **[プロジェクト]** メニューで **[新しい項目の追加]** を選択します。

2. **[Xml ファイル]** を選択し、ファイルに「 **authors .xml**」という名前を指定して、 **[追加]** を選択します。

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

4. **[ファイル]** メニューの **[.xml の保存]** を選択します。

## <a name="create-the-user-interface"></a>ユーザー インターフェイスを作成する

このアプリケーションのユーザーインターフェイスは、次の要素で構成されています。

- XML ファイルの内容をデータとして表示する <xref:System.Windows.Forms.DataGridView> コントロール。

- XML ファイルの XML スキーマを表示する <xref:System.Windows.Forms.TextBox> コントロール。

- 2つの <xref:System.Windows.Forms.Button> コントロール。

  - 1つのボタンが XML ファイルをデータセットに読み込み、<xref:System.Windows.Forms.DataGridView> コントロールに表示します。

  - 2番目のボタンは、データセットからスキーマを抽出し、<xref:System.IO.StringWriter> によって <xref:System.Windows.Forms.TextBox> コントロールに表示します。

### <a name="to-add-controls-to-the-form"></a>フォームにコントロールを追加するには

1. デザインビューで `Form1` を開きます。

2. **[ツールボックス]** から、次のコントロールをフォームにドラッグします。

    - 1つの <xref:System.Windows.Forms.DataGridView> コントロール

    - 1つの <xref:System.Windows.Forms.TextBox> コントロール

    - 2つの <xref:System.Windows.Forms.Button> コントロール

3. 次のプロパティを設定します。

    |Control|property|設定|
    |-------------|--------------|-------------|
    |`TextBox1`|**Multiline**|`true`|
    ||**ScrollBars**|**垂直方向**|
    |`Button1`|**名前**|`ReadXmlButton`|
    ||**テキスト**|`Read XML`|
    |`Button2`|**名前**|`ShowSchemaButton`|
    ||**テキスト**|`Show Schema`|

## <a name="create-the-dataset-that-receives-the-xml-data"></a>XML データを受け取るデータセットを作成する

この手順では、`authors`という名前の新しいデータセットを作成します。 データセットの詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

1. **ソリューションエクスプローラー**で、 **Form1**のソースファイルを選択し、 **[ソリューションエクスプローラー]** ツールバーの **[デザイナーの表示]** をクリックします。

2. [[ツールボックス] の [データ] タブ](../ide/reference/toolbox-data-tab.md)で、**データセット**を**Form1**にドラッグします。

3. **[データセットの追加]** ダイアログボックスで、型指定されていない **[データセット]** を選択し、[ **OK]** を選択します。

     **DataSet1**がコンポーネントトレイに追加されます。

4. **プロパティ** ウィンドウで、**名前** と `AuthorsDataSet`の <xref:System.Data.DataSet.DataSetName%2A> プロパティを設定します。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>XML ファイルをデータセットに読み込むイベントハンドラーを作成する

**[Xml の読み取り]** ボタンをクリックすると、xml ファイルがデータセットに読み込まれます。 次に、それをデータセットにバインドする <xref:System.Windows.Forms.DataGridView> コントロールのプロパティを設定します。

1. **ソリューションエクスプローラー**で **[Form1]** を選択し、 **[ソリューションエクスプローラー]** ツールバーの **[デザイナーの表示]** をクリックします。

2. **[XML の読み取り]** ボタンを選択します。

     **コードエディター**が `ReadXmlButton_Click` イベントハンドラーで開きます。

3. `ReadXmlButton_Click` イベントハンドラーに次のコードを入力します。

     [!code-csharp[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_1.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_1.vb)]

4. `ReadXMLButton_Click` イベントハンドラーのコードで、`filepath =` エントリを正しいパスに変更します。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>イベントハンドラーを作成し、テキストボックスにスキーマを表示します。

**[スキーマの表示]** ボタンをクリックすると、スキーマを格納し、<xref:System.Windows.Forms.TextBox>コントロールに表示される <xref:System.IO.StringWriter> オブジェクトが作成されます。

1. **ソリューションエクスプローラー**で **[Form1]** を選択し、 **[ビューデザイナー]** をクリックします。

2. **[スキーマの表示]** ボタンを選択します。

     **コードエディター**が `ShowSchemaButton_Click` イベントハンドラーで開きます。

3. `ShowSchemaButton_Click` イベント ハンドラーに次のコードを貼り付けます。

     [!code-csharp[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_2.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_2.vb)]

## <a name="test-the-form"></a>フォームをテストする

フォームをテストして、期待どおりに動作することを確認します。

1. **F5 キーを押し**てアプリケーションを実行します。

2. **[XML の読み取り]** ボタンを選択します。

     DataGridView には、XML ファイルの内容が表示されます。

3. **[スキーマの表示]** ボタンを選択します。

     このテキストボックスには、XML ファイルの XML スキーマが表示されます。

## <a name="next-steps"></a>次のステップ:

このチュートリアルでは、xml ファイルをデータセットに読み込む方法、および XML ファイルの内容に基づいてスキーマを作成する方法の基本について説明します。 次に、次のタスクについて説明します。

- データセット内のデータを編集し、XML として書き戻します。 詳細については、「 <xref:System.Data.DataSet.WriteXml%2A>」を参照してください。

- データセット内のデータを編集し、データベースに書き込みます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [Visual Studio の XML ツール](../xml-tools/xml-tools-in-visual-studio.md)
