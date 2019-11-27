---
title: 'チュートリアル: WPF アプリケーションでの関連データの表示 |Microsoft Docs'
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
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 5c48f188-e9c4-40a6-97d9-67cdb2f90127
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 787be52eeb546d2ab184a172464862d10cb43288
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299583"
---
# <a name="walkthrough-displaying-related-data-in-a-wpf-application"></a>チュートリアル: WPF アプリケーションでの関連データの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、親/子リレーションシップを持つデータベーステーブルのデータを表示する WPF アプリケーションを作成します。 データは、Entity Data Model 内のエンティティにカプセル化されます。 親エンティティには、一連の注文の概要情報が含まれています。 このエンティティの各プロパティは、アプリケーション内の別のコントロールにバインドされます。 子エンティティには、各注文の詳細が含まれます。 この一連のデータは、<xref:System.Windows.Controls.DataGrid> コントロールにバインドされます。

 このチュートリアルでは、次の作業について説明します。

- WPF アプリケーションと、AdventureWorksLT サンプルデータベースのデータから生成される Entity Data Model を作成します。

- 一連の注文の概要情報を表示するデータバインドコントロールのセットを作成する。 コントロールを作成するには、 **[データソース]** ウィンドウから**WPF デザイナー**に親エンティティをドラッグします。

- 選択された各注文に関連する詳細を表示する <xref:System.Windows.Controls.DataGrid> コントロールを作成します。 コントロールを作成するには、 **[データソース]** ウィンドウから**WPF デザイナー**のウィンドウに子エンティティをドラッグします。

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で初期化します。

- AdventureWorksLT サンプル データベースが添付された、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorksLT データベースは、 [CodePlex Web サイト](https://go.microsoft.com/fwlink/?linkid=87843)からダウンロードできます。

  次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- Entity Data Model および ADO.NET Entity Framework。 詳細については、「 [Entity Framework の概要](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0)」を参照してください。

- WPF デザイナーの操作。 詳細については、「 [WPF と Silverlight デザイナーの概要](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)」を参照してください。

- WPF データ バインディング。 詳しくは、「 [データ バインディングの概要](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)」をご覧ください。

## <a name="creating-the-project"></a>プロジェクトの作成
 新しい WPF プロジェクトを作成して注文レコードを表示します。

#### <a name="to-create-a-new-wpf-project"></a>新しい WPF プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. **[ビジュアルC# ]** または **[Visual Basic]** を展開し、 **[Windows]** を選択します。

4. ダイアログボックスの上部にあるコンボボックスで **.NET Framework 4**が選択されていることを確認します。 このチュートリアルで使用する <xref:System.Windows.Controls.DataGrid> コントロールは、.NET Framework 4 でのみ使用できます。

5. **[WPF アプリケーション]** プロジェクト テンプレートを選択します。

6. **[名前]** ボックスに「`AdventureWorksOrdersViewer`」と入力します。

7. **[OK]** をクリックすると、

     Visual Studio によって `AdventureWorksOrdersViewer` プロジェクトが作成されます。

## <a name="creating-an-entity-data-model-for-the-application"></a>アプリケーションの Entity Data Model を作成する
 データ バインド コントロールを作成するには、まず、アプリケーション用のデータ モデルを定義し、 **[データ ソース]** ウィンドウに追加する必要があります。 このチュートリアルでは、データモデルは Entity Data Model です。

#### <a name="to-create-an-entity-data-model"></a>Entity Data Model を作成するには

1. **[データ]** メニューの **[新しいデータソースの追加]** をクリックして、**データソース構成ウィザード**を開きます。

2. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

3. **[データベースモデルの選択]** ページで、 **[Entity Data Model]** をクリックし、 **[次へ]** をクリックします。

4. **[モデルのコンテンツの選択]** ページで、 **[データベースから生成]** をクリックし、 **[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

   - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択します。

      または

   - **[新しい接続]** をクリックし、AdventureWorksLT データベースへの接続を作成します。

     **[エンティティ接続設定に名前を付けて app.config に保存]** オプションが選択されていることを確認し、 **[次へ]** をクリックします。

6. **[データベースオブジェクトの選択]** ページで、 **[テーブル]** を展開し、次のテーブルを選択します。

   - **SalesOrderDetail**

   - **SalesOrderHeader**

7. **[完了]** をクリックします。

8. プロジェクトをビルドする。

## <a name="creating-data-bound-controls-that-display-the-orders"></a>注文を表示するデータバインドコントロールの作成
 **[データソース]** ウィンドウから WPF デザイナーに `SalesOrderHeaders` エンティティをドラッグして、注文レコードを表示するコントロールを作成します。

#### <a name="to-create-data-bound-controls-that-display-the-order-records"></a>注文レコードを表示するデータバインドコントロールを作成するには

1. **ソリューションエクスプローラー**で、mainwindow.xaml をダブルクリックします。

    WPF デザイナーでウィンドウが開きます。

2. XAML を編集して、 **Height**プロパティと**Width**プロパティを800に設定します。

3. **[データソース]** ウィンドウで、[ **[salesorderheaders]** ] ノードのドロップダウンメニューをクリックし、 **[詳細]** をクリックします。

4. **[SalesOrderHeaders]** ノードを展開します。

5. **[Salesorderid]** の横にあるドロップダウンメニューをクリックし、 **[ComboBox]** を選択します。

6. **[Salesorderheaders]** ノードの次の各子ノードについて、ノードの横にあるドロップダウンメニューをクリックし、 **[なし]** を選択します。

   - **RevisionNumber**

   - **OnlineOrderFlag**

   - **ShipToAddressID**

   - **BillToAddressID**

   - **CreditCardApprovalCode**

   - **小計**

   - **TaxAmt**

   - **おける**

   - **rowguid**

   - **ModifiedDate**

     この操作は、次の手順において、これらのノードに対応するデータ バインド コントロールが Visual Studio で作成されるのを防ぎます。 このチュートリアルでは、これらのデータをエンド ユーザーが参照する必要はありません。

7. **[データソース]** ウィンドウで、[ **[salesorderheaders]** ] ノードを**WPF デザイナー**のウィンドウにドラッグします。

    Visual Studio では、 **[salesorderheaders]** エンティティ内のデータにバインドされるコントロールのセットと、データを読み込むコードを作成する XAML が生成されます。 生成される XAML とコードの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

8. デザイナーで、 **Sales ORDER ID**ラベルの横にあるコンボボックスをクリックします。

9. **[プロパティ]** ウィンドウで、**IsReadOnly** プロパティの横のチェック ボックスをオンにします。

## <a name="creating-a-datagrid-that-displays-the-order-details"></a>注文の詳細を表示する DataGrid の作成
 **[データソース]** ウィンドウから WPF デザイナーに `SalesOrderDetails` エンティティをドラッグして、注文の詳細を表示する <xref:System.Windows.Controls.DataGrid> コントロールを作成します。

#### <a name="to-create-a-datagrid-that-displays-the-order-details"></a>注文の詳細を表示する DataGrid を作成するには

1. **[データソース]** ウィンドウで、 **[salesorderheaders]** ノードの子である**SalesOrderDetails**ノードを探します。

   > [!NOTE]
   > また、 **[salesorderheaders]** ノードのピアである**SalesOrderDetails**ノードもあります。 [ **[Salesorderheaders]** ] ノードの子ノードが選択されていることを確認します。

2. 子**SalesOrderDetails**ノードを展開します。

3. **SalesOrderDetails**ノードの次の各子ノードについて、ノードの横にあるドロップダウンメニューをクリックし、 **[なし]** を選択します。

   - **SalesOrderID**

   - **SalesOrderDetailID**

   - **rowguid**

   - **ModifiedDate**

     この操作により、Visual Studio は、次の手順で作成する <xref:System.Windows.Controls.DataGrid> コントロールにこのデータを含めないようにします。 このチュートリアルでは、これらのデータをエンド ユーザーが参照する必要はありません。

4. **[データソース]** ウィンドウで、子**SALESORDERDETAILS**ノードを**WPF デザイナー**のウィンドウにドラッグします。

    Visual Studio によって、新しいデータバインド <xref:System.Windows.Controls.DataGrid> コントロールを定義する XAML が生成され、コントロールがデザイナーに表示されます。 また、Visual Studio は、分離コードファイルの生成された `GetSalesOrderHeadersQuery` メソッドを更新して、 **SalesOrderDetails**エンティティにデータを含めます。

## <a name="testing-the-application"></a>アプリケーションのテスト
 アプリケーションをビルドして実行し、注文レコードが表示されていることを確認します。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. **F5**キーを押します。

     アプリケーションがビルドされ、実行されます。 次のことを検証します。

    - **[Sales ORDER ID]** コンボボックスには、 **71774**が表示されます。 これは、エンティティの最初の注文 ID です。

    - **[Sales ORDER ID]** コンボボックスで選択した注文ごとに、詳細な注文情報が <xref:System.Windows.Controls.DataGrid>に表示されます。

2. アプリケーションを終了します。

## <a name="next-steps"></a>次の手順
 このチュートリアルを完了した後、Visual Studio の **[データソース]** ウィンドウを使用して、WPF コントロールを他の種類のデータソースにバインドする方法について説明します。 詳細については、「 [WCF データサービスへの wpf コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)」および「[データセットへの Wpf コントロールのバインド](../data-tools/bind-wpf-controls-to-a-dataset.md)」を参照してください。

## <a name="see-also"></a>関連項目
 [Visual Studio でのデータへの wpf コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [wpf アプリケーションでの関連データの表示](../data-tools/display-related-data-in-wpf-applications.md)