---
title: データセットのデータの編集
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b51b5b4be12f76e2237ff93659617e1c1843722a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586654"
---
# <a name="edit-data-in-datasets"></a>データセットのデータの編集
データテーブル内のデータは、任意のデータベースのテーブルのデータを編集するのと同様に編集できます。 このプロセスには、テーブル内のレコードの挿入、更新、および削除を含めることができます。 データバインドフォームでは、ユーザーが編集できるフィールドを指定できます。 このような場合、データバインディングインフラストラクチャは、変更を後でデータベースに送り返すことができるように、すべての変更の追跡を処理します。 プログラムを使用してデータを編集し、それらの変更をデータベースに返信する場合は、変更の追跡を行うオブジェクトとメソッドを使用する必要があります。

実際のデータを変更するだけでなく、<xref:System.Data.DataTable> に対してクエリを実行して、特定のデータ行を返すこともできます。 たとえば、個々の行、特定のバージョンの行 (元の列と提案された行)、変更された行、またはエラーが発生した行に対してクエリを実行できます。

## <a name="to-edit-rows-in-a-dataset"></a>データセット内の行を編集するには
<xref:System.Data.DataTable>内の既存の行を編集するには、編集する <xref:System.Data.DataRow> を見つけて、更新された値を目的の列に割り当てます。

編集する行のインデックスがわからない場合は、`FindBy` メソッドを使用して、主キーで検索します。

[!code-csharp[VbRaddataEditing#3](../data-tools/codesnippet/CSharp/edit-data-in-datasets_1.cs)]
[!code-vb[VbRaddataEditing#3](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_1.vb)]

行インデックスがわかっている場合は、次のように行にアクセスして編集できます。

[!code-csharp[VbRaddataEditing#5](../data-tools/codesnippet/CSharp/edit-data-in-datasets_2.cs)]
[!code-vb[VbRaddataEditing#5](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_2.vb)]

## <a name="to-insert-new-rows-into-a-dataset"></a>データセットに新しい行を挿入するには
データバインドコントロールを使用するアプリケーションは、通常、 [BindingNavigator コントロール](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)の **[新規追加]** ボタンを使用して新しいレコードを追加します。

新しいレコードをデータセットに手動で追加するには、DataTable に対してメソッドを呼び出して、新しいデータ行を作成します。 次に、<xref:System.Data.DataTable>の <xref:System.Data.DataRow> コレクション (<xref:System.Data.DataTable.Rows%2A>) に行を追加します。

[!code-csharp[VbRaddataEditing#1](../data-tools/codesnippet/CSharp/edit-data-in-datasets_3.cs)]
[!code-vb[VbRaddataEditing#1](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_3.vb)]

データセットがデータソースに更新を送信するために必要な情報を保持するには、<xref:System.Data.DataRow.Delete%2A> メソッドを使用して、データテーブル内の行を削除します。 たとえば、アプリケーションで TableAdapter (または <xref:System.Data.Common.DataAdapter>) を使用している場合は、TableAdapter の `Update` メソッドによって、<xref:System.Data.DataRowState.Deleted>の <xref:System.Data.DataRow.RowState%2A> を持つデータベース内の行が削除されます。

アプリケーションでデータソースに更新を送信する必要がない場合は、データ行コレクション (<xref:System.Data.DataRowCollection.Remove%2A>) に直接アクセスすることでレコードを削除することができます。

#### <a name="to-delete-records-from-a-data-table"></a>データテーブルからレコードを削除するには

- <xref:System.Data.DataRow>の <xref:System.Data.DataRow.Delete%2A> メソッドを呼び出します。

     この方法では、レコードが物理的に削除されることはありません。 代わりに、レコードを削除対象としてマークします。

    > [!NOTE]
    > <xref:System.Data.DataRowCollection>の count プロパティを取得した場合、結果の数には、削除対象としてマークされているレコードが含まれます。 削除対象としてマークされていないレコードの正確な数を取得するには、各レコードの <xref:System.Data.DataRow.RowState%2A> プロパティを見て、コレクションをループ処理します。 (削除用にマークされたレコードには、<xref:System.Data.DataRowState.Deleted>の <xref:System.Data.DataRow.RowState%2A> があります)。または、行の状態に基づいてフィルター処理するデータセットのデータビューを作成し、そこから count プロパティを取得することもできます。

次の例は、<xref:System.Data.DataRow.Delete%2A> メソッドを呼び出して、`Customers` テーブルの最初の行を削除済みとしてマークする方法を示しています。

[!code-csharp[VbRaddataEditing#8](../data-tools/codesnippet/CSharp/edit-data-in-datasets_4.cs)]
[!code-vb[VbRaddataEditing#8](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_4.vb)]

## <a name="determine-if-there-are-changed-rows"></a>変更された行があるかどうかを判断する
データセット内のレコードを変更すると、その変更をコミットするまで変更情報が保持されます。 変更をコミットするには、データセットまたはデータテーブルの `AcceptChanges` メソッドを呼び出すか、TableAdapter またはデータアダプターの `Update` メソッドを呼び出す必要があります。

変更は、各データ行の2つの方法で追跡されます。

- 各データ行には、<xref:System.Data.DataRow.RowState%2A> (<xref:System.Data.DataRowState.Added>、<xref:System.Data.DataRowState.Modified>、<xref:System.Data.DataRowState.Deleted>、<xref:System.Data.DataRowState.Unchanged>など) に関連する情報が含まれています。

- 変更された各データ行には、その行の複数のバージョン (<xref:System.Data.DataRowVersion>)、元のバージョン (変更前)、および現在のバージョン (変更後) が含まれています。 変更が保留されている期間 (<xref:System.Data.DataTable.RowChanging> イベントに応答できる時間) には、3つ目のバージョン (提案されたバージョン) も使用できます。

データセットが変更された場合、データセットの <xref:System.Data.DataSet.HasChanges%2A> メソッドでは、`true` が返されます。 変更された行が存在することを確認した後は、`GetChanges` または <xref:System.Data.DataSet> の <xref:System.Data.DataTable> メソッドを呼び出して、変更された一連の行を取得できます。

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>行に変更が加えられたかどうかを確認するには

- データセットの <xref:System.Data.DataSet.HasChanges%2A> メソッドを呼び出し、変更された行があるかどうかをチェックします。

<xref:System.Data.DataSet.HasChanges%2A> メソッドから返された値をチェックし、`NorthwindDataset1` という名前のデータセットが変更された行があるかどうかを確認する方法を次の例に示します。

[!code-csharp[VbRaddataEditing#12](../data-tools/codesnippet/CSharp/edit-data-in-datasets_5.cs)]
[!code-vb[VbRaddataEditing#12](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_5.vb)]

## <a name="determine-the-type-of-changes"></a>変更の種類を決定する
また、<xref:System.Data.DataRowState> 列挙型から <xref:System.Data.DataSet.HasChanges%2A> メソッドに値を渡すことによって、データセットに加えられた変更の種類を確認することもできます。

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>行への変更の種類を確認するには

- <xref:System.Data.DataRowState> 値を <xref:System.Data.DataSet.HasChanges%2A> メソッドに渡します。

次の例では、`NorthwindDataset1` という名前のデータセットをチェックし、新しい行が追加されているかどうかを確認する方法を示します。

[!code-csharp[VbRaddataEditing#13](../data-tools/codesnippet/CSharp/edit-data-in-datasets_6.cs)]
[!code-vb[VbRaddataEditing#13](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_6.vb)]

## <a name="to-locate-rows-that-have-errors"></a>エラーのある行を検索するには
個々の列とデータ行を操作する場合、エラーが発生することがあります。 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、または <xref:System.Data.DataRow>にエラーが存在するかどうかを確認するには、`HasErrors` プロパティを確認します。

1. `HasErrors` プロパティを調べて、データセットにエラーがないかどうかを確認します。

2. `HasErrors` プロパティが `true`の場合は、テーブルのコレクションを反復処理してから行を通じて、エラーのある行を検索します。

[!code-csharp[VbRaddataEditing#23](../data-tools/codesnippet/CSharp/edit-data-in-datasets_7.cs)]
[!code-vb[VbRaddataEditing#23](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_7.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
