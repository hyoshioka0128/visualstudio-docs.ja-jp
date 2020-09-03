---
title: TableAdapter DBDirect メソッドを使用してデータを保存する |Microsoft Docs
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
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ce987f5ef90448c41da45a39c62710b968e11199
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655421"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>TableAdapter DBDirect メソッドを使用してデータを保存する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、TableAdapter の DBDirect メソッドを使用してデータベースに対して SQL ステートメントを直接実行するための詳細な手順について説明します。 TableAdapter の DBDirect メソッドを使用すると、データベースの更新をきめ細かいレベルで制御できます。 これらのメソッドを使用すると、 `Insert` `Update` `Delete` ( `Update` UPDATE、INSERT、および DELETE ステートメントをすべて1回の呼び出しで実行するオーバーロードされたメソッドではなく) 個々の、、およびメソッドを呼び出すことによって、特定の SQL ステートメントおよびストアドプロシージャを実行できます。

 このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **Windows アプリケーション**を作成します。

- [データソース構成ウィザード](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)を使用して、データセットを作成および構成します。

- **[データ ソース]** ウィンドウから項目をドラッグしたときにフォーム上に作成されるコントロールを選択します。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド フォームを作成します。

- データベースに直接アクセスして、挿入、更新、および削除を実行するメソッドを追加します。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを完了するための要件は次のとおりです。

- Northwind サンプル データベースにアクセスします。

## <a name="create-a-windows-application"></a>Windows アプリケーションを作成する
 最初の手順では、 **Windows アプリケーション**を作成します。

#### <a name="to-create-the-new-windows-project"></a>新しい Windows プロジェクトを作成するには

1. Visual Studio の [ **ファイル** ] メニューで、新しい **プロジェクト**を作成します。

2. プロジェクトに **TableAdapterDbDirectMethodsWalkthrough**という名前を指定します。

3. [ **Windows アプリケーション**] を選択し、[ **OK]** を選択します。 詳細については、「 [クライアントアプリケーション](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)」を参照してください。

     **TableAdapterDbDirectMethodsWalkthrough** プロジェクトが作成されて**ソリューション エクスプローラー**に追加されます。

## <a name="create-a-data-source-from-your-database"></a>データベースからデータソースを作成する
 この手順では、**データ ソース構成ウィザード**を使用して、Northwind サンプル データベースの `Region` テーブルに基づいてデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。

#### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. [ **データ** ] メニューの [ **データソースの表示**] をクリックします。

2. [ **データソース** ] ウィンドウで [ **新しいデータソースの追加** ] を選択して、 **データソース構成ウィザード**を開始します。

3. [ **データソースの種類を選択** ] 画面で、[ **データベース**] を選択し、[ **次へ**] を選択します。

4. [ **データ接続の選択** ] 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         - または -

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、機密データを含めるオプションを選択し、[ **次へ**] を選択します。

6. [ **アプリケーション構成ファイルへの接続文字列の保存** ] 画面で、[ **次へ**] を選択します。

7. [ **データベースオブジェクトの選択** ] 画面で、[ **テーブル** ] ノードを展開します。

8. テーブルを選択し、[ `Region` **完了**] を選択します。

     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに `Region` テーブルが表示されます。

## <a name="addcontrols-to-the-form-to-display-the-data"></a>データを表示するためのフォームへの addcontrols
 **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>Windows フォームにデータバインドコントロールを作成するには

- [**データソース**] ウィンドウからフォームにメイン**領域**ノードをドラッグします。

     レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、regiontableadapter、 <xref:System.Windows.Forms.BindingSource> 、およびが <xref:System.Windows.Forms.BindingNavigator> コンポーネントトレイに表示されます。

#### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>個々の TableAdapter DbDirect メソッドを呼び出すボタンを追加するには

1. **ツールボックス**から 3 つの <xref:System.Windows.Forms.Button> コントロールを **RegionDataGridView** の下の **Form1** にドラッグします。

2. 各ボタンの **[名前]** および **[テキスト]** プロパティを設定します。

    |名前|テキスト|
    |----------|----------|
    |`InsertButton`|**挿入**|
    |`UpdateButton`|**アップデート**|
    |`DeleteButton`|**削除**|

#### <a name="to-add-code-to-insert-new-records-into-the-database"></a>データベースに新しいレコードを挿入するコードを追加するには

1. [ **Insertbutton** ] を選択して、クリックイベントのイベントハンドラーを作成し、コードエディターでフォームを開きます。

2. `InsertButton_Click` イベント ハンドラーを次のコードで置き換えます。

     [!code-csharp[VbRaddataSaving#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs#1)]
     [!code-vb[VbRaddataSaving#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb#1)]

#### <a name="to-add-code-to-update-records-in-the-database"></a>データベースのレコードを更新するコードを追加するには

1. **[UpdateButton]** をダブルクリックして、クリック イベントのイベント ハンドラーを作成し、コード エディターでフォームを開きます。

2. `UpdateButton_Click` イベント ハンドラーを次のコードで置き換えます。

     [!code-csharp[VbRaddataSaving#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs#2)]
     [!code-vb[VbRaddataSaving#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb#2)]

#### <a name="to-add-code-to-delete-records-from-the-database"></a>データベースからレコードを削除するコードを追加するには

1. [ **Deletebutton** ] を選択して、クリックイベントのイベントハンドラーを作成し、コードエディターでフォームを開きます。

2. `DeleteButton_Click` イベント ハンドラーを次のコードで置き換えます。

     [!code-csharp[VbRaddataSaving#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs#3)]
     [!code-vb[VbRaddataSaving#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb#3)]

## <a name="run-the-application"></a>アプリケーションの実行

#### <a name="to-run-the-application"></a>アプリケーションを実行するには

- **F5 キーを押し**てアプリケーションを実行します。

- [ **挿入** ] ボタンを選択し、新しいレコードがグリッドに表示されていることを確認します。

- [ **更新** ] ボタンを選択し、グリッドでレコードが更新されていることを確認します。

- [ **削除** ] ボタンを選択し、レコードがグリッドから削除されていることを確認します。

## <a name="next-steps"></a>次の手順
 アプリケーションの要件によっては、データバインドフォームの作成後に実行する必要があるいくつかの手順があります。 このチュートリアルで行うことができる拡張には次のものがあります。

- フォームに検索機能を追加します。 詳細については、「 [方法: Windows フォームアプリケーションにパラメーター化クエリを追加](https://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416)する」を参照してください。

- **[データ ソース]** ウィンドウの **[ウィザードで DataSet を構成]** を選択して、データセットにテーブルを追加します。 関連するコードをフォームにドラッグすることによって、関連するデータを表示するコントロールを追加できます。

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
