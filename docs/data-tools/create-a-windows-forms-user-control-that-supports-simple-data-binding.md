---
title: 単純なデータ バインディングをサポートするユーザー コントロールを作成する
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ace5f9dd2781697525e7041be6cbd8df050bca97
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75586824"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成

Windows アプリケーションのフォームにデータを表示する場合は、**[ツールボックス]** から既存のコントロールを選択するか、またはアプリケーションが標準コントロールでは提供できない機能を必要とする場合は、カスタム コントロールを記述できます。 このチュートリアルでは、<xref:System.ComponentModel.DefaultBindingPropertyAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> を実装するコントロールには、データにバインドできるプロパティを 1 つ含めることができます。 このようなコントロールは、<xref:System.Windows.Forms.TextBox> や <xref:System.Windows.Forms.CheckBox> に似ています。

コントロールの作成の詳細については、「 [デザイン時の Windows フォームコントロールの開発](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)」を参照してください。

データバインディングのシナリオで使用するコントロールを作成する場合は、次のいずれかのデータバインディング属性を実装する必要があります。

|データバインディング属性の使用|
| - |
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 詳細については、「 [複合データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)する」を参照してください。|
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 詳細については、「 [参照データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)する」を参照してください。|

このチュートリアルでは、テーブルの単一の列のデータを表示する簡単なコントロールを作成します。 この例では、Northwind サンプル データベースの `Phone` テーブルの `Customers` 列を使用します。 簡易ユーザーコントロールは、を使用して電話番号にマスクを設定することにより、顧客の電話番号を標準の電話番号形式で表示し <xref:System.Windows.Forms.MaskedTextBox> ます。

このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **Windows フォームアプリケーション**を作成します。

- 新しい**ユーザー コントロール**をプロジェクトに追加します。

- ユーザー コントロールをビジュアルに設計します。

- `DefaultBindingProperty` 属性を実装します。

- **データソース構成**ウィザードを使用してデータセットを作成します。

- **[データ ソース]** ウィンドウで **[Phone]** 列が新しいコントロールを使用するように設定します。

- フォームを作成して、新しいコントロールにデータを表示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、**データストレージと処理**ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、 **Visual Studio インストーラー**の**データストレージと処理**ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-application"></a>Windows フォーム アプリケーションを作成する

最初の手順では、 **Windows フォームアプリケーション**を作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ**] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに **SimpleControlWalkthrough**という名前を入力し、[ **OK]** をクリックします。

     **SimpleControlWalkthrough** プロジェクトが作成されて**ソリューション エクスプローラー**に追加されます。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する

このチュートリアルでは、 **ユーザーコントロール**から単純なデータバインド可能なコントロールを作成します。 **SimpleControlWalkthrough**プロジェクトに**ユーザーコントロール**項目を追加します。

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** を選択します。

2. [ファイル名] 領域に「**PhoneNumberBox**」と入力し、**[追加]** をクリックします。

     **PhoneNumberBox** コントロールが **ソリューション エクスプローラー**に追加され、デザイナーが開きます。

## <a name="design-the-phonenumberbox-control"></a>PhoneNumberBox コントロールのデザイン

このチュートリアルでは、既存のを展開して、 <xref:System.Windows.Forms.MaskedTextBox> **PhoneNumberBox** コントロールを作成します。

1. **ツールボックス**からユーザー コントロールのデザイン サーフェイスに <xref:System.Windows.Forms.MaskedTextBox> をドラッグします。

2. ドラッグした <xref:System.Windows.Forms.MaskedTextBox> のスマート タグを選択し、**[マスクの設定]** を選択します。

3. **[定型入力]** ダイアログ ボックスで **[電話番号]** を選択し、**[OK]** をクリックしてマスクを設定します。

## <a name="add-the-required-data-binding-attribute"></a>必要なデータバインディング属性を追加する

データ バインディングをサポートする簡単なコントロールに対しては <xref:System.ComponentModel.DefaultBindingPropertyAttribute> を実装します。

1. **PhoneNumberBox**コントロールをコードビューに切り替えます。 (**[表示]** メニューの **[コード]** を選択します。)

2. **PhoneNumberBox**のコードを次のコードに置き換えます。

     [!code-csharp[VbRaddataDisplaying#3](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-simple-data-binding_1.cs)]
     [!code-vb[VbRaddataDisplaying#3](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-simple-data-binding_1.vb)]

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-data-source-from-your-database"></a>データベースからデータソースを作成する

この手順では、 **データソース構成** ウィザードを使用して、Northwind サンプルデータベースのテーブルに基づいてデータソースを作成し `Customers` ます。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプルデータベースの設定の詳細については、「 [方法: サンプルデータベースをインストール](../data-tools/installing-database-systems-tools-and-samples.md)する」を参照してください。

1. [データ **ソース** ] ウィンドウを開くには、[ **データ** ] メニューの [ **データソースの表示**] をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして**データ ソース構成**ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、**[データベース]** を選択し、**[次へ]** をクリックします。

4. [ **データ接続の選択** ] ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. `Customers` テーブルを選択し、**[完了]** をクリックします。

     **NorthwindDataSet**がプロジェクトに追加され、[ `Customers` **データソース**] ウィンドウにテーブルが表示されます。

## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>PhoneNumberBox コントロールを使用するように phone 列を設定する

**[データ ソース]** ウィンドウでは、フォームにコントロールをドラッグする前に作成するコントロールを設定できます。

1. デザイナーで **Form1** を開きます。

2. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

3. **[Customers]** ノードのドロップダウン矢印をクリックし、コントロール リストの **[Details]** を選択します。

4. **[Phone]** 列のドロップダウン矢印をクリックし、**[Customize]** をクリックします。

5. **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[PhoneNumberBox]** を選択します。

6. **[Phone]** 列のドロップダウン矢印をクリックし、**[PhoneNumberBox]** をクリックします。

## <a name="add-controls-to-the-form"></a>フォームへのコントロールの追加

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

フォームにデータバインドコントロールを作成するには、[**データソース**] ウィンドウから [メインの**Customers** ] ノードをフォームにドラッグし、 **PhoneNumberBox**コントロールを使用して [**電話**] 列にデータを表示することを確認します。

説明のラベルが付いたデータ バインド コントロールとレコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

## <a name="run-the-application"></a>アプリケーションの実行

**F5** キーを押してアプリケーションを実行します。

## <a name="next-steps"></a>次の手順

アプリケーションの要件に応じて、データ バインディングをサポートするコントロールの作成後に、追加の操作を実行できます。 次の手順として、一般的には、次のようなことを実行します。

- 他のアプリケーションで再利用できるように、コントロール ライブラリにカスタム コントロールを配置します。

- より複雑なデータ バインディングのシナリオをサポートするコントロールを作成します。 詳細については、「 [複合データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md) する」および「 [参照データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)する」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
