---
title: 挿入/更新/削除の動作をカスタマイズする
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 03ff1146-706e-4780-91cb-56a83df63eea
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5323cfa41dc4931db514977238fd359b4f38ab3f
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036744"
---
# <a name="walkthrough-customize-the-insert-update-and-delete-behavior-of-entity-classes"></a>チュートリアル: エンティティクラスの挿入、更新、および削除の動作のカスタマイズ

[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)には、データベース内のオブジェクトに基づいて LINQ to SQL クラス (エンティティクラス) を作成および編集するためのビジュアルデザインサーフェイスが用意されています。 [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)を使用することにより、LINQ テクノロジを使用して SQL データベースにアクセスできます。 詳細については、[LINQ (統合言語クエリ)](/dotnet/csharp/linq/) に関するページを参照してください。

既定では、更新を実行するロジックは LINQ to SQL ランタイムによって提供されます。 ランタイムは、 `Insert` `Update` `Delete` テーブルのスキーマ (列定義と主キー情報) に基づいて、既定の、、およびの各ステートメントを作成します。 既定の動作を使用しない場合は、更新動作を構成し、データベースのデータの操作に必要な挿入、更新および削除を実行する特定のストアド プロシージャを指定できます。 この方法は、既定の動作が生成されていない場合、たとえばエンティティ クラスがビューにマップされている場合にも実行できます。 また、データベースのテーブルへのアクセスには常にストアド プロシージャを通すようにすると、既定の更新動作をオーバーライドできます。 詳細については、「 [ストアドプロシージャを使用](/dotnet/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures)した操作のカスタマイズ」を参照してください。

> [!NOTE]
> このチュートリアルでは、Northwind データベースで **InsertCustomer**、**UpdateCustomer**、および **DeleteCustomer** の各ストアド プロシージャを使用できるようにしておく必要があります。

このチュートリアルでは、ストアドプロシージャを使用してデータベースにデータを保存するための既定の LINQ to SQL 実行時の動作をオーバーライドするために従う必要がある手順について説明します。

このチュートリアルでは、次のタスクを実行する方法について説明します。

- 新しい Windows フォームアプリケーションを作成し、LINQ to SQL ファイルを追加します。

- Northwind テーブルにマップされるエンティティクラスを作成 `Customers` します。

- LINQ to SQL クラスを参照するオブジェクトデータソースを作成 `Customer` します。

- クラスにバインドされているを含む Windows フォームを作成 <xref:System.Windows.Forms.DataGridView> `Customer` します。

- フォームの保存機能を実装します。

- <xref:System.Data.Linq.DataContext>ストアドプロシージャを**O/R デザイナー**に追加して、メソッドを作成します。

- `Customer`ストアドプロシージャを使用して挿入、更新、および削除を実行するようにクラスを構成します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、**データストレージと処理**ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (**SQL Server オブジェクトエクスプローラー**は、 **Visual Studio インストーラー**の**データストレージと処理**ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="creating-an-application-and-adding-linq-to-sql-classes"></a>アプリケーションの作成と LINQ to SQL クラスの追加

LINQ to SQL クラスを使用して Windows フォームにデータを表示するため、新しい Windows フォームアプリケーションを作成し、LINQ to SQL クラスファイルを追加します。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-a-new-windows-forms-application-project-that-contains-linq-to-sql-classes"></a>LINQ to SQL クラスを含む新しい Windows フォームアプリケーションプロジェクトを作成するには

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ**] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに **UpdatingWithSProcsWalkthrough**という名前を入力し、[ **OK]** をクリックします。

     **UpdatingWithSProcsWalkthrough** プロジェクトが作成されて、**ソリューション エクスプローラー**に追加されます。

4. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

5. **[LINQ to SQL クラス]** テンプレートをクリックし、**[名前]** ボックスに「**Northwind.dbml**」と入力します。

6. **[追加]** をクリックします。

     空の LINQ to SQL クラスファイル (**Northwind .dbml**) がプロジェクトに追加され、 **O/R デザイナー** が開きます。

## <a name="create-the-customer-entity-class-and-object-data-source"></a>Customer エンティティクラスとオブジェクトデータソースを作成する

**サーバーエクスプローラー**または**データベースエクスプローラー**から**O/R デザイナー**にテーブルをドラッグして、データベーステーブルにマップされている LINQ to SQL クラスを作成します。 結果は、データベース内のテーブルにマップされた LINQ to SQL エンティティ クラスになります。 作成したエンティティ クラスは、パブリック プロパティを持つ他のクラスと同様に、オブジェクト データ ソースとして使用できます。

### <a name="to-create-a-customer-entity-class-and-configure-a-data-source-with-it"></a>Customer エンティティ クラスを作成し、そのエンティティ クラスでデータ ソースを構成するには

1. **サーバーエクスプローラー**または**データベースエクスプローラー**で、Northwind サンプルデータベースの SQL Server バージョンの**Customer**テーブルを見つけます。

2. [ **Customers** ] ノードを **サーバーエクスプローラー** または **データベースエクスプローラー** から **O/R デザイナー* 画面にドラッグします。

     **Customer** という名前のエンティティ クラスが作成されます。 これには、Customers テーブルの列に対応するプロパティが含まれています。 このエンティティ クラスは Customers テーブルの 1 人の顧客を表すため、**Customers** ではなく **Customer** という名前が付けられます。

    > [!NOTE]
    > このような名前の変更動作を*複数形化*と呼びます。 [ [オプション] ダイアログボックス](../ide/reference/options-dialog-box-visual-studio.md)で、有効または無効にすることができます。 詳細については、「 [方法: 複数形化をオンまたはオフにする (O/R デザイナー)](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md)」を参照してください。

3. **[ビルド]** メニューの **[UpdatingwithSProcsWalkthrough のビルド]** をクリックして、プロジェクトをビルドします。

4. [データ **ソース** ] ウィンドウを開くには、[ **データ** ] メニューの [ **データソースの表示**] をクリックします。

5. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

6. **[データソースの種類を選択]** ページで、**[オブジェクト]** をクリックし、**[次へ]** をクリックします。

7. **[UpdatingwithSProcsWalkthrough]** ノードを展開し、**[Customer]** クラスを探して選択します。

    > [!NOTE]
    > **Customer** クラスが使用可能でない場合は、ウィザードをキャンセルし、プロジェクトをビルドしてからウィザードを再実行します。
8. **[完了]** をクリックしてデータ ソースを作成し、**Customer** エンティティ クラスを **[データ ソース]** ウィンドウに追加します。

## <a name="create-a-datagridview-to-display-the-customer-data-on-a-windows-form"></a>ユーザーデータを Windows フォームに表示するための DataGridView を作成する

[ **データ** ソース] ウィンドウから Windows フォームにデータソース項目 LINQ to SQL ドラッグして、エンティティクラスにバインドされたコントロールを作成します。

### <a name="to-add-controls-that-are-bound-to-the-entity-classes"></a>エンティティ クラスにバインドされるコントロールを追加するには

1. デザイン ビューで **[Form1]** を開きます。

2. **[データ ソース]** ウィンドウから **[Form1]** に **[Customer]** ノードをドラッグします。

    > [!NOTE]
    > **[データ ソース]** ウィンドウを表示するには、**[データ]** メニューの **[データ ソースの表示]** をクリックします。

3. コードエディターで **Form1** を開きます。

4. 次のコードをフォームに追加します。このフォームは、特定のメソッドの外部にありますが、クラス内に追加し `Form1` ます。

    ```vb
    Private NorthwindDataContext1 As New NorthwindDataContext
    ```

    ```csharp
    private NorthwindDataContext northwindDataContext1
        = new NorthwindDataContext();
    ```

5. `Form_Load` イベントのイベント ハンドラーを作成し、ハンドラーに次のコードを追加します。

    ```vb
    CustomerBindingSource.DataSource = NorthwindDataContext1.Customers
    ```

    ```csharp
    customerBindingSource.DataSource
        = northwindDataContext1.Customers;
    ```

## <a name="implement-save-functionality"></a>保存機能の実装

既定では、保存ボタンが有効ではなく、保存機能は実装されていません。 また、オブジェクト データ ソースに対してデータ バインド コントロールを作成しても、変更されたデータをデータベースに保存するコードは自動的には追加されません。 ここでは、[保存] ボタンを有効にし、LINQ to SQL オブジェクトの保存機能を実装する方法について説明します。

### <a name="to-implement-save-functionality"></a>保存機能を実装するには

1. デザイン ビューで **[Form1]** を開きます。

2. **CustomerBindingNavigator** の保存ボタン (フロッピー ディスクのアイコンのボタン) を選択します。

3. **[プロパティ]** ウィンドウで、**[Enabled]** プロパティを **[True]** に設定します。

4. 保存ボタンをダブルクリックして、イベント ハンドラーを作成し、コード エディターに切り替えます。

5. 保存ボタンのイベント ハンドラーに次のコードを追加します。

    ```vb
    NorthwindDataContext1.SubmitChanges()
    ```

    ```csharp
    northwindDataContext1.SubmitChanges();
    ```

## <a name="override-the-default-behavior-for-performing-updates-inserts-updates-and-deletes"></a>更新 (挿入、更新、および削除) を実行するための既定の動作を上書きする

### <a name="to-override-the-default-update-behavior"></a>既定の更新動作をオーバーライドするには

1. **O/R デザイナー**で LINQ to SQL ファイルを開きます。 (**ソリューション エクスプローラー**で **Northwind.dbml** ファイルをダブルクリックします。)

2. **サーバー エクスプローラー**または**データベース エクスプローラー**で、Northwind データベースの **[ストアド プロシージャ]** ノードを展開し、**InsertCustomers**、**UpdateCustomers**、および **DeleteCustomers** の各ストアド プロシージャを探します。

3. 3つのストアドプロシージャをすべて **O/R デザイナー**にドラッグします。

     各ストアド プロシージャが <xref:System.Data.Linq.DataContext> のメソッドとしてメソッド ペインに追加されます。 詳細については、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

4. **O/R デザイナー**で**Customer**エンティティクラスを選択します。

5. **[プロパティ]** ウィンドウで **[Insert]** プロパティを選択します。

6. **[ランタイムを使用]** の横にある省略記号 (**[...]**) をクリックして、**[動作の構成]** ダイアログ ボックスを開きます。

7. **[カスタマイズ]** を選択します。

8. **[カスタマイズ]** リストの **[InsertCustomers]** メソッドを選択します。

9. **[適用]** をクリックして、選択したクラスと動作の構成を保存します。

    > [!NOTE]
    > 変更を行うたびに **[適用]** をクリックすると、各クラスと動作の組み合わせに対して動作の構成を続けることができます。 [ **適用**] をクリックする前にクラスまたは動作を変更すると、変更を適用する機会を提供する警告ダイアログボックスが表示されます。

10. **[動作]** リストの **[Update]** を選択します。

11. **[カスタマイズ]** を選択します。

12. **[カスタマイズ]** リストの **[UpdateCustomers]** メソッドを選択します。

     **[メソッドの引数]** および **[クラスのプロパティ]** のリストを調べると、テーブルの一部の列には 2 つの**メソッドの引数**と 2 つの**クラスのプロパティ**があることがわかります。 これにより、変更を追跡したり、コンカレンシー違反をチェックするステートメントを作成したりすることが簡単になります。

13. **Original_CustomerID** メソッド引数を **CustomerID (オリジナル)** クラス プロパティにマップします。

    > [!NOTE]
    > 既定では、メソッド引数は名前が一致した場合にクラス プロパティにマップされます。 プロパティ名が変更され、テーブルとエンティティ クラス間で一致しなくなったために、**O/R デザイナー**が正しいマッピングを判断できないときは、マップ先となる同等のクラス プロパティを選択することが必要になる場合があります。 また、メソッド引数のマップ先として有効なクラス プロパティがない場合は、**[クラスのプロパティ]** 値を **[(なし)]** に設定できます。

14. **[適用]** をクリックして、選択したクラスと動作の構成を保存します。

15. **[動作]** リストの **[Delete]** を選択します。

16. **[カスタマイズ]** を選択します。

17. **[カスタマイズ]** リストの **[DeleteCustomers]** メソッドを選択します。

18. **Original_CustomerID** メソッド引数を **CustomerID (オリジナル)** クラス プロパティにマップします。

19. **[OK]** をクリックします。

> [!NOTE]
> このチュートリアルでは問題ではありませんが、挿入と更新の際に、データベースで生成され LINQ to SQL た値が id (自動インクリメント)、rowguidcol (データベースによって生成された GUID)、およびタイムスタンプ列に対して自動的に処理されることに注意してください。 その他の列型のデータベースが生成した値は、予想に反して null 値になります。 データベースで生成された値を返すには、をに手動で設定し、次のいずれかを指定する必要があります <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> `true` <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> : [autosync。 Always](<xref:System.Data.Linq.Mapping.AutoSync.Always>)、 [autosync. OnInsert](<xref:System.Data.Linq.Mapping.AutoSync.OnInsert>)、または [autosync. OnUpdate](<xref:System.Data.Linq.Mapping.AutoSync.OnUpdate>)。

## <a name="test-the-application"></a>アプリケーションをテストする

アプリケーションを再実行し、データベース内の顧客レコードが **UpdateCustomers** ストアド プロシージャによって正しく更新されることを確認します。

1. **F5**キーを押します。

2. グリッド内のレコードを変更して、更新動作をテストします。

3. 新しいレコードを追加して、挿入動作をテストします。

4. 保存ボタンをクリックして変更をデータベースに保存します。

5. フォームを閉じます 

6. **F5**キーを押して、更新されたレコードと新しく挿入されたレコードが保持されていることを確認します。

7. 手順 3 で作成した新しいレコードを削除して、削除動作をテストします。

8. 保存ボタンをクリックして変更を送信し、削除されたレコードをデータベースから削除します。

9. フォームを閉じます 

10. **F5**キーを押して、削除したレコードがデータベースから削除されたことを確認します。

    > [!NOTE]
    > アプリケーションで SQL Server Express Edition を使用している場合、データベース ファイルの **[出力ディレクトリにコピー]** プロパティの値によっては、手順 10 で **F5** キーを押したときに変更が表示されない場合があります。

## <a name="next-steps"></a>次のステップ

アプリケーションの要件によっては、LINQ to SQL エンティティクラスを作成した後に実行する必要があるいくつかの手順があります。 このアプリケーションで行うことができる拡張には次のものがあります。

- 更新時のコンカレンシー チェックを実装します。 詳細については、「 [オプティミスティック同時実行制御: 概要](/dotnet/framework/data/adonet/sql/linq/optimistic-concurrency-overview)」を参照してください。

- LINQ クエリを追加してデータをフィルター処理します。 詳細については、「 [LINQ クエリの概要 (C#)](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries)」を参照してください。

## <a name="see-also"></a>参照

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [DataContext メソッド](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [LINQ to SQL クエリ](/dotnet/framework/data/adonet/sql/linq/linq-to-sql-queries)
