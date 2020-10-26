---
title: データバインディングを使用して Windows フォームユーザーコントロールを作成する
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 97d9e64a0fcabb207d4606d4819f6afcb61b1043
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75586849"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>複合データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成

Windows アプリケーションのフォームにデータを表示する場合は、[ **ツールボックス**] から既存のコントロールを選択できます。 または、アプリケーションに標準コントロールでは使用できない機能が必要な場合は、カスタムコントロールを作成できます。 このチュートリアルでは、<xref:System.ComponentModel.ComplexBindingPropertiesAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> を実装するコントロールには、データにバインドできる `DataSource` プロパティと `DataMember` プロパティが含まれます。 このようなコントロールは、<xref:System.Windows.Forms.DataGridView> や <xref:System.Windows.Forms.ListBox> に似ています。

コントロールの作成の詳細については、「 [デザイン時の Windows フォームコントロールの開発](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)」を参照してください。

データ バインディングのシナリオで使用するためのコントロールを作成するときは、次のいずれかのデータ バインディング属性を実装する必要があります。

|データバインディング属性の使用|
| - |
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 詳細については、「 [単純なデータバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)する」を参照してください。|
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 詳細については、「 [参照データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)する」を参照してください。|

このチュートリアルでは、テーブルからのデータ行を表示する複合コントロールを作成します。 この例では、Northwind サンプル データベースの `Customers` テーブルを使用します。 複合ユーザー コントロールは、カスタム コントロールの <xref:System.Windows.Forms.DataGridView> で Customers テーブルを表示します。

このチュートリアルでは、次の方法について説明します。

- 新しい**ユーザー コントロール**をプロジェクトに追加します。

- ユーザー コントロールをビジュアルに設計します。

- `ComplexBindingProperty` 属性を実装します。

- [データソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用してデータセットを作成します。

- [[データソース] ウィンドウ](add-new-data-sources.md#data-sources-window)の**Customers**テーブルを、新しい複合コントロールを使用するように設定します。

- **[データ ソース]** ウィンドウから **Form1** に新しいコントロールをドラッグして追加します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、**データストレージと処理**ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

1. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの **データストレージと処理** ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    1. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    1. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-app-project"></a>Windows フォームアプリプロジェクトを作成する

最初の手順では、C# または Visual Basic 用の **Windows フォームアプリ** プロジェクトを作成します。 プロジェクトに **ComplexControlWalkthrough** という名前を付けます。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する

このチュートリアルでは、 **ユーザーコントロール**から複雑なデータバインド可能なコントロールを作成するため、 **ユーザーコントロール** 項目をプロジェクトに追加します。

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** を選択します。

1. **[ファイル名]** 領域に「**ComplexDataGridView**」と入力し、**[追加]** をクリックします。

    **ComplexDataGridView** コントロールが**ソリューション エクスプローラー**に追加され、デザイナーが開きます。

## <a name="design-the-complexdatagridview-control"></a>ComplexDataGridView コントロールをデザインする

をユーザーコントロールに追加するには、 <xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.DataGridView> **ツールボックス** からユーザーコントロールのデザインサーフェイスにをドラッグします。

## <a name="add-the-required-data-binding-attribute"></a>必要なデータバインディング属性を追加する

データ バインディングをサポートする複合コントロールには、<xref:System.ComponentModel.ComplexBindingPropertiesAttribute> を実装できます。

1. **ComplexDataGridView** コントロールをコード ビューに切り替えます  (**[表示]** メニューの **[コード]** を選択します)。

1. `ComplexDataGridView` のコードを次のコードで置き換えます。

    [!code-csharp[VbRaddataDisplaying#4](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-complex-data-binding_1.cs)]
    [!code-vb[VbRaddataDisplaying#4](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-complex-data-binding_1.vb)]

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-data-source-from-your-database"></a>データベースからデータソースを作成する

**データソース構成**ウィザードを使用して、Northwind サンプルデータベースのテーブルに基づいてデータソースを作成し `Customers` ます。

1. [データ **ソース** ] ウィンドウを開くには、[ **データ** ] メニューの [ **データソースの表示**] をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして**データ ソース構成**ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

   - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

   - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. `Customers` テーブルを選択し、**[完了]** をクリックします。

   **NorthwindDataSet**がプロジェクトに追加され、[ `Customers` **データソース**] ウィンドウにテーブルが表示されます。

## <a name="set-the-customers-table-to-use-the-complexdatagridview-control"></a>ComplexDataGridView コントロールを使用するように Customers テーブルを設定する

**[データ ソース]** ウィンドウでは、フォームにコントロールをドラッグする前に作成するコントロールを設定できます。

1. デザイナーで **Form1** を開きます。

1. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

1. **[Customers]** ノードのドロップダウン矢印をクリックし、**[カスタマイズ]** をクリックします。

1. **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[ComplexDataGridView]** を選択します。

1. `Customers` テーブルのドロップダウン矢印をクリックし、コントロール リストから **ComplexDataGridView** を選択します。

## <a name="add-controls-to-the-form"></a>フォームへのコントロールの追加

データバインドコントロールを作成するには、[ **データソース** ] ウィンドウからフォームに項目をドラッグします。 **[データ ソース]** ウィンドウからフォームにメインの **[Customers]** ノードをドラッグします。 **Complexdatagridview**コントロールがテーブルのデータを表示するために使用されていることを確認します。

## <a name="run-the-application"></a>アプリケーションの実行

**F5** キーを押してアプリケーションを実行します。

## <a name="next-steps"></a>次の手順

アプリケーションの要件に応じて、データ バインディングをサポートするコントロールの作成後に、追加の操作を実行できます。 次の手順として、一般的には、次のようなことを実行します。

- 他のアプリケーションで再利用できるように、コントロール ライブラリにカスタム コントロールを配置します。

- 検索のシナリオをサポートするコントロールを作成します。 詳細については、「 [参照データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)する」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
- [Windows フォームコントロール](/dotnet/framework/winforms/controls/index)
