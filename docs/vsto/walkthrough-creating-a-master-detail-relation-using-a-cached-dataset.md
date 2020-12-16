---
title: キャッシュされたデータセットを使用したマスター詳細関係の作成
description: ワークシートでマスター/詳細関係を作成し、ソリューションをオフラインで使用できるようにデータをキャッシュする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- master-detail tables [Office development in Visual Studio], walkthroughs
- data caching [Office development in Visual Studio], Master/Detail Relation
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: de7bf3ba34a2a7dd3e7db9ff549e4a839800d524
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97524873"
---
# <a name="walkthrough-create-a-master-detail-relation-using-a-cached-dataset"></a>チュートリアル: キャッシュされたデータセットを使用したマスター詳細関係の作成
  このチュートリアルでは、ワークシートでマスター/詳細関係を作成し、ソリューションをオフラインで使用できるようにデータをキャッシュする方法について説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートにコントロールを追加します。

- ワークシートにキャッシュするデータセットを設定します。

- レコードのスクロールを有効にするコードを追加します。

- プロジェクトをテストします。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプルデータベースへのアクセス。 データベースは、開発用コンピューターまたはサーバー上に配置できます。

- SQL Server データベースに対する読み取りと書き込みの権限。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、Excel ブックプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# のいずれかを使用して、 **[My Master-Detail**] という名前の Excel ブックプロジェクトを作成します。 [ **新しいドキュメントを作成** する。 詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

   新しい Excel ブックがデザイナーで開き、 **[My Master-Detail** ] プロジェクトが **ソリューションエクスプローラー** に追加されます。

## <a name="create-the-data-source"></a>データソースを作成する
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [   >  **他の Windows**  >  **データソース** の表示] をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. [ **データベース** ] を選択し、[ **次へ**] をクリックします。

4. Northwind サンプル SQL Server データベースへのデータ接続を選択するか、[ **新しい接続** ] ボタンを使用して新しい接続を追加します。

5. 接続を選択または作成したら、[ **次へ**] をクリックします。

6. 選択されている場合は、接続を保存するオプションをオフにして、[ **次へ**] をクリックします。

7. [**データベースオブジェクト**] ウィンドウで、[**テーブル**] ノードを展開します。

8. **Orders** テーブルと **Order Details** テーブルを選択します。

9. **[完了]** をクリックします。

   2つのテーブルが [ **データソース** ] ウィンドウに追加されます。 また、 **ソリューションエクスプローラー** に表示される、型指定されたデータセットをプロジェクトに追加します。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 この手順では、名前付き範囲、リストオブジェクト、および2つのボタンを最初のワークシートに追加します。 まず、[ **データソース** ] ウィンドウから名前付き範囲とリストオブジェクトを追加して、自動的にデータソースにバインドされるようにします。 次に、[ **ツールボックス**] からボタンを追加します。

### <a name="to-add-a-named-range-and-a-list-object"></a>名前付き範囲とリストオブジェクトを追加するには

1. **Sheet1** が表示された状態で、Visual Studio デザイナーで **[My Master-Detail.xlsx** ] ブックが開いていることを確認します。

2. [ **データソース** ] ウィンドウを開き、[ **Orders** ] ノードを展開します。

3. [ **OrderID** ] 列を選択し、表示されるドロップダウン矢印をクリックします。

4. ドロップダウンリストで [ **NamedRange** ] をクリックし、 **OrderID** 列をセル **A2** にドラッグします。

     <xref:Microsoft.Office.Tools.Excel.NamedRange>という名前のコントロール `OrderIDNamedRange` がセル **A2** に作成されます。 同時に、と <xref:System.Windows.Forms.BindingSource> いう名前 `OrdersBindingSource` のテーブルアダプターと <xref:System.Data.DataSet> インスタンスがプロジェクトに追加されます。 コントロールは、にバインドされ <xref:System.Windows.Forms.BindingSource> 、さらにインスタンスにバインドされ <xref:System.Data.DataSet> ます。

5. **Orders** テーブルの下にある列を下にスクロールします。 一覧の一番下には、 **Order Details** テーブルがあります。これは、 **Orders** テーブルの子であるためです。 **Orders** テーブルと同じレベルにある [ **Order Details** ] テーブルを選択し、表示されるドロップダウン矢印をクリックします。

6. ドロップダウンリストで [ **ListObject** ] をクリックし、 **OrderDetails** テーブルをセル **A6** にドラッグします。

7. <xref:Microsoft.Office.Tools.Excel.ListObject> **Order_DetailsListObject** という名前のコントロールがセル **A6** に作成され、にバインドされ <xref:System.Windows.Forms.BindingSource> ます。

### <a name="to-add-two-buttons"></a>2つのボタンを追加するには

1. **ツールボックス** の [**コモンコントロール**] タブから、 <xref:System.Windows.Forms.Button> ワークシートのセル **A3** にコントロールを追加します。

    このボタンにはという名前が付けら `Button1` れます。

2. <xref:System.Windows.Forms.Button>ワークシートのセル **B3** に別のコントロールを追加します。

    このボタンにはという名前が付けら `Button2` れます。

   次に、ドキュメントにキャッシュするデータセットをマークします。

## <a name="cache-the-dataset"></a>データセットをキャッシュする
 データセットをパブリックにして、 **CacheInDocument** プロパティを設定することにより、ドキュメントにキャッシュされるデータセットをマークします。

### <a name="to-cache-the-dataset"></a>データセットをキャッシュするには

1. コンポーネントトレイの [ **NorthwindDataSet** ] を選択します。

2. [ **プロパティ** ] ウィンドウで、[ **修飾子** ] プロパティを **Public** に変更します。

    データセットは、キャッシュが有効になる前にパブリックである必要があります。

3. **CacheInDocument** プロパティを **True** に変更します。

   次の手順では、ボタンにテキストを追加し、C# ではイベントハンドラーをフックするコードを追加します。

## <a name="initialize-the-controls"></a>コントロールを初期化します
 ボタンテキストを設定し、イベントの発生時にイベントハンドラーを追加し <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> ます。

### <a name="to-initialize-the-data-and-the-controls"></a>データとコントロールを初期化するには

1. **ソリューションエクスプローラー** で、[ **Sheet1** ] または [ **Sheet1.cs**] を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. 次のコードをメソッドに追加して、 `Sheet1_Startup` ボタンのテキストを設定します。

     [!code-vb[Trin_VstcoreDataExcel#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#15)]
     [!code-csharp[Trin_VstcoreDataExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#15)]

3. C# の場合のみ、ボタンクリックイベントのイベントハンドラーをメソッドに追加し `Sheet1_Startup` ます。

     [!code-csharp[Trin_VstcoreDataExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#16)]

## <a name="add-code-to-enable-scrolling-through-the-records"></a>レコードのスクロールを有効にするコードを追加する
 <xref:System.Windows.Forms.Control.Click>各ボタンのイベントハンドラーにコードを追加して、レコード間を移動します。

### <a name="to-scroll-through-the-records"></a>レコードをスクロールするには

1. のイベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> `Button1` し、次のコードを追加してレコードを後方に移動します。

     [!code-vb[Trin_VstcoreDataExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#17)]
     [!code-csharp[Trin_VstcoreDataExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#17)]

2. イベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> し、 `Button2` 次のコードを追加してレコードを事前に処理します。

     [!code-vb[Trin_VstcoreDataExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#18)]
     [!code-csharp[Trin_VstcoreDataExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#18)]

## <a name="test-the-application"></a>アプリケーションをテストする
 ブックをテストして、データが想定どおりに表示されること、およびオフラインでソリューションを使用できることを確認できるようになりました。

### <a name="to-test-the-data-caching"></a>データキャッシュをテストするには

1. **F5** キーを押します。

2. 名前付き範囲とリストオブジェクトに、データソースからのデータが格納されていることを確認します。

3. ボタンをクリックして、レコードの一部をスクロールします。

4. ブックを保存し、ブックと Visual Studio を閉じます。

5. データベースへの接続を無効にします。 データベースがサーバーに配置されている場合は、コンピューターからネットワークケーブルを取り外します。または、データベースが開発用コンピューター上にある場合は、SQL Server サービスを停止します。

6. Excel を開き、 *\bin* ディレクトリ (C# では *\My Master-Detail\bin* in Visual Basic または *\My Master-Detail\bin\debug* ) から **[My Master-Detail.xlsx** ] を開きます。

7. 一部のレコードをスクロールして、接続が切断されたときにワークシートが正常に動作することを確認します。

8. データベースに再接続します。 データベースがサーバーに配置されている場合は、もう一度コンピューターをネットワークに接続します。または、データベースが開発用コンピューター上にある場合は、SQL Server サービスを開始します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、ワークシートでマスター/詳細データリレーションシップを作成し、データセットをキャッシュする方法の基本について説明します。 ここでは、次の作業を行います。

- ソリューションを展開する。 詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office ソリューションのデータ](../vsto/data-in-office-solutions.md)
- [キャッシュ データ](../vsto/caching-data.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
