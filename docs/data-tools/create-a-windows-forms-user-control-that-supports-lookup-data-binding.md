---
title: データバインディングでのルックアップテーブルの使用-Windows フォーム
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: fe2289a54dba0c3b3e34de54991e9b7cfbee4c93
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037394"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する

フォームにデータを表示する場合は、**ツールボックス**から既存のコントロールを選択するか、またはアプリケーションが標準コントロールでは提供できない機能を必要とする場合は、カスタム コントロールを記述できます。 このチュートリアルでは、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールには、データにバインドできるプロパティを 3 つ含めることができます。 このようなコントロールは、<xref:System.Windows.Forms.ComboBox> に似ています。

コントロールの作成の詳細については、「 [デザイン時の Windows フォームコントロールの開発](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)」を参照してください。

データ バインディングのシナリオで使用するためのコントロールを作成するときは、次のいずれかのデータ バインド属性を実装する必要があります。

|データバインディング属性の使用|
| - |
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 詳細については、「 [単純なデータバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)する」を参照してください。|
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 詳細については、「 [複合データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)する」を参照してください。|
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|

このチュートリアルでは、2 つのテーブルのデータにバインドする検索コントロールを作成します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。 参照コントロールは、テーブルのフィールドにバインドされ `CustomerID` `Orders` ます。 この値を使用して、テーブルからを検索し `CompanyName` `Customers` ます。

このチュートリアルでは、次の方法について説明します。

- 新しい **Windows フォームアプリケーション**を作成します。

- 新しい**ユーザー コントロール**をプロジェクトに追加します。

- ユーザー コントロールをビジュアルに設計します。

- `LookupBindingProperty` 属性を実装します。

- **データソース構成**ウィザードを使用してデータセットを作成します。

- **[データ ソース]** ウィンドウで **Orders** テーブルの **[CustomerID]** 列が新しいコントロールを使用するように設定します。

- フォームを作成して、新しいコントロールにデータを表示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、**データストレージと処理**ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの **データストレージと処理** ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-app-project"></a>Windows フォームアプリプロジェクトを作成する

最初の手順では、 **Windows フォームアプリケーション** プロジェクトを作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ**] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに **Lookupcontrolwalkthrough**という名前を指定し、[ **OK]** を選択します。

     **LookupControlWalkthrough** プロジェクトが作成されて**ソリューション エクスプローラー**に追加されます。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する

このチュートリアルでは**ユーザー コントロール**から検索コントロールを作成するので、**ユーザー コントロール**の項目を **LookupControlWalkthrough** プロジェクトに追加します。

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

2. [ `LookupBox` **名前** ] 領域に「」と入力し、[ **追加**] をクリックします。

     **LookupBox** コントロールが **ソリューション エクスプローラー**に追加され、デザイナーが開きます。

## <a name="design-the-lookupbox-control"></a>LookupBox コントロールのデザイン

LookupBox コントロールをデザインするには、 <xref:System.Windows.Forms.ComboBox> **ツールボックス** からユーザーコントロールのデザインサーフェイスにをドラッグします。

## <a name="add-the-required-data-binding-attribute"></a>必要なデータバインディング属性を追加する

データ バインディングをサポートする検索コントロールには、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装できます。

1. **LookupBox** コントロールをコード ビューに切り替えます。 (**[表示]** メニューの **[コード]** を選択します。)

2. `LookupBox` のコードを次のコードで置き換えます。

     [!code-vb[VbRaddataDisplaying#5](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.vb)]
     [!code-csharp[VbRaddataDisplaying#5](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.cs)]

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-data-source-from-your-database"></a>データベースからデータソースを作成する

この手順では、**データ ソース構成**ウィザードを使用して、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルに基づいてデータ ソースを作成します。

1. [データ **ソース** ] ウィンドウを開くには、[ **データ** ] メニューの [ **データソースの表示**] をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして**データ ソース構成**ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. `Customers` テーブルと `Orders` テーブルを選択し、**[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに `Customers` テーブルと `Orders` テーブルが表示されます。

## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>LookupBox コントロールを使用するように Orders テーブルの CustomerID 列を設定します。

[ **データソース** ] ウィンドウでは、フォームに項目をドラッグする前に作成するコントロールを設定できます。

1. デザイナーで **Form1** を開きます。

2. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

3. **[Fax]** 列の下の **[Customers]** 列にある **[Orders]** ノードを展開します。

4. **[Orders]** ノードのドロップダウン矢印をクリックし、コントロール一覧の **[Details]** を選択します。

5. **[Orders]** ノードの **[CustomerID]** 列のドロップダウン矢印をクリックし、**[Customize]** をクリックします。

6. **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[LookupBox]** を選択します。

7. **[OK]** をクリックします。

8. **[CustomerID]** 列のドロップダウン矢印をクリックし、**[LookupBox]** をクリックします。

## <a name="add-controls-to-the-form"></a>フォームへのコントロールの追加

**[データ ソース]** ウィンドウから **Form1** に項目をドラッグして、データ バインディング コントロールを作成します。

Windows フォームにデータバインドコントロールを作成するには、[**データソース**] ウィンドウから windows フォームに [ **Orders** ] ノードをドラッグし、 **LookupBox**コントロールを使用して列のデータを表示することを確認し `CustomerID` ます。

## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>Customers テーブルから CompanyName を参照するようにコントロールをバインドする

参照バインドを設定するには、[**データソース**] ウィンドウで [メインの**Customers** ] ノードを選択し、 **Form1**の**CustomerIDLookupBox**のコンボボックスにドラッグします。

これによって、`Orders` テーブルの `CustomerID` 値を維持しながら、`Customers` テーブルの `CompanyName` を表示するためのデータ バインディングがセットアップされます。

## <a name="run-the-application"></a>アプリケーションの実行

- **F5** キーを押してアプリケーションを実行します。

- レコード間を移動し、`LookupBox` コントロールに `CompanyName` が表示されることを確認します。

## <a name="see-also"></a>参照

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
