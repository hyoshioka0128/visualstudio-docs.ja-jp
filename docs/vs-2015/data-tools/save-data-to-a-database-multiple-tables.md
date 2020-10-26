---
title: データベースへのデータの保存 (複数のテーブル) |Microsoft Docs
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
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c5c4d5fc73660c97bcb69957a93d2ff08f64e31c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655458"
---
# <a name="save-data-to-a-database-multiple-tables"></a>データベースへのデータの保存 (複数テーブル)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーション開発における最も一般的なシナリオの 1 つに、Windows アプリケーションのフォームにデータを表示して編集し、更新したデータをデータベースに返送する操作があります。 このチュートリアルでは、2 つの関連するテーブルのデータを表示するフォームを作成し、レコードを編集して変更内容をデータベースに保存する方法を示します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。

 アプリケーション内のデータをデータベースに保存するには、TableAdapter の `Update` メソッドを呼び出します。 [ **データソース** ] ウィンドウからフォームにテーブルをドラッグすると、データを保存するために必要なコードが自動的に追加されます。フォームに追加されるテーブルでは、このコードを手動で追加する必要があります。 ここでは、複数のテーブルから更新を保存するコードを追加する手順を示します。

> [!NOTE]
> 表示されるダイアログボックスとメニューコマンドは、アクティブな設定や使用しているエディションによっては、ヘルプに記載されているものと異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

 このチュートリアルでは、以下のタスクを行います。

- 新しい **Windows アプリケーション** プロジェクトを作成しています。

- [データソース構成ウィザード](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)を使用して、アプリケーションでのデータソースの作成と構成を行います。

- [ [データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)の項目のコントロールを設定します。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

- データセット内の各テーブルのいくつかのレコードを変更する。

- データセット内の更新されたデータをデータベースに返送するコードを変更します。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを完了するための要件は次のとおりです。

- Northwind サンプル データベースにアクセスします。

## <a name="create-the-windows-application"></a>Windows アプリケーションを作成する
 最初の手順では、 **Windows アプリケーション**を作成します。 この手順では、プロジェクトへの名前の割り当ては省略可能ですが、後で保存することを計画しているため、名前を付けます。

#### <a name="to-create-the-new-windows-application-project"></a>新しい Windows アプリケーションプロジェクトを作成するには

1. [ **ファイル** ] メニューで、新しいプロジェクトを作成します。

2. プロジェクトに `UpdateMultipleTablesWalkthrough` という名前を付けます。

3. [ **Windows アプリケーション**] を選択し、[ **OK]** を選択します。 詳細については、「 [クライアントアプリケーション](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)」を参照してください。

     **UpdateMultipleTablesWalkthrough** プロジェクトが作成されて、**ソリューション エクスプローラー**に追加されます。

## <a name="create-the-data-source"></a>データソースを作成する
 この手順では、**データ ソース構成ウィザード**を使用して、Northwind データベースからデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。

#### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. [ **データ** ] メニューの [**データソースの表示**] をクリックします。

2. [ **データソース** ] ウィンドウで [**新しいデータソースの追加** ] を選択して、 **データソース構成ウィザード**を開始します。

3. [ **データソースの種類を選択**] 画面で、[ **データベース**] を選択し、[ **次へ**] を選択します。

4. [ **データ接続の選択**] 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         - または -

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを開きます。

5. データベースにパスワードが必要な場合は、機密データを含めるオプションを選択し、[ **次へ**] を選択します。

6. [ **接続文字列をアプリケーション構成ファイルに保存する**] で、[ **次へ**] を選択します。

7. [ **データベースオブジェクトの選択**] 画面で、[ **テーブル** ] ノードを展開します。

8. **Customers**テーブルと**Orders**テーブルを選択し、[**完了**] を選択します。

     自分のプロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウにテーブルが表示されます。

## <a name="set-the-controls-to-be-created"></a>作成するコントロールを設定する
 このチュートリアルでは、テーブル内のデータは、 `Customers` 個々のコントロールにデータが表示される **詳細** レイアウトに含まれています。 テーブルのデータ `Orders` は、コントロールに表示される **グリッド** レイアウトに含まれてい <xref:System.Windows.Forms.DataGridView> ます。

#### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>[データ ソース] ウィンドウの項目にドロップ タイプを設定するには

1. [ **データソース** ] ウィンドウで、[ **Customers** ] ノードを展開します。

2. [ **Customers** ] ノードで、コントロールリストの [ **詳細** ] を選択して、 **customers** テーブルのコントロールを個々のコントロールに変更します。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

## <a name="create-the-data-bound-form"></a>データバインドフォームを作成する
 データバインドコントロールを作成するには、[ **データソース** ] ウィンドウからフォームに項目をドラッグします。

#### <a name="to-create-data-bound-controls-on-the-form"></a>フォームにデータ バインド コントロールを作成するには

1. **[データ ソース]** ウィンドウから **Form1** にメインの **[Customers]** ノードをドラッグします。

     説明のラベルが付いたデータ バインド コントロールとレコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

2. **[データ ソース]** ウィンドウから **Form1** に関連する **[Orders]** ノードをドラッグします。

    > [!NOTE]
    > 関連する **[Orders]** ノードは **[Fax]** 列の下にあり、**[Customers]** ノードの子ノードです。

     レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 OrdersTableAdapter とが <xref:System.Windows.Forms.BindingSource> コンポーネントトレイに表示されます。

## <a name="addcode-to-update-the-database"></a>データベースを更新するための addcode
 **Customers** TableAdapter および **Orders** TableAdapter の `Update` メソッドを呼び出して、データベースを更新できます。 既定では、データベースに更新を送信するために、の [ **保存** ] ボタンのイベントハンドラー <xref:System.Windows.Forms.BindingNavigator> がフォームのコードに追加されます。 この手順では、更新プログラムを正しい順序で送信するようにコードを変更します。これにより、参照整合性エラーが発生する可能性がなくなります。 また、Update 呼び出しを try-catch ブロックにラップして、エラー処理も実装します。 アプリケーションの要件に適合するようにコードを変更できます。

> [!NOTE]
> わかりやすくするために、このチュートリアルではトランザクションを使用しません。ただし、2つ以上の関連テーブルを更新する場合は、すべての更新ロジックをトランザクション内に含めます。 トランザクションとは、変更がコミットされる前に、データベースに関連するすべての変更が正常に行われることを保証するプロセスです。 詳しくは、「[トランザクションとコンカレンシー](https://msdn.microsoft.com/library/f46570de-9e50-4fe6-8710-a8c31fa8569b)」をご覧ください。

#### <a name="to-add-update-logic-to-the-application"></a>アプリケーションに更新ロジックを追加するには

1. の [ **保存** ] ボタンを選択し <xref:System.Windows.Forms.BindingNavigator> ます。これにより、コードエディターが開き、イベントハンドラーが表示され `bindingNavigatorSaveItem_Click` ます。

2. イベント ハンドラーのコードを、関連する TableAdapter の `Update` メソッドを呼び出すコードに置き換えます。 次のコードは、最初に、各 <xref:System.Data.DataRowState> (<xref:System.Data.DataRowState>、<xref:System.Data.DataRowState>、および <xref:System.Data.DataRowState>) の更新済み情報を保持する 3 つの一時的なデータ テーブルを作成します。 その後、更新プログラムは正しい順序で実行されます。 コードは、次のようになります。

     [!code-csharp[VbRaddataSaving#10](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form4.cs#10)]
     [!code-vb[VbRaddataSaving#10](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form4.vb#10)]

## <a name="test-the-application"></a>アプリケーションをテストする

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. **F5 キーを押し**ます。

2. 各テーブルの 1 つ以上のレコードのデータを変更します。

3. **[保存]** ボタンを選択します。

4. データベースの値をチェックし、変更が保存されたことを確認します。

## <a name="next-steps"></a>次の手順
 アプリケーションの要件によっては、Windows アプリケーションでデータバインドフォームを作成した後に実行する必要があるいくつかの手順があります。 このチュートリアルで行うことができる拡張には次のものがあります。

- フォームに検索機能を追加します。 詳細については、「 [方法: Windows フォームアプリケーションにパラメーター化クエリを追加](https://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416)する」を参照してください。

- データ ソースを編集し、データベース オブジェクトの追加または削除を行います。 詳細については、「 [方法: データセットを編集](https://msdn.microsoft.com/library/f2dade5f-9c7a-4ddb-96a8-e0a39e50bfd3)する」を参照してください。

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
