---
title: パラメーター付きの TableAdapter クエリを作成する
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- TableAdapters, parameterized queries
- data [Visual Studio], searching data
- queries [Visual Studio], creating
- TableAdapters, searching data
- queries [Visual Studio], TableAdapters
ms.assetid: 104d1d19-b5a9-4071-b81e-1b3af08e9c7b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a2b94e10dd09d26a17a7574db97880567f7725cd
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282606"
---
# <a name="create-parameterized-tableadapter-queries"></a>パラメーター付きの TableAdapter クエリを作成する

パラメーター クエリは、クエリ内の WHERE 句の条件を満たすデータを返します。 たとえば、顧客リストをパラメーター化して、顧客のリストを戻す SQL ステートメントに `WHERE City = @City` を追加することで、特定の都市の顧客のみが表示されるようにできます。

パラメーター化された TableAdapter クエリは、**データセットデザイナー**で作成します。また、[**データ**] メニューの [**データソースのパラメーター**化] コマンドを使用して、Windows アプリケーションで作成することもできます。 [**データソース**のパラメーター化] コマンドを実行すると、フォームにコントロールが作成され、パラメーター値を入力してクエリを実行できます。

> [!NOTE]
> パラメーター化クエリを作成する場合は、コーディングしているデータベースに固有のパラメーター表記を使用します。 たとえば、Access データ ソースと OleDb データ ソースは疑問符 "?" を使用してパラメーターを表すため、WHERE 句は `WHERE City = ?` のようになります。

## <a name="create-a-parameterized-tableadapter-query"></a>パラメーター化された TableAdapter クエリを作成する

### <a name="to-create-a-parameterized-query-in-the-dataset-designer"></a>データセット デザイナーでパラメーター クエリを作成するには

- 新しい TableAdapter を作成し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。 詳細については、「 [tableadapter の作成と構成](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

     \- または -

- 既存の TableAdapter にクエリを追加し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。

### <a name="to-create-a-parameterized-query-while-designing-a-data-bound-form"></a>データ バインド フォームの設計時にパラメーター クエリを作成するには

1. フォーム上の既にデータセットにバインドされているコントロールを選択します。 詳細については、「 [Visual Studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」を参照してください。

2. [**データ**] メニューの [**クエリの追加**] をクリックします。

3. **[検索条件ビルダー]** ダイアログ ボックスの設定を完了し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。

### <a name="to-add-a-query-to-an-existing-data-bound-form"></a>既存のデータ バインド フォームにクエリを追加するには

1. **Windows フォーム デザイナー**でフォームを開きます。

2. [**データ**] メニューの [**クエリ**または**データスマートタグ**の追加] をクリックします。

    > [!NOTE]
    > **[データ]** メニューの **[クエリの追加]** が使用できない場合は、パラメーターの追加先のデータ ソースを表示するフォーム上のコントロールを選択します。 たとえば、フォームに <xref:System.Windows.Forms.DataGridView> コントロールのデータが表示される場合は、そのコントロールを選択します。 フォームに個々のコントロールのデータが表示される場合は、いずれかのデータ バインド コントロールを選択します。

3. **[データソーステーブルの選択**] 領域で、パラメーター化を追加するテーブルを選択します。

4. 新しいクエリを作成する場合は、**[新しいクエリ名]** ボックスに名前を入力します。

     \- または -

     **[既存のクエリ名]** ボックスでクエリを選択します。

5. [**クエリ] テキスト**ボックスに、パラメーターを受け取るクエリを入力します。

6. **[OK]** を選択します。

     パラメーターを入力するコントロールと **[読み込み]** ボタンが、<xref:System.Windows.Forms.ToolStrip> コントロールのフォームに追加されます。

### <a name="query-for-null-values"></a>Null 値のクエリ

現在の値がないレコードをクエリする場合は、TableAdapter パラメーターに null 値を割り当てることができます。 たとえば、次のクエリでは、句にパラメーターを指定しているとし `ShippedDate` `WHERE` ます。

```sql
SELECT CustomerID, OrderDate, ShippedDate
FROM Orders
WHERE (ShippedDate = @ShippedDate) OR (ShippedDate IS NULL)
```

これが TableAdapter に対するクエリであった場合は、次のコードで出荷されていないすべての注文に対してクエリを実行できます。

[!code-csharp[VbRaddataTableAdapters#8](../data-tools/codesnippet/CSharp/create-parameterized-tableadapter-queries_1.cs)]
[!code-vb[VbRaddataTableAdapters#8](../data-tools/codesnippet/VisualBasic/create-parameterized-tableadapter-queries_1.vb)]

クエリで null 値を使用できるようにするには、次のようにします。

1. **データセットデザイナー**で、null パラメーター値を受け入れる必要がある TableAdapter クエリを選択します。

2. [**プロパティ**] ウィンドウで、[**パラメーター**] を選択し、省略記号ボタン ([.**..**]) をクリックして、[**パラメーターコレクションエディター**] を開きます。

3. Null 値を許容するパラメーターを選択し、 **Allowdbnull**プロパティをに設定し `true` ます。

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
