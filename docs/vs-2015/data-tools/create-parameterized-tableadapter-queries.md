---
title: パラメーター付きの TableAdapter クエリを作成する
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- TableAdapters, parameterized queries
- data [Visual Studio], searching data
- queries [Visual Studio], creating
- TableAdapters, searching data
- queries [Visual Studio], TableAdapters
ms.assetid: 104d1d19-b5a9-4071-b81e-1b3af08e9c7b
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 560587e70365a485c3391a0623b959f88d417698
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671065"
---
# <a name="create-parameterized-tableadapter-queries"></a>パラメーター付きの TableAdapter クエリを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

パラメーター クエリは、クエリ内の WHERE 句の条件を満たすデータを返します。 たとえば、顧客リストをパラメーター化して、顧客のリストを戻す SQL ステートメントに `WHERE City = @City` を追加することで、特定の都市の顧客のみが表示されるようにできます。

パラメーター化された TableAdapter クエリは、データセットデザイナーで作成します。 また、[**データ**] メニューの [**データソースのパラメーター**化] コマンドを使用して、Windows アプリケーションで作成することもできます。 [ **データソース** のパラメーター化] コマンドを実行すると、フォームにコントロールが作成され、パラメーター値を入力してクエリを実行できます。

> [!NOTE]
> パラメーター化クエリを作成する場合は、コーディングしているデータベースに固有のパラメーター表記を使用します。 たとえば、Access データ ソースと OleDb データ ソースは疑問符 "?" を使用してパラメーターを表すため、WHERE 句は `WHERE City = ?` のようになります。

> [!NOTE]
> 表示されるダイアログボックスとメニューコマンドは、アクティブな設定や使用しているエディションによっては、ヘルプに記載されているものと異なる場合があります。 設定を変更するには、[ **ツール** ] メニューの [ **設定のインポートとエクスポート**] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="create-a-parameterized-tableadapter-query"></a>パラメーター化された TableAdapter クエリを作成する

- 新しい TableAdapter を作成し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。 詳細については、「 [tableadapter の作成と構成](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

     - または -

- 既存の TableAdapter にクエリを追加し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。

### <a name="create-a-parameterized-query-while-designing-a-data-bound-form"></a>データバインドフォームのデザイン時にパラメーター化クエリを作成する

1. フォーム上の既にデータセットにバインドされているコントロールを選択します。 詳細については、「 [Visual Studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」を参照してください。

2. [ **データ** ] メニューの [**クエリの追加**] をクリックします。

3. **[検索条件ビルダー]** ダイアログ ボックスの設定を完了し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。

### <a name="add-a-query-to-an-existing-data-bound-form"></a>既存のデータバインドフォームにクエリを追加する

1. **Windows フォーム デザイナー**でフォームを開きます。

2. [ **データ** ] メニューの [ **クエリ** または **データスマートタグ**の追加] をクリックします。

   > [!NOTE]
   > **[データ]** メニューの **[クエリの追加]** が使用できない場合は、パラメーターの追加先のデータ ソースを表示するフォーム上のコントロールを選択します。 たとえば、フォームに <xref:System.Windows.Forms.DataGridView> コントロールのデータが表示される場合は、そのコントロールを選択します。 フォームに個々のコントロールのデータが表示される場合は、いずれかのデータ バインド コントロールを選択します。

3. **[データソーステーブルの選択**] 領域で、パラメーター化を追加する tablethat 選択します。

4. 新しいクエリを作成する場合は、**[新しいクエリ名]** ボックスに名前を入力します。

    - または -

    **[既存のクエリ名]** ボックスでクエリを選択します。

5. [ **クエリ] テキスト** ボックスに、パラメーターを受け取るクエリを入力します。

6. **[OK]** を選択します。

    パラメーターを入力するコントロールと **[読み込み]** ボタンが、<xref:System.Windows.Forms.ToolStrip> コントロールのフォームに追加されます。

   現在の値がないレコードをクエリする場合は、TableAdapter パラメーターに null 値を割り当てることができます。 たとえば、次のクエリでは、句にパラメーターを指定しているとし `ShippedDate` `WHERE` ます。

   ```sql
   SELECT CustomerID, OrderDate, ShippedDate
   FROM Orders
   WHERE (ShippedDate = @ShippedDate) OR
   (ShippedDate IS NULL)
   ```

これが TableAdapter に対するクエリであった場合は、次のコードで出荷されていないすべての注文に対してクエリを実行できます。

   [!code-csharp[VbRaddataTableAdapters#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Form2.cs#8)]
   [!code-vb[VbRaddataTableAdapters#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Form2.vb#8)]

### <a name="enable-a-query-to-accept-null-values"></a>クエリで null 値を許容できるようにする

1. **データセットデザイナー**で、null パラメーター値を受け入れる必要がある TableAdapter クエリを選択します。

2. [ **プロパティ** ] ウィンドウで、[ **パラメーター**] を選択します。 次に、省略記号ボタン ([.**..**]) をクリックして、 **Parameters コレクションエディター**を開きます。

3. Null 値を許容するパラメーターを選択し、 **Allowdbnull** プロパティをに設定し `true` ます。

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)