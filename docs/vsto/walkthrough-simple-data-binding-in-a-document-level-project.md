---
title: 'チュートリアル: ドキュメントレベルのプロジェクトでの単純データバインディング'
description: ドキュメントレベルのプロジェクトでのデータバインディングの基本について説明します。また、SQL Server データベースの1つのデータフィールドが Microsoft Excel の名前付き範囲にバインドされていることを確認します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], worksheet cell to Database field
- worksheets [Office development in Visual Studio], binding worksheet cell to Database field
- Database field [Office development in Visual Studio]
- data [Office development in Visual Studio], binding data
- simple data binding [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 36d4da65a6cd39c53f1f9d8edf4f9d9b1fe46284
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826851"
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>チュートリアル: ドキュメントレベルのプロジェクトでの単純データバインディング
  このチュートリアルでは、ドキュメントレベルのプロジェクトでのデータバインディングの基本について説明します。 SQL Server データベースの単一のデータフィールドは、Microsoft Office Excel の名前付き範囲にバインドされます。 このチュートリアルでは、テーブル内のすべてのレコードをスクロールできるようにするコントロールを追加する方法についても説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- Excel プロジェクトのデータソースを作成する。

- ワークシートにコントロールを追加する。

- データベースレコードをスクロールしています。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプルデータベースを使用したサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みの権限。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、Excel ブックプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# のいずれかを使用して、 **My Simple Data Binding** という名前の Excel ブックプロジェクトを作成します。 [ **新しいドキュメントを作成** する。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

   新しい Excel ブックがデザイナーで開き、 **[My Simple Data Binding** ] プロジェクトが **ソリューションエクスプローラー** に追加されます。

## <a name="create-the-data-source"></a>データ ソースを作成する
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [   >  **他の Windows**  >  **データソース** の表示] をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. [ **データベース** ] を選択し、[ **次へ**] をクリックします。

4. Northwind サンプル SQL Server データベースへのデータ接続を選択するか、[ **新しい接続** ] ボタンを使用して新しい接続を追加します。

5. 接続を選択または作成したら、[ **次へ**] をクリックします。

6. 選択されている場合は、接続を保存するオプションをオフにして、[ **次へ**] をクリックします。

7. [**データベースオブジェクト**] ウィンドウで、[**テーブル**] ノードを展開します。

8. **Customers** テーブルの横にあるチェックボックスをオンにします。

9. **[完了]** をクリックします。

   [**データソース**] ウィンドウに **Customers** テーブルが追加されます。 また、 **ソリューションエクスプローラー** に表示される、型指定されたデータセットをプロジェクトに追加します。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 このチュートリアルでは、最初のワークシートに2つの名前付き範囲と4つのボタンが必要です。 まず、[ **データソース** ] ウィンドウから2つの名前付き範囲を追加して、データソースに自動的にバインドされるようにします。 次に、[ **ツールボックス**] からボタンを追加します。

### <a name="to-add-two-named-ranges"></a>2つの名前付き範囲を追加するには

1. Visual Studio デザイナーで *[My Simple Data Binding.xlsx* ] ブックが開いていることを確認します。 **Sheet1** が表示されます。

2. [ **データソース** ] ウィンドウを開き、[ **Customers** ] ノードを展開します。

3. [ **CompanyName** ] 列を選択し、表示されるドロップダウン矢印をクリックします。

4. ドロップダウンリストから [ **NamedRange** ] を選択し、[ **CompanyName** ] 列をセル **A1** にドラッグします。

     <xref:Microsoft.Office.Tools.Excel.NamedRange>という名前のコントロール `companyNameNamedRange` がセル **A1** に作成されます。 同時に、と <xref:System.Windows.Forms.BindingSource> いう名前 `customersBindingSource` のテーブルアダプターと <xref:System.Data.DataSet> インスタンスがプロジェクトに追加されます。 コントロールは、にバインドされ <xref:System.Windows.Forms.BindingSource> 、さらにインスタンスにバインドされ <xref:System.Data.DataSet> ます。

5. [**データソース**] ウィンドウで [ **CustomerID** ] 列を選択し、表示されるドロップダウン矢印をクリックします。

6. ドロップダウンリストで [ **NamedRange** ] をクリックし、[ **CustomerID** ] 列をセル **B1** にドラッグします。

7. と <xref:Microsoft.Office.Tools.Excel.NamedRange> いう名前の別のコントロール `customerIDNamedRange` がセル **B1** に作成され、にバインドされ <xref:System.Windows.Forms.BindingSource> ます。

### <a name="to-add-four-buttons"></a>4つのボタンを追加するには

1. **ツールボックス** の [**コモンコントロール**] タブから、 <xref:System.Windows.Forms.Button> ワークシートのセル **A3** にコントロールを追加します。

    このボタンにはという名前が付けら `Button1` れます。

2. この順序で次のセルに3つのボタンを追加して、名前が表示されるようにします。

   |Cell (セル)|[(名前)]|
   |----------|--------------|
   |B3|Button2|
   |C3|Button3|
   |D3|Button4|

   次の手順では、ボタンにテキストを追加し、C# ではイベントハンドラーを追加します。

## <a name="initialize-the-controls"></a>コントロールを初期化します
 ボタンテキストを設定し、イベントの発生時にイベントハンドラーを追加し <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> ます。

### <a name="to-initialize-the-controls"></a>コントロールを初期化するには

1. **ソリューションエクスプローラー** で、 **Sheet1** または **sheet1** を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. 次のコードをメソッドに追加して、 `Sheet1_Startup` 各ボタンのテキストを設定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet2":::

3. C# の場合のみ、ボタンクリックイベントのイベントハンドラーをメソッドに追加し `Sheet1_Startup` ます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet3":::

   次に <xref:System.Windows.Forms.Control.Click> 、ユーザーがレコードを参照できるように、ボタンのイベントを処理するコードを追加します。

## <a name="add-code-to-enable-scrolling-through-the-records"></a>レコードのスクロールを有効にするコードを追加する
 <xref:System.Windows.Forms.Control.Click>各ボタンのイベントハンドラーにコードを追加して、レコード間を移動します。

### <a name="to-move-to-the-first-record"></a>最初のレコードに移動するには

1. ボタンのイベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> `Button1` し、最初のレコードに移動する次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet4":::

### <a name="to-move-to-the-previous-record"></a>前のレコードに移動するには

1. ボタンのイベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> `Button2` し、次のコードを追加して位置を1つずつ移動します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet5":::

### <a name="to-move-to-the-next-record"></a>次のレコードに移動するには

1. ボタンのイベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> `Button3` し、次のコードを追加して位置を1つずつ進めます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet6":::

### <a name="to-move-to-the-last-record"></a>最後のレコードに移動するには

1. ボタンのイベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> `Button4` し、次のコードを追加して最後のレコードに移動します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet7":::

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、ブックをテストして、データベース内のレコードを参照できるかどうかを確認できます。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. 最初のレコードがセル **A1** と **B1** に表示されることを確認します。

3. **>**( `Button3` ) ボタンをクリックし、次のレコードがセル **A1** と **B1** に表示されることを確認します。

4. 他のスクロールボタンをクリックして、レコードが想定どおりに変更されていることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、データベースのフィールドに名前付き範囲をバインドする方法の基本について説明します。 ここでは、次の作業を行います。

- データをキャッシュして、オフラインで使用できるようにします。 詳細については、「 [方法: オフラインまたはサーバー上で使用するデータをキャッシュ](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)する」を参照してください。

- 1つのフィールドではなく、テーブル内の複数の列にセルをバインドします。 詳細については、「 [チュートリアル: ドキュメントレベルのプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)」を参照してください。

- コントロールを使用し <xref:System.Windows.Forms.BindingNavigator> てレコードをスクロールします。 詳細については、「 [方法: Windows フォーム BindingNavigator コントロールを使用してデータを移動する](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office ソリューションのデータ](../vsto/data-in-office-solutions.md)
- [チュートリアル: ドキュメントレベルのプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
