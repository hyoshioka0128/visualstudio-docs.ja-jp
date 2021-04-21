---
title: 'チュートリアル: サーバー上のブックからキャッシュされたデータを取得する'
description: ServerDocument クラスを使用して Excel を起動することなく、Microsoft Excel ブックにキャッシュされているデータセットからデータを取得する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks [Office development in Visual Studio], retrieving data
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e11099b0ea37856919affb927c3f118572d339af
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826877"
---
# <a name="walkthrough-retrieve-cached-data-from-a-workbook-on-a-server"></a>チュートリアル: サーバー上のブックからキャッシュされたデータを取得する
  このチュートリアルでは、クラスを使用して Excel を起動することなく、Microsoft Office Excel ブックにキャッシュされているデータセットからデータを取得する方法について説明 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- *AdventureWorksLT* データベースのデータを含むデータセットを定義する。

- Excel ブックプロジェクトとコンソールアプリケーションプロジェクトでデータセットのインスタンスを作成する。

- ブックのデータ <xref:Microsoft.Office.Tools.Excel.ListObject> セットにバインドされたを作成し、ブックを <xref:Microsoft.Office.Tools.Excel.ListObject> 開いたときににデータを設定します。

- ブック内のデータセットをデータキャッシュに追加します。

- Excel を起動せずに、キャッシュされたデータセットからコンソールアプリケーションのデータセットにデータを読み込む。

  このチュートリアルでは、開発用コンピューターでコードを実行していることを前提としていますが、このチュートリアルで示すコードは、Excel がインストールされていないサーバーで使用できます。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- AdventureWorksLT サンプルデータベースがアタッチされている Microsoft SQL Server または Microsoft SQL Server Express の実行中のインスタンスへのアクセス。 AdventureWorksLT データベースは、 [CodePlex の web サイト](https://archive.codeplex.com/?p=SqlServerSamples)からダウンロードできます。 データベースをアタッチする方法について詳しくは、次のトピックをご覧ください。

  - SQL Server Management Studio または SQL Server Management Studio Express を使用してデータベースをアタッチする方法については、「 [データベースをアタッチする方法 (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database)」を参照してください。

  - コマンドラインを使用してデータベースをアタッチする方法については、「 [方法: SQL Server Express にデータベースファイルをアタッチ](/previous-versions/sql/)する」を参照してください。

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>データセットを定義するクラスライブラリプロジェクトを作成する
 Excel ブックプロジェクトとコンソールアプリケーションで同じデータセットを使用するには、これらのプロジェクトの両方によって参照される別のアセンブリにデータセットを定義する必要があります。 このチュートリアルでは、クラスライブラリプロジェクトにデータセットを定義します。

### <a name="create-the-class-library-project"></a>クラス ライブラリ プロジェクトを作成する

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. [テンプレート] ペインで [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows**] をクリックします。

4. プロジェクトテンプレートの一覧で [ **クラスライブラリ**] を選択します。

5. [ **名前** ] ボックスに「 **AdventureWorksDataSet**」と入力します。

6. [ **参照**] をクリックし、 *%UserProfile%\My ドキュメント* (windows XP 以前の場合) または *%UserProfile%\Documents* (windows Vista の場合) フォルダーに移動して、[ **フォルダーの選択**] をクリックします。

7. [ **新しいプロジェクト** ] ダイアログボックスで、[ **ソリューションのディレクトリを作成** する] チェックボックスがオフになっていることを確認します。

8. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**AdventureWorksDataSet** プロジェクトを **ソリューションエクスプローラー** に追加し、 *class1* または *class1* コードファイルを開きます。

9. **ソリューションエクスプローラー** で、[ *class1* ] または [ *class1*] を右クリックし、[**削除**] をクリックします。 このチュートリアルでは、このファイルは必要ありません。

## <a name="define-a-dataset-in-the-class-library-project"></a>クラスライブラリプロジェクトでのデータセットの定義
 SQL Server 2005 の AdventureWorksLT データベースのデータを含む、型指定されたデータセットを定義します。 このチュートリアルの後半では、Excel ブックプロジェクトとコンソールアプリケーションプロジェクトからこのデータセットを参照します。

 データセットは、AdventureWorksLT データベースの Product テーブルのデータを表す、 *型指定* されたデータセットです。 型指定されたデータセットの詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

### <a name="define-a-typed-dataset-in-the-class-library-project"></a>クラスライブラリプロジェクトで型指定されたデータセットを定義する

1. **ソリューションエクスプローラー** で、 **AdventureWorksDataSet** プロジェクトをクリックします。

2. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [   >  **他の Windows**  >  **データソース** の表示] をクリックして表示します。

3. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

4. **[データベース]** をクリックして、 **[次へ]** をクリックします。

5. AdventureWorksLT データベースへの既存の接続がある場合は、この接続を選択し、[ **次へ**] をクリックします。

    それ以外の場合は、 **[新しい接続]** をクリックし、 **[接続の追加]** ダイアログ ボックスを使用して新しい接続を作成します。 詳細については、「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

6. **[アプリケーション構成ファイルへの接続文字列を保存]** ページで、 **[次へ]** をクリックします。

7. [ **データベースオブジェクトの選択** ] ページで、[ **テーブル** ] を展開し、[ **Product (saleslt)**] を選択します。

8. **[完了]** をクリックします。

    *Adventureworksltdataset.xsd* ファイルが **AdventureWorksDataSet** プロジェクトに追加されます。 このファイルでは、次の項目を定義します。

   - `AdventureWorksLTDataSet`という名前の型指定されたデータセット。 このデータセットは、AdventureWorksLT データベース内の Product テーブルの内容を表します。

   - という名前の TableAdapter `ProductTableAdapter` 。 この TableAdapter を使用して、のデータの読み取りと書き込みを行うことができ `AdventureWorksLTDataSet` ます。 詳細については、「 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

     これらのオブジェクトは、どちらもこのチュートリアルの後半で使用します。

9. **ソリューションエクスプローラー** で、[ **AdventureWorksDataSet** ] を右クリックし、[**ビルド**] をクリックします。

     プロジェクトのビルドでエラーが発生しないことを確認します。

## <a name="create-an-excel-workbook-project"></a>Excel ブックプロジェクトを作成する
 データへのインターフェイスの Excel ブックプロジェクトを作成します。 このチュートリアルの後半では、データを <xref:Microsoft.Office.Tools.Excel.ListObject> 表示するを作成し、データセットのインスタンスをブックのデータキャッシュに追加します。

### <a name="create-the-excel-workbook-project"></a>Excel ブックプロジェクトを作成する

1. **ソリューションエクスプローラー** で、 **AdventureWorksDataSet** ソリューションを右クリックし、[**追加**] をポイントして、[**新しいプロジェクト**] をクリックします。

2. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

3. 展開した **[Office/SharePoint]** ノードの下で、 **[Office Add-ins]** ノードを選択します。

4. プロジェクト テンプレートのリストで、 **[Excel 2010 ブック]** または **[Excel 2013 ブック]** プロジェクトを選択します。

5. [ **名前** ] ボックスに「 **AdventureWorksReport**」と入力します。 場所は変更しないでください。

6. **[OK]** をクリックします。

     **Visual Studio Tools for Office プロジェクト ウィザード** が開きます。

7. [ **新しいドキュメントを作成** する] が選択されていることを確認し、[ **OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]デザイナーで **AdventureWorksReport** ブックを開き、**ソリューションエクスプローラー** に **AdventureWorksReport** プロジェクトを追加します。

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>Excel ブックプロジェクトのデータソースにデータセットを追加する
 Excel ブックでデータセットを表示するには、まず、Excel ブックプロジェクトのデータソースにデータセットを追加する必要があります。

1. **ソリューションエクスプローラー** で、 **AdventureWorksReport** プロジェクトの [ *Sheet1* ] または [ *sheet1* ] をダブルクリックします。

     デザイナーでブックが開きます。

2. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

     **データソース構成ウィザード** が開きます。

3. [ **オブジェクト**] をクリックし、[ **次へ**] をクリックします。

4. [ **バインド先のオブジェクトを選択** してください] ページで、[ **参照の追加**] をクリックします。

5. [ **プロジェクト** ] タブで、[ **AdventureWorksDataSet** ] をクリックし、[ **OK**] をクリックします。

6. **AdventureWorksDataSet** アセンブリの **AdventureWorksDataSet** 名前空間で、[ **adventureworksltdataset.xsd** ] をクリックし、[**完了**] をクリックします。

     [ **データソース** ] ウィンドウが開き、 **adventureworksltdataset.xsd** がデータソースの一覧に追加されます。

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>データセットのインスタンスにバインドされた ListObject を作成する
 ブックにデータセットを表示するには、 <xref:Microsoft.Office.Tools.Excel.ListObject> データセットのインスタンスにバインドされたを作成します。 コントロールをデータにバインドする方法の詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

1. [**データソース**] ウィンドウで、[ **AdventureWorksDataSet**] の下の [ **adventureworksltdataset.xsd** ] ノードを展開します。

2. **Product** ノードを選択し、表示されるドロップダウン矢印をクリックして、ドロップダウンリストで [ **ListObject** ] を選択します。

     ドロップダウン矢印が表示されない場合は、ブックがデザイナーで開かれていることを確認します。

3. **Product** テーブルをセル A1 にドラッグします。

     <xref:Microsoft.Office.Tools.Excel.ListObject>という名前のコントロール `productListObject` がワークシートに作成され、セル A1 から開始されます。 同時に、 `adventureWorksLTDataSet` という名前のデータセット オブジェクトと、 <xref:System.Windows.Forms.BindingSource> という名前の `productBindingSource` がプロジェクトに追加されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:System.Windows.Forms.BindingSource>にバインドされ、さらにこれがデータセット オブジェクトにバインドされます。

## <a name="add-the-dataset-to-the-data-cache"></a>データセットをデータキャッシュに追加する
 Excel ブックプロジェクトの外部にあるコードで、ブック内のデータセットにアクセスできるようにするには、データセットをデータキャッシュに追加する必要があります。 データキャッシュの詳細については、「 [ドキュメントレベルのカスタマイズでのキャッシュデータ](../vsto/cached-data-in-document-level-customizations.md) 」と「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

1. デザイナーで、[ **adventureworksltdataset.xsd**] をクリックします。

2. [ **プロパティ** ] ウィンドウで、[ **修飾子** ] プロパティを [ **パブリック**] に設定します。

3. **CacheInDocument** プロパティを **True** に設定します。

## <a name="initialize-the-dataset-in-the-workbook"></a>ブック内のデータセットを初期化します
 コンソールアプリケーションを使用してキャッシュされたデータセットからデータを取得するには、まず、キャッシュされたデータセットにデータを設定する必要があります。

1. **ソリューションエクスプローラー** で、 *sheet1* ファイルまたは *sheet1* ファイルを右クリックし、[コードの **表示**] をクリックします。

2. `Sheet1_Startup` イベント ハンドラーを次のコードで置き換えます。 このコードでは、AdventureWorksDataSet プロジェクトで定義されているクラスのインスタンスを使用して、キャッシュされたデータセットにデータが格納され `ProductTableAdapter` ます (現在空の場合)。 

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/AdventureWorksReport/Sheet1.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/AdventureWorksReport/Sheet1.vb" id="Snippet8":::

## <a name="checkpoint"></a>Checkpoint
 Excel ブックプロジェクトをビルドして実行し、エラーなしでコンパイルおよび実行されることを確認します。 この操作では、キャッシュされたデータセットがいっぱいになり、ブックにデータが保存されます。

### <a name="build-and-run-the-project"></a>プロジェクトをビルドして実行する

1. **ソリューションエクスプローラー** で、 **AdventureWorksReport** プロジェクトを右クリックし、[**デバッグ**]、[**新しいインスタンスを開始**] の順にクリックします。

     プロジェクトがビルドされ、Excel でブックが開きます。 次の点を確認します。

    - は <xref:Microsoft.Office.Tools.Excel.ListObject> データを格納します。

    - の最初の行の **ListPrice** 列の値 <xref:Microsoft.Office.Tools.Excel.ListObject> は1431.5 です。 このチュートリアルの後半では、コンソールアプリケーションを使用して、 **ListPrice** 列の値を変更します。

2. ブックを保存します。 ファイル名やブックの場所は変更しないでください。

3. Excel を終了します。

## <a name="create-a-console-application-project"></a>コンソールアプリケーションプロジェクトの作成
 ブック内のキャッシュされたデータセットのデータを変更するために使用するコンソールアプリケーションプロジェクトを作成します。

1. **ソリューションエクスプローラー** で、 **AdventureWorksDataSet** ソリューションを右クリックし、[**追加**] をポイントして、[**新しいプロジェクト**] をクリックします。

2. [ **プロジェクトの種類** ] ペインで、[ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows**] をクリックします。

3. **[テンプレート]** ペインで **[コンソール アプリケーション]** をクリックします。

4. [ **名前** ] ボックスに「 **DataReader**」と入力します。 場所は変更しないでください。

5. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**DataReader** プロジェクトを **ソリューションエクスプローラー** に追加し、*プログラム .cs* または module1.vb コードファイルを開き *ます。*

## <a name="retrieve-data-from-the-cached-dataset-by-using-the-console-application"></a>コンソールアプリケーションを使用して、キャッシュされたデータセットからデータを取得する
 コンソールアプリケーションのクラスを使用して <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 、ローカルオブジェクトにデータを読み取り `AdventureWorksLTDataSet` ます。 ローカルデータセットが、キャッシュされたデータセットのデータで初期化されたことを確認するために、アプリケーションはローカルデータセットの行数を表示します。

### <a name="retrieve-data-from-the-cached-dataset"></a>キャッシュされたデータセットからデータを取得する

1. **ソリューションエクスプローラー** で、 **DataReader** プロジェクトを右クリックし、[**参照の追加**] をクリックします。

2. [ **.Net** ] タブで、[ **VisualStudio. ServerDocument**] を選択します。

3. **[OK]** をクリックします。

4. **ソリューションエクスプローラー** で、 **DataReader** プロジェクトを右クリックし、[**参照の追加**] をクリックします。

5. [ **プロジェクト** ] タブで [ **AdventureWorksDataSet**] を選択し、[ **OK**] をクリックします。

6. コードエディターで、*プログラム .cs* ファイルまたは module1.vb ファイルを *開きます。*

7. コードファイルの先頭に、(C# の場合) または **Imports** (for Visual Basic) ステートメントを **使用して**、次のコードを追加します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet1":::

8. `Main` メソッドに次のコードを追加します。 このコードは、次のオブジェクトを宣言します。

   - `AdventureWorksLTDataSet` **AdventureWorksDataSet** プロジェクトで定義されている型のインスタンス。

   - **AdventureWorksReport** プロジェクトの build フォルダー内の AdventureWorksReport ブックへのパス。

   - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>ブック内のデータキャッシュへのアクセスに使用するオブジェクト。

     > [!NOTE]
     > 次のコードは、ブックが *.xlsx* 拡張子を使用して保存されていることを前提としています。 プロジェクト内のブックの拡張子が異なる場合は、必要に応じてパスを変更します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet10":::

9. `Main`前の手順で追加したコードの後に、次のコードをメソッドに追加します。 このコードは、以下のタスクを実行します。

   - このメソッドは、クラスのプロパティを使用して、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> ブック内のキャッシュされたデータセットにアクセスします。

   - キャッシュされたデータセットからローカルデータセットにデータを読み取ります。

   - データがあることを確認するために、ローカルデータセット内の行の数が表示されます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet11":::

10. [ **ビルド** ] メニューの [ **DataReader のビルド**] をクリックします。

## <a name="test-the-project"></a>プロジェクトをテストする
 コンソールアプリケーションを実行すると、ローカルデータセット内の行の数が表示されます。

### <a name="test-the-workbook"></a>ブックをテストする

1. **ソリューションエクスプローラー** で、 **DataReader** プロジェクトを右クリックし、[**デバッグ**] をポイントして、[**新しいインスタンスを開始**] をクリックします。

     ローカルデータセットに295行が含まれていることがアプリケーションによって報告されていることを確認します。

2. **Enter** キーを押してアプリケーションを閉じます。

## <a name="next-steps"></a>次のステップ
 キャッシュされたデータの操作の詳細については、次のトピックを参照してください。

- Excel を起動せずに、キャッシュされたデータセット内のデータを変更する。 詳細については、「 [チュートリアル: サーバー上のブックにキャッシュされたデータを変更](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [チュートリアル: サーバー上のブックにデータを挿入する](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)
- [チュートリアル: サーバー上のブックでキャッシュされたデータを変更する](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)
