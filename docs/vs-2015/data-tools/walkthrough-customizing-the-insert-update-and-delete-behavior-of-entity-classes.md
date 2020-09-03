---
title: 'チュートリアル: エンティティクラスの挿入、更新、および削除の動作のカスタマイズ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 03ff1146-706e-4780-91cb-56a83df63eea
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9901d917de2babf4992519ffe6b360454542aad1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72602569"
---
# <a name="walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes"></a>チュートリアル: エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)には、 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] データベース内のオブジェクトに基づくクラス (エンティティクラス) を作成および編集するためのビジュアルデザインサーフェイスが用意されています。 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)を使用することにより、LINQ テクノロジを使用して SQL データベースにアクセスできます。 詳細については、「 [LINQ (統合言語クエリ)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)」を参照してください。

 既定では、更新を実行するロジックは [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] ランタイムによって提供されます。 ランタイムは、テーブルのスキーマ (列定義と主キー情報) に基づいて、既定の Insert、Update、および Delete の各ステートメントを作成します。 既定の動作を使用しない場合は、更新動作を構成し、データベースのデータの操作に必要な Insert、Update、および Delete を実行する特定のストアド プロシージャを指定できます。 この方法は、既定の動作が生成されていない場合、たとえばエンティティ クラスがビューにマップされている場合にも実行できます。 また、データベースのテーブルへのアクセスには常にストアド プロシージャを通すようにすると、既定の更新動作をオーバーライドできます。 詳しくは、「[ストアド プロシージャによる操作のカスタマイズ](https://msdn.microsoft.com/library/aedbecc1-c33c-4fb4-8861-fdf7e1dc6b8a)」をご覧ください。

> [!NOTE]
> このチュートリアルでは、Northwind データベースで **InsertCustomer**、**UpdateCustomer**、および **DeleteCustomer** の各ストアド プロシージャを使用できるようにしておく必要があります。

 このチュートリアルでは、ストアド プロシージャを使用して、データベースにデータを保存する既定の LINQ to SQL ランタイムの動作をオーバーライドするために必要な手順を示します。

 このチュートリアルでは、次のタスクを実行する方法を学習します。

- 新しい Windows フォーム アプリケーションを作成し、[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] ファイルを追加します。

- Northwind の Customers テーブルにマップされるエンティティ クラスを作成します。

- LINQ to SQL Customer クラスを参照するオブジェクト データ ソースを作成します。

- Customer クラスにバインドされる <xref:System.Windows.Forms.DataGridView> を含む Windows フォームを作成します。

- フォームの保存機能を実装します。

- <xref:System.Data.Linq.DataContext>にストアド プロシージャを追加することにより、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] のメソッドを作成します。

- ストアド プロシージャを使用して挿入、更新、および削除を実行するように Customer クラスを構成します。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するための要件は次のとおりです。

- Northwind サンプル データベースの SQL Server バージョンにアクセスします。

- Northwind データベースの **Insertcustomer**、 **UpdateCustomer**、および **DeleteCustomer** ストアドプロシージャ。

## <a name="creating-an-application-and-adding-linq-to-sql-classes"></a>アプリケーションの作成と LINQ to SQL クラスの追加
 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] クラスを操作してデータを Windows フォームに表示できるように、新しい Windows フォーム アプリケーションを作成し、LINQ to SQL クラス ファイルを追加します。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-a-new-windows-application-project-that-contains-linq-to-sql-classes"></a>LINQ to SQL クラスを含む新しい Windows アプリケーション プロジェクトを作成するには

1. [ **ファイル** ] メニューで、新しいプロジェクトを作成します。

2. プロジェクトに **UpdatingwithSProcsWalkthrough**という名前を指定します。

    > [!NOTE]
    > [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]は [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロジェクトと C# プロジェクトでサポートされています。 したがって、新しいプロジェクトはこれらの言語のどちらかで作成してください。

3. **Windows フォームアプリケーション**テンプレートをクリックし、[ **OK]** をクリックします。 詳細については、「 [クライアントアプリケーション](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)」を参照してください。

     UpdatingwithSProcsWalkthrough プロジェクトが作成され、 **ソリューションエクスプローラー**に追加されます。

4. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

5. **[LINQ to SQL クラス]** テンプレートをクリックし、**[名前]** ボックスに「**Northwind.dbml**」と入力します。

6. **[追加]** をクリックします。

     プロジェクトに空の LINQ to SQL クラス ファイル (Northwind.dbml) が追加され、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]が開きます。

## <a name="creating-the-customer-entity-class-and-object-data-source"></a>Customer エンティティ クラスとオブジェクト データ ソースの作成
 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]**サーバーエクスプローラー**データベースエクスプローラーからにテーブルをドラッグして、データベーステーブルにマップされるクラスを作成 / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] します。 結果は、データベース内のテーブルにマップされた LINQ to SQL エンティティ クラスになります。 作成したエンティティ クラスは、パブリック プロパティを持つ他のクラスと同様に、オブジェクト データ ソースとして使用できます。

#### <a name="to-create-a-customer-entity-class-and-configure-a-data-source-with-it"></a>Customer エンティティ クラスを作成し、そのエンティティ クラスでデータ ソースを構成するには

1. **サーバーエクスプローラー** / **データベースエクスプローラー**で、Northwind サンプルデータベースの SQL Server バージョンの Customer テーブルを見つけます。

2. **サーバーエクスプローラー**データベースエクスプローラーから [ **Customers (顧客**) ノードを画面にドラッグし / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

     **Customer** という名前のエンティティ クラスが作成されます。 これには、Customers テーブルの列に対応するプロパティが含まれています。 このエンティティ クラスは Customers テーブルの 1 人の顧客を表すため、**Customers** ではなく **Customer** という名前が付けられます。

    > [!NOTE]
    > このような名前の変更動作を*複数形化*と呼びます。 [ [オプション] ダイアログボックス](../ide/reference/options-dialog-box-visual-studio.md)で、有効または無効にすることができます。 詳細については、「 [方法: 複数形化をオンまたはオフにする (O/R デザイナー)](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md)」を参照してください。

3. **[ビルド]** メニューの **[UpdatingwithSProcsWalkthrough のビルド]** をクリックして、プロジェクトをビルドします。

4. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

5. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

6. **[データソースの種類を選択]** ページで、**[オブジェクト]** をクリックし、**[次へ]** をクリックします。

7. **[UpdatingwithSProcsWalkthrough]** ノードを展開し、**[Customer]** クラスを探して選択します。

    > [!NOTE]
    > **Customer** クラスが使用可能でない場合は、ウィザードをキャンセルし、プロジェクトをビルドしてからウィザードを再実行します。

8. **[完了]** をクリックしてデータ ソースを作成し、**Customer** エンティティ クラスを **[データ ソース]** ウィンドウに追加します。

## <a name="creating-a-datagridview-to-display-the-customer-data-on-a-windows-form"></a>Windows フォームに顧客データを表示するための DataGridView の作成
 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)][**データ**ソース] ウィンドウから Windows フォームにデータソース項目をドラッグして、エンティティクラスにバインドされるコントロールを作成します。

#### <a name="to-add-controls-that-are-bound-to-the-entity-classes"></a>エンティティ クラスにバインドされるコントロールを追加するには

1. デザイン ビューで [Form1] を開きます。

2. [ **データソース** ] ウィンドウで、[ **Customer** ] ノードを Form1 にドラッグします。

    > [!NOTE]
    > **[データ ソース]** ウィンドウを表示するには、**[データ]** メニューの **[データ ソースの表示]** をクリックします。

3. コード エディターで Form1 を開きます。

4. フォームに次のコードを追加します。フォームに対してグローバルになるように、Form1 クラスの内部でありながら、どのメソッドにも属さない位置に追加します。

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

## <a name="implementing-save-functionality"></a>保存機能の実装
 既定では、保存ボタンが有効ではなく、保存機能は実装されていません。 また、オブジェクト データ ソースに対してデータ バインド コントロールを作成しても、変更されたデータをデータベースに保存するコードは自動的には追加されません。 ここでは、保存ボタンを有効にし、[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] オブジェクトの保存機能を実装する方法について説明します。

#### <a name="to-implement-save-functionality"></a>保存機能を実装するには

1. デザイン ビューで [Form1] を開きます。

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

## <a name="overriding-the-default-behavior-for-performing-updates-inserts-updates-and-deletes"></a>更新 (Insert、Update、および Delete) の実行に対する既定の動作のオーバーライド

#### <a name="to-override-the-default-update-behavior"></a>既定の更新動作をオーバーライドするには

1. [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]で LINQ to SQL ファイルを開きます  (**ソリューション エクスプローラー**で **Northwind.dbml** ファイルをダブルクリックします。)

2. **サーバーエクスプローラー** / **データベースエクスプローラー**で、Northwind データベースの [**ストアドプロシージャ**] ノードを展開し、 **insertcustomers**、 **UpdateCustomers**、および**DeleteCustomers**ストアドプロシージャを探します。

3. 3 つのストアド プロシージャをすべて [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]にドラッグします。

     各ストアド プロシージャが <xref:System.Data.Linq.DataContext> のメソッドとしてメソッド ペインに追加されます。 詳しくは、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」をご覧ください。

4. で **Customer** エンティティクラスを選択し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

5. **[プロパティ]** ウィンドウで **[Insert]** プロパティを選択します。

6. **[ランタイムを使用]** の横にある省略記号 ([...]) をクリックして、**[動作の構成]** ダイアログ ボックスを開きます。

7. **[カスタマイズ]** を選択します。

8. **[カスタマイズ]** リストの **[InsertCustomers]** メソッドを選択します。

9. **[適用]** をクリックして、選択したクラスと動作の構成を保存します。

    > [!NOTE]
    > 変更を行うたびに **[適用]** をクリックすると、各クラスと動作の組み合わせに対して動作の構成を続けることができます。 [ **適用**] をクリックする前にクラスまたは動作を変更すると、変更を適用するための警告ダイアログボックスが表示されます。

10. **[動作]** リストの **[Update]** を選択します。

11. **[カスタマイズ]** を選択します。

12. **[カスタマイズ]** リストの **[UpdateCustomers]** メソッドを選択します。

     **[メソッドの引数]** および **[クラスのプロパティ]** のリストを調べると、テーブルの一部の列には 2 つの**メソッドの引数**と 2 つの**クラスのプロパティ**があることがわかります。 これにより、変更を追跡したり、コンカレンシー違反をチェックするステートメントを作成したりすることが簡単になります。

13. **Original_CustomerID** メソッド引数を **CustomerID (オリジナル)** クラス プロパティにマップします。

    > [!NOTE]
    > 既定では、メソッド引数は名前が一致した場合にクラス プロパティにマップされます。 プロパティ名が変更され、テーブルとエンティティ クラス間で一致しなくなったために、O/R デザイナーが正しいマッピングを判断できないときは、マップ先となる同等のクラス プロパティを選択することが必要になる場合があります。 また、メソッド引数のマップ先として有効なクラス プロパティがない場合は、**[クラスのプロパティ]** 値を **[(なし)]** に設定できます。

14. **[適用]** をクリックして、選択したクラスと動作の構成を保存します。

15. **[動作]** リストの **[Delete]** を選択します。

16. **[カスタマイズ]** を選択します。

17. **[カスタマイズ]** リストの **[DeleteCustomers]** メソッドを選択します。

18. **Original_CustomerID** メソッド引数を **CustomerID (オリジナル)** クラス プロパティにマップします。

19. **[OK]** をクリックします。

> [!NOTE]
> この特定のチュートリアルに限った問題ではありませんが、[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] は、ID 列 (自動インクリメント)、rowguidcol 列 (データベースが生成した GUID)、およびタイムスタンプ列であれば、データベースによって生成された値を、挿入時および更新時に自動的に処理します。 その他の列型のデータベースが生成した値は、予想に反して null 値になります。 データベースが生成した値を返すには、手動で <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> を `true` に設定し、<xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> を <xref:System.Data.Linq.Mapping.AutoSync>、<xref:System.Data.Linq.Mapping.AutoSync>、または <xref:System.Data.Linq.Mapping.AutoSync> のいずれかに設定する必要があります。

## <a name="testing-the-application"></a>アプリケーションのテスト
 アプリケーションを再実行し、データベース内の顧客レコードが **UpdateCustomers** ストアド プロシージャによって正しく更新されることを確認します。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. F5 キーを押す。

2. グリッド内のレコードを変更して、Update の動作をテストします。

3. 新しいレコードを追加して、Insert の動作をテストします。

4. 保存ボタンをクリックして変更をデータベースに保存します。

5. フォームを閉じます 

6. F5 キーを押し、更新されたレコードと新しく挿入したレコードが永続化されていることを確認します。

7. 手順 3. で作成した新しいレコードを削除して、Delete の動作をテストします。

8. 保存ボタンをクリックして変更を送信し、削除されたレコードをデータベースから削除します。

9. フォームを閉じます 

10. F5 キーを押し、削除したレコードがデータベースから削除されていることを確認します。

    > [!NOTE]
    > アプリケーションで SQL Server Express Edition を使用している場合、データベース ファイルの **[出力ディレクトリにコピー]** プロパティの値によっては、手順 10 で F5 キーを押したときに変更が表示されない場合があります。

## <a name="next-steps"></a>次の手順
 アプリケーションの要件に応じて、[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] エンティティ クラスの作成後にいくつかの手順を実行することが必要な場合があります。 このアプリケーションで行うことができる拡張には次のものがあります。

- 更新時のコンカレンシー チェックを実装します。 詳細については、「 [オプティミスティック同時実行制御: 概要](https://msdn.microsoft.com/library/c2e38512-d0c8-4807-b30a-cb7e30338694)」を参照してください。

- LINQ クエリを追加してデータをフィルター処理します。 詳細については、「 [LINQ クエリの概要 (C#)](https://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)」を参照してください。

## <a name="see-also"></a>参照
 [Visual studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [LINQ to SQL クエリ](https://msdn.microsoft.com/library/f4897aaa-7f44-4c20-a471-b948c2971aae) [DataContext メソッド (o/r デザイナー)](../data-tools/datacontext-methods-o-r-designer.md) [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (o/r デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md) [visual Studio 2012 でのデータアプリケーション開発の新機能 PAVE](https://msdn.microsoft.com/3d50d68f-5f44-4915-842f-6d42fce793f1)
