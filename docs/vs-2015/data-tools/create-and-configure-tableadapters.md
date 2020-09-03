---
title: Tableadapter の作成と構成 |Microsoft Docs
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
- table adapters, creating
- creating TableAdapters
- data [Visual Studio], creating data components
- data [Visual Studio], TableAdapters
- data [Visual Studio], creating table adapters
ms.assetid: 08630d69-0d6c-4e8f-b42d-2922f45f8415
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9a2136960dfcbbbcf63fbefeb16d527793d4b939
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72631032"
---
# <a name="create-and-configure-tableadapters"></a>Tableadapter の作成および構成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TableAdapter を使用すると、アプリケーションとデータベース間で通信できます。 これらは、データベースに接続し、クエリまたはストアドプロシージャを実行して、新しいデータテーブルを返すか、または返されたデータを既存のに格納し <xref:System.Data.DataTable> ます。 Tableadapter では、更新されたデータをアプリケーションからデータベースに送信することもできます。

 Tableadapter は、次のいずれかの操作を実行すると作成されます。

- [データソース構成ウィザード](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)を実行し、**データベース**または**Web サービス**のいずれかのデータソースの種類を選択します。

- [サーバーエクスプローラー](https://msdn.microsoft.com/library/4ea29b3b-bbb2-45e4-9082-eaf635c41c4d)から**データセットデザイナー**にデータベースオブジェクトをドラッグします。

  新しい TableAdapter を作成し、データソースを使用して構成するには、ツールボックスから **データセットデザイナー** サーフェイスの空の領域に tableadapter をドラッグします。

  Tableadapter の概要については、「Tableadapter を使用した [データセットの読み込み](../data-tools/fill-datasets-by-using-tableadapters.md)」を参照してください。

  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="use-the-tableadapter-configuration-wizard"></a>TableAdapter 構成ウィザードの使用
 Tableadapter とそれに関連する Datatable を作成または編集するには、 **Tableadapter 構成ウィザード** を実行します。 **データセットデザイナー**で既存の TableAdapter を右クリックして構成できます。

 ![レーダーデータテーブルアダプター構成ウィザード](../data-tools/media/raddata-table-adapter-configuration-wizard.png "レーダーデータテーブルアダプター構成ウィザード")

 **データセットデザイナー**がフォーカスされているときにツールボックスから新しい TableAdapter をドラッグすると、tableadapter の接続先のデータソースと、データベース、SQL ステートメント、またはストアドプロシージャとの通信に使用する必要があるコマンドの種類を指定するように求められます。 データソースに既に関連付けられている TableAdapter を構成している場合は、表示されません。

- Create メソッドを使用して **データベースオプションに更新を直接送信** することは、 `GenerateDBDirectMethods` プロパティを true に設定することと同じです。 元の SQL ステートメントに十分な情報が含まれていないか、クエリが更新可能なクエリではない場合、このオプションは使用できません。 たとえば、 **結合** クエリや、単一の (スカラー) 値を返すクエリで、このような状況が発生する可能性があります。

- データベースに対する適切な権限を持っている場合は、基になるデータベースに新しいストアドプロシージャを作成することもできます。 これらのアクセス許可がない場合、これはオプションではありません。

- また、TableAdapter の **SELECT**、 **INSERT**、 **UPDATE**、および **DELETE** の各コマンドに対して、既存のストアドプロシージャを実行することもできます。 たとえば、 **Update** コマンドに割り当てられているストアドプロシージャは、メソッドが呼び出されたときに実行され `TableAdapter.Update()` ます。

     選択したストアド プロシージャのパラメーターを、データ テーブルの対応する列に割り当てます。 たとえば、ストアドプロシージャがという名前のパラメーターを受け取り、 `@CompanyName` テーブルの列に渡す場合は、 `CompanyName` パラメーターの **Source 列** を `@CompanyName` に設定 `CompanyName` します。

    > [!NOTE]
    > SELECT コマンドに割り当てられているストアドプロシージャは、ウィザードの次の手順で名前を指定した TableAdapter のメソッドを呼び出すことによって実行されます。 既定のメソッドは `Fill` であるため、選択プロシージャを実行するために通常使用されるコードは `TableAdapter.Fill(tableName)` です。 既定の名前をから変更する場合は `Fill` 、を `Fill` 割り当てた名前に置き換え、"tableadapter" を tableadapter の実際の名前 (たとえば、) に置き換え `CustomersTableAdapter` ます。

- ウィザードの **[詳細設定] オプション** を使用すると、[ **SQL ステートメントの生成** ] ページで定義されている select ステートメントに基づいて、INSERT、UPDATE、および DELETE の各ステートメントを生成できます。 オプティミスティック同時実行制御を使用し、INSERT ステートメントと UPDATE ステートメントの実行後にデータテーブルを更新するかどうかを指定します。

## <a name="configure-a-tableadapters-fill-method"></a>TableAdapter の Fill メソッドを構成する
 場合によっては、TableAdapter のテーブルのスキーマを変更する必要があります。 これを行うには、TableAdapter の主要な方法を変更し `Fill` ます。 Tableadapter は、 `Fill` 関連付けられたデータテーブルのスキーマを定義する主要なメソッドを使用して作成されます。 主 `Fill` な方法は、TableAdapter を最初に構成したときに入力したクエリまたはストアドプロシージャに基づいています。 データセットデザイナーのデータテーブルの下にある最初の (最上位の) メソッドです。

 ![複数のクエリがある TableAdapter](../data-tools/media/tableadapter.gif "TableAdapter")

 TableAdapter の main メソッドに対して行った変更 `Fill` は、関連付けられたデータテーブルのスキーマに反映されます。 たとえば、main メソッドのクエリから列を削除すると、 `Fill` 関連付けられているデータテーブルから列も削除されます。 さらに、main メソッドから列を削除すると、 `Fill` その TableAdapter の追加クエリから列が削除されます。

 Tableadapter クエリの構成ウィザードを使用すると、TableAdapter の追加のクエリを作成および編集できます。 これらの追加のクエリは、スカラー値を返さない限り、テーブルスキーマに準拠している必要があります。  追加のクエリには、指定した名前 (など) があり `CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")` ます。

#### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>新しいクエリを使用して TableAdapter クエリの構成ウィザードを開始するには

1. **データセット デザイナー**でご自分のデータセットを開きます。

2. 新しいクエリを作成する場合は、[**ツールボックス**] の [**データセット**] タブから**クエリ**オブジェクトをにドラッグする <xref:System.Data.DataTable> か、TableAdapter のショートカットメニューから [**クエリの追加**] を選択します。 **クエリ**オブジェクトを**データセットデザイナー**の空の領域にドラッグして、関連付けられていない TableAdapter を作成することもでき <xref:System.Data.DataTable> ます。 これらのクエリは、単一の (スカラー) 値を返すことも、データベースに対して UPDATE、INSERT、または DELETE コマンドを実行することもできます。

3. [ **データ接続の選択** ] 画面で、クエリが使用する接続を選択または作成します。

    > [!NOTE]
    > この画面は、デザイナーが使用する適切な接続を判断できない場合、または接続が使用できない場合にのみ表示されます。

4. [ **コマンドの種類を選択** ] 画面で、データベースからデータをフェッチする方法を次の中から選択します。

    - **Sql** ステートメントを使用すると、データベースからデータを選択するための sql ステートメントを入力できます。

    - **新しいストアドプロシージャを作成** すると、指定した select ステートメントに基づいて、ウィザードで新しいストアドプロシージャ (データベース内) を作成できます。

    - **既存のストアドプロシージャを使用** すると、クエリの実行時に既存のストアドプロシージャを実行できます。

#### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>既存のクエリで TableAdapter クエリの構成ウィザードを起動するには

- 既存の TableAdapter クエリを編集している場合は、クエリを右クリックし、ショートカットメニューの [ **構成** ] をクリックします。

    > [!NOTE]
    > TableAdapter のメインクエリを右クリックすると、TableAdapter とスキーマが再構成され <xref:System.Data.DataTable> ます。 ただし、TableAdapter に対して追加のクエリを右クリックすると、選択したクエリのみが構成されます。 Tableadapter の **構成ウィザード** は tableadapter の定義を再構成しますが、tableadapter クエリの構成ウィザードでは、選択したクエリのみを再構成します。

#### <a name="to-add-a-global--query-to-a-tableadapter"></a>TableAdapter にグローバルクエリを追加するには

- *グローバルクエリ* は、単一の (スカラー) 値または値を返さない SQL クエリです。 通常、グローバル関数は、挿入、更新、削除などのデータベース操作を実行します。 また、テーブル内の顧客の数や特定の注文のすべての品目の合計料金などの情報も集計されます。

     グローバルクエリを追加するには、[**ツールボックス**] の [**データセット**] タブから**データセットデザイナー**の空の領域に**クエリ**オブジェクトをドラッグします。

- たとえば、必要なタスクを実行するクエリを指定 `SELECT COUNT(*) AS CustomerCount FROM Customers` します。

    > [!NOTE]
    > **クエリ**オブジェクトを**データセットデザイナー**に直接ドラッグすると、スカラー (単一) 値のみを返すメソッドが作成されます。 選択したクエリまたはストアドプロシージャで複数の値が返される場合がありますが、ウィザードによって作成されるメソッドは、1つの値のみを返します。 たとえば、クエリは、返されたデータの最初の行の最初の列を返す場合があります。

## <a name="see-also"></a>参照
 [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
