---
title: 同時実行例外の処理 |Microsoft Docs
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
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1b3f9bdaf5107f805100b938212128d42c0263dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670032"
---
# <a name="handle-a-concurrency-exception"></a>コンカレンシー例外を処理する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

2 人のユーザーが同じデータベースの同じデータを同時に変更しようとすると、コンカレンシー例外 (<xref:System.Data.DBConcurrencyException>) が発生します。 このチュートリアルでは、をキャッチする方法、 <xref:System.Data.DBConcurrencyException> エラーの原因となった行を特定する方法、およびその処理方法の方法を説明する Windows アプリケーションを作成します。

 ここでは次の手順を実行します。

1. 新しい **Windows アプリケーション** プロジェクトを作成します。

2. Northwind `Customers` テーブルに基づいて、新しいデータセットを作成します。

3. データを表示する <xref:System.Windows.Forms.DataGridView> を備えたフォームを作成します。

4. Northwind データベースの `Customers` テーブルからデータセットにデータを読み込みます。

5. Visual Studio の [Visual Database Tools](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1) を使用して、データテーブルに直接アクセスし、 `Customers` レコードを変更します。

6. 同じレコードを別の値に変更し、データセットを更新して、データベースへの変更の書き込みを試行します。これにより、同時実行エラーが発生します。

7. エラーをキャッチし、操作を継続してデータベースを更新するか、または更新をキャンセルするかを判断できるように、レコードの異なるバージョンを表示します。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを完了するための要件は次のとおりです。

- Northwind サンプル データベースにアクセスして更新を実行するためのアクセス許可。

> [!NOTE]
> 表示されるダイアログボックスとメニューコマンドは、アクティブな設定や使用しているエディションによっては、ヘルプに記載されているものと異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 新しい Windows アプリケーションの作成からチュートリアルを開始します。

#### <a name="to-create-a-new-windows-application-project"></a>新しい Windows アプリケーションプロジェクトを作成するには

1. [ **ファイル** ] メニューで、新しいプロジェクトを作成します。

2. [ **プロジェクトの種類** ] ペインで、プログラミング言語を選択します。

3. **[テンプレート]** ウィンドウで **[Windows アプリケーション]** を選択します。

4. プロジェクトに名前を指定し、[ `ConcurrencyWalkthrough` **OK]** を選択します。

     Visual Studio によってプロジェクトが **ソリューションエクスプローラー** に追加され、デザイナーに新しいフォームが表示されます。

## <a name="create-the-northwind-dataset"></a>Northwind データセットの作成
 このセクションでは、という名前のデータセットを作成し `NorthwindDataSet` ます。

#### <a name="to-create-the-northwinddataset"></a>NorthwindDataSet を作成するには

1. [ **データ** ] メニューの [ **新しいデータソースの追加**] をクリックします。

     [データソース構成ウィザード](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)が開きます。

2. [ **データソースの種類を選択**] 画面で、[ **データベース**] を選択します。

3. 使用可能な接続の一覧から、Northwind サンプルデータベースへの接続を選択します。接続の一覧で接続が使用できない場合は、[**新しい接続**] を選択します。

    > [!NOTE]
    > ローカルデータベースファイルに接続する場合は、ファイルをプロジェクトに追加するかどうかを確認するメッセージが表示されたら、[ **いいえ** ] を選択します。

4. [ **アプリケーション構成ファイルへの接続文字列の保存**] 画面で、[ **次へ**] を選択します。

5. [ **テーブル** ] ノードを展開し、テーブルを選択し `Customers` ます。 既定のデータセット名は、`NorthwindDataSet` です。

6. [ **完了** ] を選択して、データセットをプロジェクトに追加します。

## <a name="create-a-data-bound-datagridview-control"></a>データバインド DataGridView コントロールを作成する
 このセクションでは、 <xref:System.Windows.Forms.DataGridView> [**データソース**] ウィンドウから Windows フォームに**Customers**項目をドラッグして、を作成します。

#### <a name="to-create-a-datagridview-control-that-is-bound-to-the-customers-table"></a>Customers テーブルにバインドする DataGridView コントロールを作成するには

1. [ **データ** ] メニューの [ **データソースの表示** ] をクリックして、[ **データソース] ウィンドウ**を開きます。

2. [ **データソース** ] ウィンドウで、[ **NorthwindDataSet** ] ノードを展開し、[ **Customers** ] テーブルを選択します。

3. テーブルノードの下矢印を選択し、ドロップダウンリストで [ **DataGridView** ] を選択します。

4. テーブルをフォームの空の領域にドラッグします。

     <xref:System.Windows.Forms.DataGridView>という名前のコントロールとと `CustomersDataGridView` いう名前のが <xref:System.Windows.Forms.BindingNavigator> `CustomersBindingNavigator` 、にバインドされるフォームに追加され <xref:System.Windows.Forms.BindingSource> ます。このはにあり、のテーブルにバインドされ `Customers` `NorthwindDataSet` ます。

## <a name="test-the-form"></a>フォームをテストする
 フォームをテストして、ここまでの設定が期待どおりに動作することを確認します。

#### <a name="to-test-the-form"></a>フォームをテストするには

1. **F5 キーを押し**てアプリケーションを実行します。

     フォームには、 <xref:System.Windows.Forms.DataGridView> テーブルのデータを格納したコントロールが表示され `Customers` ます。

2. [ **デバッグ** ] メニューの [**デバッグの停止**] をクリックします。

## <a name="handleconcurrency-errors"></a>Handleconcurrency エラー
 エラーの処理方法は、アプリケーションを管理する特定のビジネスルールによって異なります。 このチュートリアルでは、次の方法を使用して、同時実行エラーを処理する方法の例を示します。

 Applicationpresents、次の3つのバージョンのレコードをユーザーに提示します。

- データベース内の現在のレコード

- データセットに読み込まれた元のレコード

- データセット内の提案された変更

  ユーザーは、提案されたバージョンでデータベースを上書きするか、更新をキャンセルし、データベースから新しい値をデータセットに再読み込むことができます。

#### <a name="to-enable-the-handling-of-concurrency-errors"></a>コンカレンシー エラーを処理できるようにするには

1. カスタム エラー ハンドラーの作成

2. ユーザーに対する選択肢の表示

3. ユーザーの応答の処理

4. 更新の再送、またはデータセット内のデータのリセット

### <a name="addcode-to-handle-the-concurrency-exception"></a>同時実行例外を処理するための addcode
 更新を実行しようとしたときに例外が発生した場合、通常は、発生した例外によって提供される情報を使用して何らかの処理を行います。

 このセクションでは、データベースの更新を試みるコードを追加します。また <xref:System.Data.DBConcurrencyException> 、発生する可能性のあるものや、その他の例外も処理します。

> [!NOTE]
> このチュートリアルの後半で、`CreateMessage` メソッドと `ProcessDialogResults` メソッドを追加します。

##### <a name="to-add-error-handling-for-the-concurrency-error"></a>コンカレンシー エラー用のエラー処理を追加するには

1. `Form1_Load` メソッドの下に次のコードを追加します。

     [!code-csharp[VbRaddataConcurrency#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#1)]
     [!code-vb[VbRaddataConcurrency#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#1)]

2. 次のように `CustomersBindingNavigatorSaveItem_Click` メソッドを `UpdateDatabase` メソッドの呼び出しに置き換えます。

     [!code-csharp[VbRaddataConcurrency#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#2)]
     [!code-vb[VbRaddataConcurrency#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#2)]

### <a name="displaychoices-to-the-user"></a>ユーザーへの displaychoices
 上のコードにより `CreateMessage` プロシージャが呼び出され、ユーザーにエラー情報が表示されます。 このチュートリアルでは、メッセージボックスを使用して、レコードのさまざまなバージョンをユーザーに表示します。これにより、ユーザーは、レコードを変更で上書きするか、編集をキャンセルするかを選択できます。 ユーザーがメッセージ ボックスのオプションを選択する (ボタンをクリックする) と、`ProcessDialogResult` メソッドに応答が渡されます。

##### <a name="to-create-the-message-to-display-to-the-user"></a>ユーザーに表示するメッセージを作成するには

- **コード エディター**に次のコードを追加して、メッセージを作成します。 このコードは、`UpdateDatabase` メソッドの下に入力します。

     [!code-csharp[VbRaddataConcurrency#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#4)]
     [!code-vb[VbRaddataConcurrency#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#4)]

### <a name="process-the-users-response"></a>ユーザーの応答の処理
 また、メッセージボックスに対するユーザーの応答を処理するコードも必要です。 オプションは、データベース内の現在のレコードを提案された変更で上書きするか、ローカルの変更を破棄し、現在データベース内にあるレコードを使用してデータテーブルを更新するかのどちらかです。 ユーザーが [はい] を選択 <xref:System.Data.DataTable.Merge%2A> すると、メソッドが呼び出され、 *preserveChanges* 引数がに設定され `true` ます。 これにより、レコードの元のバージョンがデータベース内のレコードと一致するようになったため、更新が成功します。

##### <a name="to-process-the-user-input-from-the-message-box"></a>メッセージ ボックスからのユーザーの入力を処理するには

- 前のセクションで追加したコードの下に次のコードを追加します。

     [!code-csharp[VbRaddataConcurrency#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#3)]
     [!code-vb[VbRaddataConcurrency#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#3)]

## <a name="test-the-form"></a>フォームをテストする
 フォームをテストして、期待どおりに動作することを確認します。 コンカレンシー違反をシミュレートするには、NorthwindDataSet にデータを読み込んだ後で、データベースのデータを変更する必要があります。

#### <a name="to-test-the-form"></a>フォームをテストするには

1. **F5 キーを押し**てアプリケーションを実行します。

2. フォームが表示されたら、実行を継続したまま Visual Studio IDE に切り替えます。

3. **[表示]** メニューの **[サーバー エクスプローラー]** を選択します。

4. **サーバー エクスプローラー**で、アプリケーションで使用する接続を展開し、次に **[テーブル]** ノードを展開します。

5. **Customers**テーブルを右クリックし、[**テーブルデータの表示**] をクリックします。

6. 最初のレコード ( `ALFKI` ) で、 `ContactName` をに変更 `Maria Anders2` します。

    > [!NOTE]
    > 別の行に移動し、変更をコミットします。

7. `ConcurrencyWalkthrough` の実行中のフォームに切り替えます。

8. フォーム () の最初のレコードで `ALFKI` 、 `ContactName` をに変更 `Maria Anders1` します。

9. **[保存]** ボタンを選択します。

     コンカレンシー エラーが発生し、メッセージ ボックスが表示されます。

10. [ **いいえ** ] を選択すると、更新がキャンセルされ、現在データベース内にある値によってデータセットが更新されます。 **[はい]** を選択すると、提示された値がデータベースに書き込まれます。

## <a name="see-also"></a>参照

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)