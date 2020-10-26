---
title: XML データを dataset に読み取る |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
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
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c34fb87c02ff60d9b28c43130d6fbf3a12e70349
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72652903"
---
# <a name="read-xml-data-into-a-dataset"></a>XML データのデータセットへの読み込み
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ADO.NET には、XML データを操作するための単純なメソッドが用意されています。 このチュートリアルでは、XML データをデータセットに読み込む Windows アプリケーションを作成します。 次に、データセットがコントロールに表示され <xref:System.Windows.Forms.DataGridView> ます。 最後に、XML ファイルの内容に基づく XML スキーマがテキストボックスに表示されます。

 このチュートリアルは、次の5つの主要な手順で構成されています。

1. 新しいプロジェクトの作成

2. データセットに読み込む XML ファイルの作成

3. ユーザー インターフェイスの作成

4. データセットの作成、XML ファイルの読み取り、およびコントロールの表示 <xref:System.Windows.Forms.DataGridView>

5. コントロール内の XML ファイルに基づいて XML スキーマを表示するコードの追加 <xref:System.Windows.Forms.TextBox>

> [!NOTE]
> 表示されるダイアログボックスとメニューコマンドは、アクティブな設定や使用しているエディションによっては、ヘルプに記載されているものと異なる場合があります。 設定を変更するには、[  **ツール** ] メニューの [**設定のインポートとエクスポート**] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、このチュートリアルを含む Visual Basic または Visual C# プロジェクトを作成します。

#### <a name="to-create-the-new-windows-project"></a>新しい Windows プロジェクトを作成するには

1. [ **ファイル** ] メニューで、新しいプロジェクトを作成します。

2. プロジェクトに `ReadingXML` という名前を付けます。

3. [ **Windows アプリケーション**] を選択し、[ **OK]** を選択します。 詳細については、「 [クライアントアプリケーション](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)」を参照してください。

     **ReadingXML**プロジェクトが作成され、**ソリューションエクスプローラー**に追加されます。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>データセットに読み込む XML ファイルを生成します。
 このチュートリアルでは、XML データをデータセットに読み込むことに重点を置いて、XML ファイルの内容を示します。

#### <a name="to-create-the-xml-file-that-will-be-read-into-the-dataset"></a>データセットに読み込む XML ファイルを作成するには

1. [ **プロジェクト** ] メニューの [**新しい項目の追加**] をクリックします。

2. [ **XML ファイル**] を選択し、ファイルに名前を指定して、[ `authors.xml` **追加**] を選択します。

     XML ファイルがデザイナーに読み込まれ、編集できる状態になります。

3. 次のコードをエディターの XML 宣言の下に貼り付けます。

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

4. [ **ファイル** ] メニューの [**authors.xmlの保存 **] を選択します。

## <a name="create-the-user-interface"></a>ユーザー インターフェイスを作成する
 このアプリケーションのユーザーインターフェイスは、次の要素で構成されています。

- <xref:System.Windows.Forms.DataGridView>XML ファイルの内容をデータとして表示するコントロール。

- <xref:System.Windows.Forms.TextBox>Xml ファイルの xml スキーマを表示するコントロール。

- 2つ <xref:System.Windows.Forms.Button> のコントロール。

  - 1つのボタンが XML ファイルをデータセットに読み込み、コントロールに表示し <xref:System.Windows.Forms.DataGridView> ます。

  - 2番目のボタンは、データセットからスキーマを抽出し、を使用して <xref:System.IO.StringWriter> コントロールにスキーマを表示し <xref:System.Windows.Forms.TextBox> ます。

#### <a name="to-add-controls-to-the-form"></a>フォームにコントロールを追加するには

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

## <a name="create-the-dataset-thatreceives-the-xml-data"></a>XML データを受け取るデータセットを作成する
 この手順では、という名前の新しいデータセットを作成し `authors` ます。 データセットの詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

#### <a name="to-create-a-new-dataset-that--receives-the-xml-data"></a>XML データを受け取る新しいデータセットを作成するには

1. **ソリューションエクスプローラー**で、 **Form1**のソースファイルを選択し、[**ソリューションエクスプローラー** ] ツールバーの [**デザイナーの表示**] をクリックします。

2. [ [ツールボックス] の [データ] タブ](../ide/reference/toolbox-data-tab.md)で、 **データセット** を **Form1**にドラッグします。

3. [ **データセットの追加** ] ダイアログボックスで、[型指定されていない **データセット**] を選択し、[ **OK]** を選択します。

     **DataSet1** がコンポーネントトレイに追加されます。

4. [ **プロパティ** ] ウィンドウで、の **名前** とプロパティを設定し <xref:System.Data.DataSet.DataSetName%2A> `AuthorsDataSet` ます。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>XML ファイルをデータセットに読み込むイベントハンドラーを作成する
 [ **Xml の読み取り** ] ボタンをクリックすると、xml ファイルがデータセットに読み込まれます。 次に、それを <xref:System.Windows.Forms.DataGridView> データセットにバインドするコントロールのプロパティを設定します。

#### <a name="to-add-code-to-the-readxmlbutton_click-event-handler"></a>ReadXmlButton_Click イベントハンドラーにコードを追加するには

1. **ソリューションエクスプローラー**で [ **Form1**] を選択し、[**ソリューションエクスプローラー** ] ツールバーの [**デザイナーの表示**] をクリックします。

2. [ **XML の読み取り** ] ボタンを選択します。

     イベントハンドラーで **コードエディター** が開き `ReadXmlButton_Click` ます。

3. イベントハンドラーに次のコードを入力し `ReadXmlButton_Click` ます。

     [!code-csharp[VbRaddataFillingAndExecuting#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#2)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#2)]

4. `ReadXMLButton_Click`イベントハンドラーのコードで、エントリを `filepath =` 正しいパスに変更します。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>イベントハンドラーを作成し、テキストボックスにスキーマを表示します。
 [ **スキーマの表示** ] ボタンをクリックすると、スキーマを格納したオブジェクトが作成され、 <xref:System.IO.StringWriter> コントロールに表示され <xref:System.Windows.Forms.TextBox> ます。

#### <a name="to-add-code-to-the-showschemabutton_click-event-handler"></a>ShowSchemaButton_Click イベントハンドラーにコードを追加するには

1. **ソリューションエクスプローラー**で [ **Form1**] を選択し、[**ビューデザイナー** ] をクリックします。

2. [ **スキーマの表示** ] ボタンを選択します。

     イベントハンドラーで **コードエディター** が開き `ShowSchemaButton_Click` ます。

3. イベントハンドラーに次のコードを入力し `ShowSchemaButton_Click` ます。

     [!code-csharp[VbRaddataFillingAndExecuting#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#3)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#3)]

## <a name="test-the-form"></a>フォームをテストする

フォームをテストして、期待どおりに動作することを確認します。

1. **F5 キーを押し**てアプリケーションを実行します。

2. [ **XML の読み取り** ] ボタンを選択します。

     DataGridView には、XML ファイルの内容が表示されます。

3. [ **スキーマの表示** ] ボタンを選択します。

     このテキストボックスには、XML ファイルの XML スキーマが表示されます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、xml ファイルをデータセットに読み込む方法、および XML ファイルの内容に基づいてスキーマを作成する方法の基本について説明します。 次に、次のタスクについて説明します。

- データセット内のデータを編集し、XML として書き戻します。 詳細については、「<xref:System.Data.DataSet.WriteXml%2A>」を参照してください。

- データセット内のデータを編集し、データベースに書き込みます。

## <a name="see-also"></a>参照
 データ[チュートリアル](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4) [visual studio でデータにアクセス](../data-tools/accessing-data-in-visual-studio.md)[するアプリケーションの準備](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad) [Visual studio でデータ XML ツール](../xml-tools/xml-tools-in-visual-studio.md)を受け取る
