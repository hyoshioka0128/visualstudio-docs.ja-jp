---
title: トランザクションにデータを保存する |Microsoft Docs
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
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b30f51da001c62166a97c954b1416e35fd8b540f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671086"
---
# <a name="save-data-in-a-transaction"></a>トランザクションにデータを保存する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、名前空間を使用してトランザクションにデータを保存する方法について説明 <xref:System.Transactions> します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。

## <a name="prerequisites"></a>前提条件
 このチュートリアルでは、Northwind サンプル データベースへのアクセスが必要です。

## <a name="create-a-windows-application"></a>Windows アプリケーションを作成する
 最初の手順では、 **Windows アプリケーション**を作成します。

#### <a name="to-create-the-new-windows-project"></a>新しい Windows プロジェクトを作成するには

1. Visual Studio の [ **ファイル** ] メニューで、新しい **プロジェクト**を作成します。

2. プロジェクトに **SavingDataInATransactionWalkthrough**という名前を指定します。

3. [ **Windows アプリケーション**] を選択し、[ **OK]** を選択します。 詳細については、「 [クライアントアプリケーション](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)」を参照してください。

     **SavingDataInATransactionWalkthrough** プロジェクトが作成されて**ソリューション エクスプローラー**に追加されます。

## <a name="create-a-database-data-source"></a>データベースデータソースの作成
 この手順では、 [データソース構成ウィザード](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) を使用して、 `Customers` Northwind サンプルデータベースのテーブルとテーブルに基づいてデータソースを作成し `Orders` ます。

#### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. [ **データ** ] メニューの [**データソースの表示**] をクリックします。

2. [ **データソース** ] ウィンドウで [ **新しいデータソースの追加** ] を選択して、 **データソース構成ウィザード**を開始します。

3. [ **データソースの種類を選択**] 画面で、[ **データベース**] を選択し、[ **次へ**] を選択します。

4. [ **データ接続の選択**] 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         - または -

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示し、Northwind データベースへの接続を作成します。

5. データベースにパスワードが必要な場合は、機密データを含めるオプションを選択し、[ **次へ**] を選択します。

6. [ **アプリケーション構成ファイルへの接続文字列の保存** ] 画面で、[ **次へ**] を選択します。

7. [ **データベースオブジェクトの選択** ] 画面で、[ **テーブル** ] ノードを展開します。

8. `Customers`テーブルとテーブルを選択し、[ `Orders` **完了**] を選択します。

     **NorthwindDataSet**がプロジェクトに追加され、 `Customers` テーブルとテーブルが [ `Orders` **データソース**] ウィンドウに表示されます。

## <a name="addcontrols-to-the-form"></a>Addcontrols をフォームに追加します。
 データバインドコントロールを作成するには、[ **データソース** ] ウィンドウからフォームに項目をドラッグします。

#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>Windows フォームにデータバインドコントロールを作成するには

- [ **データソース** ] ウィンドウで、[ **Customers** ] ノードを展開します。

- **[データ ソース]** ウィンドウから **Form1** にメインの **[Customers]** ノードをドラッグします。

     レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

- 関連する [ **orders** ] ノード (メインの [ **orders** ] ノードではなく、[ **Fax** ] 列の下にある [関連する子テーブル] ノード) を、[顧客] の [ **datagridview**] の下のフォームにドラッグします。

     <xref:System.Windows.Forms.DataGridView> がフォームに表示されます。 OrdersTableAdapter とが <xref:System.Windows.Forms.BindingSource> コンポーネントトレイに表示されます。

## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>System.string アセンブリへの参照を追加します。
 トランザクションは、<xref:System.Transactions> 名前空間を使用します。 既定では、システムのトランザクションアセンブリへのプロジェクト参照は追加されないため、手動で追加する必要があります。

#### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>System.Transactions の DLL ファイルへの参照を追加するには

1. [ **プロジェクト** ] メニューの [**参照の追加**] をクリックします。

2. [ **.Net** ] タブで [ **system.string] を選択し**、[ **OK]** を選択します。

     **System.Transactions** への参照がプロジェクトに追加されます。

## <a name="modifythe-code-in-the-bindingnavigators-saveitem-button"></a>BindingNavigator の saveitem ボタンのコードの modify
 フォームに最初にドロップされたテーブルに対しては、 `click` の [保存] ボタンのイベントに既定でコードが追加され <xref:System.Windows.Forms.BindingNavigator> ます。 追加テーブルを更新する場合は、手動でコードを追加する必要があります。 このチュートリアルでは、[保存] ボタンのクリックイベントハンドラーから既存の保存コードをリファクターします。また、行を追加または削除する必要があるかどうかに基づいて、特定の更新機能を提供するためのメソッドもいくつか作成します。

#### <a name="to-modify-the-auto-generated-save-code"></a>自動生成された保存コードを変更するには

1. **顧客 Sbindingnavigator**の [**保存**] ボタン (フロッピーディスクのアイコンが付いたボタン) を選択します。

2. `CustomersBindingNavigatorSaveItem_Click` メソッドを次のコードに置き換えます。

    [!code-csharp[VbRaddataSaving#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#4)]
    [!code-vb[VbRaddataSaving#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#4)]

   関連するデータへの変更を解決する順序は次のとおりです。

- 子レコードを削除します。 (この場合は、テーブルからレコードを削除 `Orders` します)。

- 親レコードを削除します。 (この場合は、テーブルからレコードを削除 `Customers` します)。

- 親レコードを挿入します。(この場合は、テーブルにレコードを挿入 `Customers` します。)

- 子レコードを挿入します。 (この場合は、テーブルにレコードを挿入 `Orders` します。)

#### <a name="to-delete-existing-orders"></a>既存の注文を削除するには

- 次の `DeleteOrders` メソッドを **Form1** に追加します。

     [!code-csharp[VbRaddataSaving#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#5)]
     [!code-vb[VbRaddataSaving#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#5)]

#### <a name="to-delete-existing-customers"></a>既存の顧客を削除するには

- 次の `DeleteCustomers` メソッドを **Form1** に追加します。

     [!code-csharp[VbRaddataSaving#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#6)]
     [!code-vb[VbRaddataSaving#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#6)]

#### <a name="to-add-new-customers"></a>新規顧客を追加するには

- 次の `AddNewCustomers` メソッドを **Form1** に追加します。

     [!code-csharp[VbRaddataSaving#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#7)]
     [!code-vb[VbRaddataSaving#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#7)]

#### <a name="to-add-new-orders"></a>新規注文を追加するには

- 次の `AddNewOrders` メソッドを **Form1** に追加します。

     [!code-csharp[VbRaddataSaving#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#8)]
     [!code-vb[VbRaddataSaving#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#8)]

## <a name="run-the-application"></a>アプリケーションの実行

#### <a name="to-run-the-application"></a>アプリケーションを実行するには

- **F5 キーを押し**てアプリケーションを実行します。

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
