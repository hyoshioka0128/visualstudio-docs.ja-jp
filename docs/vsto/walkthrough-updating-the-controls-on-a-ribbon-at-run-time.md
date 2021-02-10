---
title: 'チュートリアル: 実行時にリボンのコントロールを更新する'
description: リボンが Office アプリケーションに読み込まれた後に、リボンオブジェクトモデルを使用してリボン上のコントロールを更新する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- updating Ribbon controls
- Ribbon [Office development in Visual Studio], dynamic menu
- dynamic menus [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 181fafeb55720b5a97a635a4c2322cf7343643d3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937187"
---
# <a name="walkthrough-update-the-controls-on-a-ribbon-at-run-time"></a>チュートリアル: 実行時にリボンのコントロールを更新する

このチュートリアルでは、リボンオブジェクトモデルを使用して、リボンが Office アプリケーションに読み込まれた後で、リボン上のコントロールを更新する方法について説明します。

[!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

この例では、Northwind サンプル データベースからデータを取得し、Microsoft Office Outlook のコンボ ボックスとメニューに読み込みます。 これらのコントロールで選択した項目によっ **て、などのフィールド****が** 自動的に電子メールメッセージに入力されます。

このチュートリアルでは、次の作業について説明します。

- 新しい Outlook VSTO アドインプロジェクトを作成します。

- カスタムリボングループをデザインします。

- 組み込みタブにカスタムグループを追加します。

- 実行時にリボンのコントロールを更新します。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドインプロジェクトを作成する

まず、Outlook VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、 **Ribbon_Update_At_Runtime** という名前の Outlook VSTO アドインプロジェクトを作成します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。

3. プロジェクトを既定のプロジェクト ディレクトリに保存します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

## <a name="design-a-custom-ribbon-group"></a>カスタムリボングループのデザイン

この例のリボンは、ユーザーが新しいメールメッセージを作成したときに表示されます。 リボンのカスタムグループを作成するには、まず、プロジェクトにリボン項目を追加し、次にリボンデザイナーでそのグループをデザインします。 このカスタムグループを使用すると、データベースから名前を取得し、履歴を注文して、フォローアップ電子メールメッセージを顧客に生成するのに役立ちます。

### <a name="to-design-a-custom-group"></a>カスタム グループをデザインするには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** をクリックします。

3. 新しいリボンの名前を [顧客] **リボン** に変更し、[ **追加**] をクリックします。

     リボンデザイナーで CustomerRibbon.cs またはファイルが開き、既定のタブとグループが表示され *ます。*

4. リボン デザイナーをクリックして選択します。

5. [ **プロパティ** ] ウィンドウで、[ **ribbontype** ] プロパティの横にあるドロップダウン矢印をクリックし、[ **Microsoft**] をクリックします。

     これにより、ユーザーが Outlook で新しいメールメッセージを作成したときにリボンが表示されるようになります。

6. リボンデザイナーで、[ **Group1** ] をクリックして選択します。

7. [ **プロパティ** ] ウィンドウで、[ **ラベル** ] を「 **Customer 購入**」に設定します。

8. **ツールボックス** の [ **Office リボンコントロール**] タブから、 **ComboBox** を **Customer 購入** グループにドラッグします。

9. [ **ComboBox1** ] をクリックして選択します。

10. [ **プロパティ** ] ウィンドウで、[ **ラベル** ] を「 **Customers**」に設定します。

11. **ツールボックス** の [ **Office リボンコントロール**] タブから、**メニュー** を **Customer 購入** グループにドラッグします。

12. [ **プロパティ** ] ウィンドウで、[ **ラベル** ] を「 **製品購入**」に設定します。

13. **Dynamic** を **true** に設定します。

     これにより、リボンが Office アプリケーションに読み込まれた後に、実行時にメニューのコントロールを追加および削除できます。

## <a name="add-the-custom-group-to-a-built-in-tab"></a>組み込みタブへのカスタムグループの追加

組み込みタブは、Outlook エクスプローラーまたはインスペクターのリボン上に既にあるタブです。 この手順では、組み込みタブにカスタム グループを追加し、タブ上のカスタム グループの位置を指定します。

### <a name="to-add-the-custom-group-to-a-built-in-tab"></a>組み込みタブにカスタム グループを追加するには

1. [ **Tabaddins (組み込み)** ] タブをクリックして選択します。

2. [ **プロパティ** ] ウィンドウで、[ **ControlId** ] プロパティを展開し、[ **officeid** ] を **TabNewMailMessage** に設定します。

     これにより、 **顧客の購入** グループが、新しいメールメッセージに表示されるリボンの [ **メッセージ** ] タブに追加されます。

3. [ **顧客の購入** ] グループをクリックして選択します。

4. [ **プロパティ** ] ウィンドウで、 **Position** プロパティを展開し、 **positiontype** プロパティの横にあるドロップダウン矢印をクリックして、[ **beforeofficeid**] をクリックします。

5. **Officeid** プロパティを **groupclipboard** に設定します。

     これにより、[**メッセージ**] タブの [**クリップボード**] グループの前に **顧客の購入** グループが配置されます。

## <a name="create-the-data-source"></a>データソースを作成する

**[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

     **データソース構成ウィザード** が起動します。

2. [ **データベース**] を選択し、[ **次へ**] をクリックします。

3. [ **データセット**] を選択し、[ **次へ**] をクリックします。

4. Northwind サンプル Microsoft SQL Server Compact 4.0 データベースへのデータ接続を選択するか、[ **新しい接続** ] ボタンを使用して新しい接続を追加します。

5. 接続を選択または作成したら、[ **次へ**] をクリックします。

6. [ **次へ** ] をクリックして、接続文字列を保存します。

7. [ **データベースオブジェクトの選択** ] ページで、[ **テーブル**] を展開します。

8. 次の各テーブルの横にあるチェック ボックスをオンにします。

    1. **企業**

    2. **注文の詳細**

    3. **Orders**

    4. **製品**

9. **[Finish]** をクリックします。

## <a name="update-controls-in-the-custom-group-at-run-time"></a>実行時にカスタムグループのコントロールを更新する

リボン オブジェクト モデルを使用して、以下のタスクを実行します。

- 顧客名を **Customers** コンボボックスに追加します。

- 購入した販売注文と製品を表すメニューおよびボタンコントロールを [購入した **製品** ] メニューに追加します。

- [ **顧客** ] コンボボックスと [購入した **製品** ] メニューのデータを使用して、新しいメールメッセージの [宛先]、[件名]、および [本文] フィールドを設定します。

### <a name="to-update-controls-in-the-custom-group-by-using-the-ribbon-object-model"></a>リボン オブジェクト モデルを使用してカスタム グループのコントロールを更新するには

1. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

2. [ **参照の追加** ] ダイアログボックスで、[ **.net** ] タブをクリックし、[system.string **] アセンブリを** 選択して [ **OK**] をクリックします。

    このアセンブリには、統合言語クエリ (LINQ) を使用するためのクラスが含まれています。 ここでは、LINQ を使用して Northwind データベースから取得したデータをカスタム グループのコントロールに読み込みます。

3. **ソリューションエクスプローラー** で、 **CustomerRibbon.cs** または **顧客のリボン** をクリックして選択します。

4. **[表示]** メニューの **[コード]** をクリックします。

    コード エディターでリボン コード ファイルが開きます。

5. リボン コード ファイルの先頭に次のステートメントを追加します。 これらのステートメントによって、LINQ 名前空間や Outlook プライマリ相互運用機能アセンブリ (PIA) の名前空間に簡単にアクセスできます。

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#1](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#1)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#1](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#1)]

6. クラス内に次のコードを追加し `CustomerRibbon` ます。 このコードは、Northwind データベースの Customer、Orders、Order Details、および Product テーブルから取得した情報を格納するために使用するデータ テーブルおよびテーブル アダプターを宣言します。

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#2](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#2)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#2](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#2)]

7. `CustomerRibbon` クラスに次のコード ブロックを追加します。 このコードは、実行時にリボンのコントロールを作成する3つのヘルパーメソッドを追加します。

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#3](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#3)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#3](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#3)]

8. `CustomerRibbon_Load` イベント ハンドラー メソッドを次のコードで置き換えます。 このコードは、LINQ クエリを使用して以下のタスクを実行します。

   - Northwind データベースの20人の顧客の ID と名前を使用して、 **customers** コンボボックスにデータを入力します。

   - `PopulateSalesOrderInfo` ヘルパー メソッドを呼び出す。 このメソッドは、現在選択されている顧客に関連する販売注文番号で **products purchased** メニューを更新します。

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#4](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#4)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#4](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#4)]

9. 次のコードを `CustomerRibbon` クラスに追加します。 このコードは、LINQ クエリを使用して以下のタスクを実行します。

   - 選択した顧客に関連する各販売注文の **products purchased** メニューにサブメニューを追加します。

   - 販売注文に関連する製品を示すボタンを各サブメニューに追加する。

   - 各ボタンにイベントハンドラーを追加する。

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#6](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#6)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#6](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#6)]

10. **ソリューションエクスプローラー** で、リボンコードファイルをダブルクリックします。

     リボン デザイナーが開きます。

11. リボンデザイナーで、[ **Customers** ] コンボボックスをダブルクリックします。

     リボン コード ファイルがコード エディターで開き、`ComboBox1_TextChanged` イベント ハンドラーが表示されます。

12. `ComboBox1_TextChanged` イベント ハンドラーを次のコードで置き換えます。 このコードは、以下のタスクを実行します。

    - `PopulateSalesOrderInfo` ヘルパー メソッドを呼び出す。 このメソッドは、[購入した **製品** ] メニューを、選択した顧客に関連する販売注文に更新します。

    - `PopulateMailItem` ヘルパー メソッドを呼び出し、現在のテキスト (つまり、選択されている顧客の名前) を渡します。 このメソッドは、新しいメールメッセージの [宛先]、[件名]、および [本文] フィールドを設定します。

      [!code-csharp[Trin_Ribbon_Update_At_Runtime#5](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#5)]
      [!code-vb[Trin_Ribbon_Update_At_Runtime#5](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#5)]

13. 次の `Click` イベント ハンドラーを `CustomerRibbon` クラスに追加します。 このコードは、選択した製品の名前を新しいメールメッセージの本文フィールドに追加します。

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#8](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#8)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#8](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#8)]

14. 次のコードを `CustomerRibbon` クラスに追加します。 このコードは、以下のタスクを実行します。

    - 現在選択されている顧客の電子メールアドレスを使用して、新しいメールメッセージの行をに設定します。

    - 新しいメールメッセージの [件名] フィールドと [本文] フィールドにテキストを追加します。

      [!code-csharp[Trin_Ribbon_Update_At_Runtime#7](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#7)]
      [!code-vb[Trin_Ribbon_Update_At_Runtime#7](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#7)]

## <a name="test-the-controls-in-the-custom-group"></a>カスタムグループのコントロールをテストする

Outlook で新しいメールフォームを開くと、 **Customer 購入** という名前のカスタムグループがリボンの [ **メッセージ** ] タブに表示されます。

顧客のフォローアップ電子メールメッセージを作成するには、顧客を選択し、顧客が購入した製品を選択します。 **顧客の購入** グループ内のコントロールは、実行時に Northwind データベースのデータと共に更新されます。

### <a name="to-test-the-controls-in-the-custom-group"></a>カスタム グループのコントロールをテストするには

1. **F5** キーを押して、プロジェクトを実行します。

     Outlook が起動します。

2. Outlook で、[ **ファイル** ] メニューの [ **新規作成**] をポイントし、[ **メールメッセージ**] をクリックします。

     次のアクションが発生します。

    - 新しいメール メッセージのインスペクター ウィンドウが表示されます。

    - リボンの [**メッセージ**] タブで、**クリップボード** グループの前に **顧客の購入** グループが表示されます。

    - グループ内の **customers** コンボボックスは、Northwind データベース内の顧客の名前で更新されます。

3. リボンの [ **メッセージ** ] タブの [顧客の **購入** ] グループで、 **[顧客] コンボボックス** から顧客を選択します。

     次のアクションが発生します。

    - [ **購入** した製品] メニューが更新され、選択した顧客の各販売注文が表示されます。

    - 個々の販売注文サブメニューが、その注文で購入された商品を示すように更新されます。

    - 選択した顧客の電子メールアドレスがメールメッセージの [ **宛先** ] 行に追加され、メールメッセージの件名と本文にテキストが入力されます。

4. [ **製品の購入** ] メニューをクリックし、任意の販売注文をポイントして、販売注文の製品をクリックします。

     製品の名前がメール メッセージの本文に追加されます。

## <a name="next-steps"></a>次のステップ

Office UI をカスタマイズする方法の詳細については、次のトピックで説明します。

- ドキュメント レベルのカスタマイズにコンテキスト ベースの UI を追加する。 詳細については、「 [操作ウィンドウの概要](../vsto/actions-pane-overview.md)」を参照してください。

- 標準またはカスタムの Microsoft Office Outlook フォームを拡張する。 詳細については、「 [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)」を参照してください。

- Outlook にカスタム作業ウィンドウを追加する。 詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [統合言語クエリ (LINQ: Language-Integrated Query)](/dotnet/csharp/linq/index)
- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [リボンオブジェクトモデルの概要](../vsto/ribbon-object-model-overview.md)
- [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)
- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)
- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [方法: リボンをリボンデザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: アドインのユーザーインターフェイスエラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)